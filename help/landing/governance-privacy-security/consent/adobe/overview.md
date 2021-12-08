---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Processamento de consentimento no Adobe Experience Platform
topic-legacy: getting started
description: Saiba como processar sinais de consentimento do cliente no Adobe Experience Platform usando o padrão Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: f9ccce8943e2aaf65cd3e0ffe2b974a668bba9b7
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 0%

---

# Processamento de consentimento no Adobe Experience Platform

O Adobe Experience Platform permite processar os dados de consentimento coletados dos clientes e integrá-los aos perfis de clientes armazenados. Esses dados podem ser usados por processos de downstream para determinar se a coleta de dados ocorre para um cliente específico ou se seus perfis são usados para fins específicos. Por exemplo, os dados de consentimento para um perfil específico podem determinar se podem ser incluídos em um segmento de público-alvo exportado ou se podem participar de canais de marketing específicos, como email, mensagens de texto ou notificações por push.

Este documento fornece uma visão geral de como configurar as operações de dados da plataforma para assimilar dados de consentimento do cliente gerados por uma plataforma de gerenciamento de consentimento (CMP) e integrar esses dados aos perfis do cliente para casos de uso de downstream.

>[!NOTE]
>
>Este documento se concentra no processamento de dados de consentimento usando o padrão Adobe. Se você estiver processando dados de consentimento em conformidade com a Estrutura de transparência e consentimento (TCF) 2.0 do IAB, consulte o guia em [Suporte ao TCF 2.0 no Real-time Customer Data Platform](../iab/overview.md).

## Pré-requisitos

Este guia requer um entendimento prático dos vários serviços do Experience Platform envolvidos no processamento de dados de consentimento:

* [Experience Data Model (XDM)](../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [Perfil do cliente em tempo real](../../../../profile/home.md): Usos [!DNL Identity Service] recursos para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. O Perfil do cliente em tempo real extrai dados do Data Lake e mantém perfis de cliente em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços da plataforma ao seu site voltado para o cliente.
   * [Comandos de consentimento do SDK](../../../../edge/consent/supporting-consent.md): Uma visão geral do caso de uso dos comandos SDK relacionados ao consentimento mostrados neste guia.
* [Serviço de segmentação do Adobe Experience Platform](../../../../segmentation/home.md): Permite dividir os dados do Perfil do cliente em tempo real em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

## Resumo do fluxo de processamento do consentimento {#summary}

A seguir, descreve como os dados de consentimento são processados após a configuração correta do sistema:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo no site.
1. Em cada carregamento de página (ou quando o CMP detecta uma alteração nas preferências de consentimento), um script personalizado no site mapeia as preferências atuais para um objeto XDM padrão. Esse objeto é então passado para o SDK da Web da plataforma `setConsent` comando.
1. When `setConsent` for chamado, o SDK da Web da plataforma verificará se os valores de consentimento são diferentes daqueles que recebeu pela última vez. Se os valores forem diferentes (ou não houver um valor anterior), os dados estruturados de consentimento/preferência serão enviados para o Adobe Experience Platform.
1. Os dados de consentimento/preferência são assimilados em um [!DNL Profile]conjunto de dados habilitado para o , cujo esquema contém campos de consentimento/preferência.

Além dos comandos do SDK acionados por ganchos de alteração de consentimento da CMP, os dados de consentimento também podem fluir para o Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que sejam carregados diretamente para um [!DNL Profile]Conjunto de dados habilitado para .

### Execução do consentimento

Na versão atual do suporte de processamento de consentimento no Platform, somente a permissão de coleta de dados (`collect.val`) é aplicada automaticamente pelo SDK da Web da plataforma. Embora consentimentos e preferências mais granulares possam ser coletados e mantidos em perfis de clientes, esses sinais adicionais devem ser aplicados manualmente em seus próprios processos de downstream.

>[!NOTE]
>
>Para obter mais informações sobre a estrutura dos campos de consentimento do XDM mencionados acima, consulte o guia no [[!UICONTROL Consentimentos e preferências] tipo de dados](../../../../xdm/data-types/consents.md).

Depois que o sistema é configurado, o SDK da Web da plataforma interpreta o valor de consentimento da coleta de dados para o usuário atual a fim de determinar se os dados devem ser enviados para a Rede de borda da Adobe Experience Platform, descartados do cliente ou persistentes até que a permissão da coleta de dados seja definida como sim ou não.

## Determine como gerar dados de consentimento do cliente em sua CMP {#consent-data}

Como cada sistema CMP é exclusivo, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento à medida que interagirem com seu serviço. Uma maneira comum de fazer isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao seguinte exemplo:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Essa caixa de diálogo deve permitir que o cliente opte por participar ou não de casos de uso específicos de marketing e personalização para seus dados. Esses consentimentos e preferências devem estar em conformidade com o modelo de dados definido para a variável [!DNL Profile]Conjunto de dados habilitado para a próxima etapa.

## Adicionar campos de consentimento padronizados a um [!DNL Profile]Conjunto de dados habilitado para o {#dataset}

Os dados de consentimento do cliente devem ser enviados para um [!DNL Profile]conjunto de dados habilitado para o , cujo esquema contém campos de consentimento. Esses campos devem ser incluídos no mesmo esquema e conjunto de dados que você usa para capturar informações de atributos sobre clientes individuais.

Consulte o tutorial em [configuração de um conjunto de dados para capturar dados de consentimento](./dataset.md) para obter etapas detalhadas sobre como adicionar esses campos obrigatórios a um [!DNL Profile]Conjunto de dados habilitado para o , antes de continuar com este guia.

## Atualizar [!DNL Profile] mesclar políticas para incluir dados de consentimento {#merge-policies}

Depois de criar uma [!DNL Profile]Conjunto de dados habilitado para processar dados de consentimento, você deve garantir que suas políticas de mesclagem tenham sido configuradas para sempre incluir campos de consentimento em cada perfil de cliente. Isso envolve definir a precedência do conjunto de dados para que seu conjunto de dados de consentimento seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

>[!NOTE]
>
>Se você não tiver conjuntos de dados em conflito, deverá definir a precedência do carimbo de data e hora para sua política de mesclagem. Isso ajuda a garantir que o consentimento mais recente especificado por um cliente seja a configuração de consentimento usada.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, comece lendo a variável [visão geral das políticas de mesclagem](../../../../profile/merge-policies/overview.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus perfis incluam todos os atributos de consentimento necessários fornecidos pelo [!UICONTROL Consentimentos e preferências] grupo de campos de esquema, conforme descrito no guia em [preparação do conjunto de dados](./dataset.md).

## Trazer dados de consentimento para o Platform

Depois de ter seus conjuntos de dados e políticas de mesclagem para representar os campos de consentimento necessários nos perfis do cliente, a próxima etapa é trazer os dados de consentimento em si para a Platform.

Principalmente, você deve usar o SDK da Web da Adobe Experience Platform para enviar dados de consentimento à Platform sempre que eventos de alteração de consentimento forem detectados pelo CMP. Se estiver coletando dados de consentimento em uma plataforma móvel, você deve usar o SDK do Adobe Experience Platform Mobile. Você também pode optar por assimilar seus dados de consentimento coletados diretamente, mapeando-os para o esquema XDM do conjunto de dados de consentimento e enviando-os para a Platform por meio da assimilação em lote.

Os detalhes de cada um desses métodos são fornecidos nas subseções abaixo.

### Configurar o SDK da Web do Experience Platform para processar dados de consentimento {#web-sdk}

Depois de configurar o CMP para acompanhar eventos de alteração de consentimento no site, você pode integrar o SDK da Web do Experience Platform para receber as configurações de consentimento atualizadas e enviá-las para a plataforma em cada carregamento de página e sempre que ocorrerem eventos de alteração de consentimento. Consulte o guia sobre [configuração do SDK da Web para processar os dados de consentimento do cliente](../sdk.md) para obter mais informações.

### Configurar o SDK do Experience Platform Mobile para processar dados de consentimento {#mobile-sdk}

Se as preferências de consentimento do cliente forem necessárias em seu aplicativo móvel, você poderá integrar o SDK do Experience Platform Mobile para recuperar e atualizar as configurações de consentimento, enviando-o para a Plataforma sempre que a API de consentimento for chamada.

Consulte a documentação do SDK móvel para [configuração da extensão para dispositivos móveis Consent](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) e [uso da API de consentimento](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). Para obter mais detalhes sobre como lidar com preocupações de privacidade usando o SDK móvel, consulte a seção [Privacidade e o GDPR](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### Assimilar dados de consentimento em conformidade com o XDM diretamente {#batch}

Você pode assimilar dados de consentimento compatíveis com XDM de um arquivo CSV usando a assimilação em lote. Isso pode ser útil se você tiver um backlog de dados de consentimento coletados anteriormente que ainda não foram integrados aos perfis de clientes.

Siga o tutorial em [mapeamento de um arquivo CSV para XDM](../../../../ingestion/tutorials/map-a-csv-file.md) para saber como converter seus campos de dados para XDM e assimilá-los em Platform. Ao selecionar o [!UICONTROL Destino] para o mapeamento , certifique-se de selecionar a variável **[!UICONTROL Usar conjunto de dados existente]** e escolha a [!DNL Profile]Conjunto de dados de consentimento habilitado para o uso anterior.

## Testar sua implementação {#test-implementation}

Depois de assimilar os dados de consentimento do cliente em sua [!DNL Profile]conjunto de dados habilitado para o , você pode verificar seus perfis atualizados para ver se eles contêm atributos de consentimento.

>[!IMPORTANT]
>
>Para visualizar os atributos de um perfil existente na interface do usuário, você deve saber pelo menos um valor de identidade (e seu namespace correspondente) associado a esse perfil.
>
>Se você não tiver acesso a essas informações, poderá optar por assimilar seus próprios dados de consentimento de teste e associá-los a um valor/namespace de identidade conhecido por você.

Consulte a seção sobre [navegar pelos perfis por identidade](../../../../profile/ui/user-guide.md#browse) no [!DNL Profile] Guia da interface do usuário para obter etapas específicas sobre como pesquisar os detalhes de um perfil.

Por padrão, os novos atributos de consentimento não aparecerão no painel de um perfil. Portanto, você deve navegar até a variável **[!UICONTROL Atributos]** na página de detalhes de um perfil para confirmar que eles foram assimilados conforme esperado. Consulte o guia sobre [painel de perfis](../../../../profile/ui/profile-dashboard.md) para saber como personalizar o painel de acordo com suas necessidades.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Próximas etapas

Este guia cobriu como configurar as operações da Platform para processar os dados de consentimento do cliente usando o padrão do Adobe e fazer com que esses atributos sejam representados nos perfis do cliente. Agora é possível integrar as preferências de consentimento do cliente como um fator determinante na qualificação de segmento e outros casos de uso downstream.

Para obter mais informações sobre os recursos relacionados à privacidade do Experience Platform, consulte a visão geral sobre [governança, privacidade e segurança na plataforma](../../overview.md).
