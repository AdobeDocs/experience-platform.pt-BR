---
title: Conexão Adobe Campaign Managed Cloud Services
description: O Adobe Campaign Managed Cloud Services fornece uma plataforma para projetar experiências de clientes entre canais e um ambiente para a orquestração visual de campanhas, o gerenciamento de interação em tempo real e a execução entre canais.
source-git-commit: 81c17a6ea07efbbea91e0d918d52ec96e0335152
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 4%

---

# Conexão Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Essa integração funciona com [Adobe Campaign versão 8.4 ou superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1).

## Visão geral {#overview}

O Adobe Campaign Managed Cloud Services fornece uma plataforma para projetar experiências de clientes entre canais e um ambiente para a orquestração visual de campanhas, o gerenciamento de interação em tempo real e a execução entre canais. [Introdução ao Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Use o Campaign para:
* Impulsionar a personalização e o envolvimento por meio de uma única visualização acessível do cliente,
* Integrar canais de email, móveis, online e offline à jornada do cliente,
* Automatizar a entrega de mensagens e ofertas relevantes e oportunas.

>[!IMPORTANT]
>
>Lembre-se das seguintes medidas de proteção ao usar a conexão Adobe Campaign Managed Cloud Services:
>
>* No máximo 50 segmentos podem ser [ativado](#activate) para o destino,
>* Para cada segmento, você pode adicionar até 20 campos para [mapa](#map) para a Adobe Campaign,
>* Retenção de dados na DLZ (Data Landing Zone) de armazenamento do Azure Blob : 7 dias,
>* A frequência de ativação é de 3 horas no mínimo.


## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do Adobe Campaign Manage Service, esta é uma amostra de caso de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

O Adobe Experience Platform cria um perfil de cliente que incorpora informações como o gráfico de identidade, dados comportamentais de análises, mescla dados offline e online etc. Com essa integração, você pode aumentar os recursos de segmentação que já existem no Adobe Campaign com esses públicos-alvo alimentados pela Adobe Experience Platform e, portanto, ativar esses dados no Campaign.

Por exemplo, uma empresa de roupas esportivas deseja aproveitar os segmentos inteligentes alimentados pela Adobe Experience Platform e ativá-los usando o Adobe Campaign para alcançar a base do cliente nos diferentes canais compatíveis com a Adobe Campaign.

Depois que as mensagens são enviadas, elas desejam aprimorar o perfil do cliente na Adobe Experience Platform com dados de experiência do Adobe Campaign, como envios, aberturas e cliques.

O resultado são campanhas em vários canais que são mais consistentes no ecossistema da Adobe Experience Cloud e um perfil de cliente avançado que está se adaptando e aprendendo rapidamente.

[Saiba mais sobre a integração do Adobe Campaign com o Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)


## Pré-requisitos {#prerequisites}

Para que o Campaign possa recuperar dados do Adobe Experience Platform, é necessário criar um projeto de API do Campaign e solicitar ao Atendimento ao cliente que adicione a ID do cliente associada a uma lista de permissões.

>[!NOTE]
>
>As informações globais sobre como criar um projeto de API estão detalhadas em [esta documentação](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman.html)

1. Faça logon em [Console do Adobe Developer](https://console.adobe.io/) e criar um novo projeto.

1. Selecionar **[!UICONTROL Adicionar API]** e escolha **[!UICONTROL Adobe Campaign]**.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/create-api.png)

1. Gere um par de chaves.

1. Selecione o `<Instance Name> - admin` perfil de produto e selecione **[!UICONTROL Salvar API configurada]**.

1. Seu projeto de API é criado. Anote o **[!UICONTROL ID do cliente]** exibido no seu projeto. Entre em contato com o Atendimento ao cliente do Adobe e solicite que ele adicione sua ID do cliente a uma lista de permissões.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/client-id.png)

## Identidades suportadas {#supported-identities}

*Adobe Campaign Managed Cloud Services* O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| external_id | IDs de usuário personalizadas | Selecione essa identidade de destino quando sua identidade de origem for um namespace personalizado. Recomendamos usar essa identidade e mapeá-la para a ID na instância do Campaign que representa o cliente (loyalty_ID, account_ID, customer_ID...) |
| ECID | Experience Cloud ID | Um namespace que representa ECID. Esse namespace também pode ser mencionado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento em [ECID](/help/identity-service/ecid.md) para obter mais informações. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte para texto sem formatação e números de telefone com hash SHA256. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. |
| GAID | Google Advertising ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando sua identidade de origem for um namespace do IDFA. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Selecionar instância]**: Seu **[!DNL Campaign]** instância de marketing.
* **[!UICONTROL Target mapping]**: Selecione o target mapping que você está usando no **[!DNL Adobe Campaign]** para enviar deliveries. [Saiba mais](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

### Política de governança e ações de aplicação {#governance}

Selecione as ações de marketing aplicáveis aos dados que você deseja exportar para o destino. No Adobe Campaign, recomendamos que você selecione a variável **[!UICONTROL Direcionamento de email]** ação de marketing.

Para obter mais informações sobre ações de marketing, consulte o [visão geral das políticas de uso de dados](/help/data-governance/policies/overview.md) página.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar dados do público-alvo para destinos de exportação de perfil em lote](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) para obter instruções sobre como ativar os dados do público-alvo para esse destino.

### Mapear atributos e identidades {#map}

Selecione campos XDM para exportar com os perfis e mapeá-los para os campos Adobe Campaign correspondentes.[Saiba mais sobre a seleção de identidade e atributos para destinos de marketing por email](overview.md)

1. Selecionar campos de origem:

   * Selecione um **identifier** (Por exemplo: o campo email) como identidade de origem que identifica exclusivamente um perfil no Adobe Experience Platform e Adobe Campaign.

   * Selecionar todos os outros **Atributos de perfil de origem XDM** que precisam ser exportadas para o Adobe Campaign.
   >[!NOTE]
   >
   >O campo &quot;segmentMembershipStatus&quot; é um mapeamento necessário para refletir o status de segmentMembership. Este campo é adicionado por padrão e não pode ser modificado ou removido.

1. Mapeie cada campo com seu campo de destino no Adobe Campaign. Os campos de destino disponíveis são determinados pelo target mapping selecionado quando [criação do destino](#destination-details).

1. Identificar atributos obrigatórios e chaves de desduplicação. Observe que os valores nos atributos marcados como &quot;Obrigatório&quot; ou &quot;Chave de desduplicação&quot; não podem ser nulos.

   * [Atributos obrigatórios](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) verifique se todos os registros de perfil contêm os atributos selecionados. Por exemplo: todos os perfis exportados contêm um endereço de email. A recomendação é definir como obrigatório o campo de identidade e o campo usado como chave de desduplicação.
   * [Uma chave de desduplicação](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) é uma chave primária que determina a identidade pela qual os usuários desejam que seus perfis sejam desduplicados.

      >[!IMPORTANT]
      >
      >Certifique-se de que o nome do atributo da chave de desduplicação corresponda ao nome da coluna do target mapping selecionado.
   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Depois que o mapeamento for executado, você poderá revisar e concluir a configuração de destino para começar a enviar dados para o **[!DNL Campaign]**.
   [Saiba como revisar e concluir a configuração de destino](/help/destinations/destination-types.md#review).

## Dados exportados / Validar exportação de dados {#exported-data}

Depois que um destino é ativado, você pode acessar o trabalho correspondente e os dados exportados no Campaign.

### Monitorar trabalhos de exportação de dados {#jobs}

Navegue até o **[!UICONTROL Administração]** > **[!UICONTROL Auditoria]** > **[!UICONTROL Tarefas de carregamento do público-alvo]** para monitorar todos os trabalhos de exportação ativados do Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Acessar dados exportados {#data}

Navegue até o **[!UICONTROL Perfil e direcionamento]** > **[!UICONTROL Lista]** > **[!UICONTROL Públicos-alvo da AEP]** para acessar públicos-alvo criados após ativar um destino.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](/help/data-governance/home.md).
