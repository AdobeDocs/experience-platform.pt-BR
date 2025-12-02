---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Processamento de consentimento no Adobe Experience Platform
description: Saiba como processar sinais de consentimento do cliente no Adobe Experience Platform usando o padrão Adobe 2.0.
role: Developer
feature: Consent
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# Processamento de consentimento no Adobe Experience Platform

O Adobe Experience Platform permite processar os dados de consentimento coletados dos clientes e integrá-los aos perfis de clientes armazenados. Esses dados podem ser usados por processos de downstream para determinar se a coleta de dados ocorre para um cliente específico ou se seus perfis são usados para fins específicos. Por exemplo, os dados de consentimento de um perfil específico podem determinar se ele pode ser incluído em um segmento de público-alvo exportado ou se pode participar de canais de marketing específicos, como email, mensagens de texto ou notificações por push.

Este documento fornece uma visão geral de como configurar as operações de dados do Experience Platform para assimilar dados de consentimento do cliente gerados por uma plataforma de gerenciamento de consentimento (CMP) e integrar esses dados aos perfis do cliente para casos de uso downstream.

>[!NOTE]
>
>Este documento se concentra no processamento de dados de consentimento usando o padrão Adobe. Se você estiver processando dados de consentimento em conformidade com a Estrutura de Transparência e Consentimento (TCF) do IAB 2.0, consulte o manual sobre o suporte do [TCF 2.0 no Adobe Real-Time Customer Data Platform](../iab/overview.md).

## Pré-requisitos

Este guia requer uma compreensão funcional dos vários serviços da Experience Platform envolvidos no processamento de dados de consentimento:

* [Experience Data Model (XDM)](/help/xdm/home.md): a estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md): resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir as identidades de vários dispositivos e sistemas.
* [Perfil de cliente em tempo real](/help/profile/home.md): usa os recursos do [!DNL Identity Service] para criar perfis de cliente detalhados a partir dos seus conjuntos de dados em tempo real. O Perfil do cliente em tempo real extrai dados do Data Lake e mantém os perfis do cliente em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md): uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços Experience Platform ao seu site voltado para o cliente.
   * [Comandos de consentimento do SDK](/help/collection/js/commands/setconsent.md): uma visão geral dos casos de uso dos comandos do SDK relacionados ao consentimento mostrados neste guia.
* [Serviço de segmentação da Adobe Experience Platform](/help/segmentation/home.md): permite dividir os dados do Perfil do cliente em tempo real em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

## Resumo do fluxo de processamento de consentimento {#summary}

A seguir está uma descrição de como os dados de consentimento são processados após o sistema ter sido configurado corretamente:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo no site.
1. Em cada carregamento de página (ou quando o CMP detecta uma alteração nas preferências de consentimento), um script personalizado no site mapeia as preferências atuais para um objeto XDM padrão. Esse objeto é então passado para o comando `setConsent` do Experience Platform Web SDK.
1. Quando `setConsent` é chamado, o Experience Platform Web SDK verifica se os valores de consentimento são diferentes daqueles que recebeu pela última vez. Se os valores forem diferentes (ou se não houver um valor anterior), os dados estruturados de consentimento/preferência serão enviados para a Adobe Experience Platform.
1. Os dados de consentimento/preferência são assimilados em um conjunto de dados habilitado para [!DNL Profile] cujo esquema contém campos de consentimento/preferência.

Além dos comandos do SDK acionados pelos ganchos de alteração de consentimento do CMP, os dados de consentimento também podem fluir para o Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que são carregados diretamente para um conjunto de dados habilitado para [!DNL Profile].

### Execução de consentimento

Na versão atual do suporte ao processamento de consentimento no Experience Platform, somente a permissão de coleta de dados (`collect.val`) é imposta automaticamente pelo Experience Platform Web SDK. Embora seja possível coletar e manter consentimentos e preferências mais granulares nos perfis do cliente, esses sinais adicionais devem ser aplicados manualmente em seus próprios processos de downstream.

>[!NOTE]
>
>Para obter mais informações sobre a estrutura dos campos de consentimento XDM mencionados acima, consulte o manual no [[!UICONTROL Consents and Preferences] tipo de dados](/help/xdm/data-types/consents.md).

Depois que o sistema é configurado, o Experience Platform Web SDK interpreta o valor de consentimento da coleta de dados para o usuário atual a fim de determinar se os dados devem ser enviados para o Adobe Experience Platform Edge Network, descartados do cliente ou mantidos até que a permissão de coleta de dados seja definida como sim ou não.

## Determine como gerar dados de consentimento do cliente na CMP {#consent-data}

Como cada sistema CMP é exclusivo, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento enquanto interagem com seu serviço. Uma maneira comum de fazer isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao seguinte exemplo:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Essa caixa de diálogo deve permitir que o cliente aceite ou não casos de uso específicos de marketing e personalização para seus dados. Esses consentimentos e preferências devem estar em conformidade com o modelo de dados definido para o conjunto de dados habilitado para [!DNL Profile] na próxima etapa.

## Adicionar campos de consentimento padronizados a um conjunto de dados habilitado para [!DNL Profile] {#dataset}

Os dados de consentimento do cliente devem ser enviados para um conjunto de dados habilitado para [!DNL Profile] cujo esquema contém campos de consentimento. Esses campos devem ser incluídos no mesmo esquema e conjunto de dados que você usa para capturar informações de atributos sobre clientes individuais.

Consulte o tutorial sobre [configuração de um conjunto de dados para captura de dados de consentimento](./dataset.md) para obter etapas detalhadas sobre como adicionar esses campos obrigatórios a um conjunto de dados habilitado para [!DNL Profile] antes de continuar com este guia.

## Atualizar as políticas de mesclagem [!DNL Profile] para incluir dados de consentimento {#merge-policies}

Depois de criar um conjunto de dados habilitado para [!DNL Profile] para processar dados de consentimento, você deve garantir que suas políticas de mesclagem tenham sido configuradas para sempre incluir campos de consentimento em cada perfil de cliente. Isso envolve definir a precedência do conjunto de dados para que ele seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

>[!NOTE]
>
>Se não tiver conjuntos de dados conflitantes, defina a precedência do carimbo de data e hora para sua política de mesclagem. Isso ajuda a garantir que o consentimento mais recente especificado por um cliente seja a configuração de consentimento usada.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, comece lendo a [visão geral das políticas de mesclagem](../../../../profile/merge-policies/overview.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus perfis incluam todos os atributos de consentimento necessários fornecidos pelo grupo de campos de esquema [!UICONTROL Consents and Preferences], conforme descrito no guia em [preparação do conjunto de dados](./dataset.md).

## Enviar dados de consentimento para o Experience Platform

Depois de ter seus conjuntos de dados e políticas de mesclagem para representar os campos de consentimento necessários nos perfis do cliente, a próxima etapa é trazer os dados de consentimento em si para a Experience Platform.

Basicamente, você deve usar o Adobe Experience Platform Web SDK para enviar dados de consentimento à Experience Platform sempre que eventos de alteração de consentimento forem detectados pelo CMP. Se estiver coletando dados de consentimento em uma plataforma móvel, você deve usar o Adobe Experience Platform Mobile SDK. Você também pode optar por assimilar seus dados de consentimento coletados diretamente mapeando-os para o esquema XDM do conjunto de dados de consentimento e enviando-os para a Experience Platform por meio da assimilação em lote.

Os detalhes de cada um desses métodos são fornecidos nas subseções abaixo.

### Configurar o Experience Platform Web SDK para processar dados de consentimento {#web-sdk}

Depois de configurar o CMP para acompanhar eventos de alteração de consentimento em seu site, você pode integrar o Experience Platform Web SDK para receber as configurações de consentimento atualizadas e enviá-las para a Experience Platform em cada carregamento de página e sempre que eventos de alteração de consentimento ocorrerem. Consulte o manual sobre [configuração do Web SDK para processar dados de consentimento do cliente](../sdk.md) para obter mais informações.

### Configurar o Experience Platform Mobile SDK para processar dados de consentimento {#mobile-sdk}

Se as preferências de consentimento do cliente forem necessárias no aplicativo móvel, você poderá integrar o Experience Platform Mobile SDK para recuperar e atualizar as configurações de consentimento, enviando-as para a Experience Platform sempre que a API de consentimento for chamada.

Consulte a documentação do Mobile SDK para [configurar a extensão para dispositivos móveis de consentimento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) e [usar a API de consentimento](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Para obter mais detalhes sobre como lidar com questões de privacidade usando o Mobile SDK, consulte a seção [Privacidade e GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Assimilar dados de consentimento compatíveis com XDM diretamente {#batch}

Você pode assimilar dados de consentimento compatíveis com XDM de um arquivo CSV usando a assimilação em lote. Isso pode ser útil se você tiver um backlog de dados de consentimento coletados anteriormente que ainda não foram integrados aos perfis do cliente.

Siga o tutorial em [mapeamento de um arquivo CSV para XDM](../../../../ingestion/tutorials/map-csv/overview.md) para saber como converter seus campos de dados para XDM e assimilá-los no Experience Platform. Ao selecionar o [!UICONTROL Destination] para o mapeamento, certifique-se de selecionar a opção **[!UICONTROL Use existing dataset]** e escolher o conjunto de dados de consentimento habilitado para [!DNL Profile] que você criou anteriormente.

## Testar sua implementação {#test-implementation}

Depois de assimilar os dados de consentimento do cliente no conjunto de dados habilitado para [!DNL Profile], você pode verificar os perfis atualizados para ver se eles contêm atributos de consentimento.

>[!IMPORTANT]
>
>Para exibir os atributos de um perfil existente na interface do usuário do, você deve saber pelo menos um valor de identidade (e seu namespace correspondente) associado a esse perfil.
>
>Se não tiver acesso a essas informações, você poderá optar por assimilar seus próprios dados de consentimento de teste e associá-los a um valor/namespace de identidade conhecido por você.

Consulte a seção sobre [perfis de navegação por identidade](../../../../profile/ui/user-guide.md#browse) no guia da interface do usuário [!DNL Profile] para obter etapas específicas sobre como pesquisar os detalhes de um perfil.

Por padrão, os novos atributos de consentimento não aparecerão no painel de um perfil. Portanto, você deve navegar até a guia **[!UICONTROL Attributes]** na página de detalhes de um perfil para confirmar que eles foram assimilados conforme esperado. Consulte o guia no [painel de perfil](../../../../profile/ui/profile-dashboard.md) para saber como personalizar o painel de acordo com suas necessidades.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Experience Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Experience Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Experience Platform and the appropriate profile attributes are updated accordingly.
-->

## Próximas etapas

Este guia aborda como configurar as operações do Experience Platform para processar dados de consentimento do cliente usando o padrão Adobe e ter esses atributos representados em perfis do cliente. Agora é possível integrar as preferências de consentimento do cliente como um fator determinante na qualificação do segmento e em outros casos de uso de downstream.

Para obter mais informações sobre os recursos relacionados à privacidade do Experience Platform, consulte a visão geral sobre [governança, privacidade e segurança no Experience Platform](../../overview.md).
