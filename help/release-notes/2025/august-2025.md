---
title: Notas de versão de agosto de 2025 da Adobe Experience Platform
description: As notas de versão de agosto de 2025 da Adobe Experience Platform.
exl-id: d93e98f3-d165-4710-ad1d-2ad3857cd0f8
source-git-commit: 6b3b830f822cc02c78d6f593c0a949d3e19ada37
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 20%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-no)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: quarta-feira, 19 de agosto de 2025**


Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Alertas](#alerts)
- [Serviço de catálogo](#catalog-service)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation-service)
- [Origens](#sources)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades do Experience Platform. Você pode assinar diferentes regras de alerta por meio da guia [!UICONTROL Alertas] na interface do usuário do Experience Platform e pode optar por receber mensagens de alerta na própria interface ou por meio de notificações por email.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Alertas de capacidade de taxa de transferência de transmissão | Três novos alertas permitem que os usuários assinem e configurem alertas para gerenciar e monitorar proativamente o desempenho da capacidade de taxa de transferência de transmissão. Os novos alertas incluem quando a taxa de transferência de transmissão atinge 80%, 90% ou excede os limites de capacidade. Para obter mais informações, leia o [guia de regras de alerta de capacidade](../../observability/alerts/rules.md#capacity). |

Para obter mais informações sobre alertas, leia a [[!DNL Observability Insights] visão geral](../../observability/home.md).

## Serviço de catálogo {#catalog-service}

O Serviço de catálogo é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. Embora todos os dados assimilados na Experience Platform sejam armazenados no data lake como arquivos e diretórios, o Catálogo retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Retenção de dados para o perfil do cliente em tempo real | Você pode **atualizar** somente o período de retenção de dados do Perfil de cliente em tempo real uma vez a cada 30 dias. |

Para obter mais informações sobre o Serviço de Catálogo, leia a [visão geral do Serviço de Catálogo](../../catalog/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

>[!IMPORTANT]
>
>**Extensão de agendamento de exportação do conjunto de dados**
>
>Se sua organização tiver fluxos de dados de exportação do conjunto de dados criados antes de novembro de 2024, esses fluxos de dados deixarão de funcionar em **1º de setembro de 2025**. Se precisar que os fluxos de dados continuem exportando dados após 1º de setembro de 2025, estenda suas agendas para cada destino para o qual você está exportando conjuntos de dados seguindo as etapas no [este guia](../../destinations/ui/dataset-expiration-update.md).

>[!IMPORTANT]
>
>**Atualização de inclui na lista de permissões com base em IP necessária para destinos com API**
>
>Devido a atualizações no mecanismo de exportação de destinos de transmissão, as organizações que usam as [listas de permissões de IP](../../destinations/catalog/streaming/ip-address-allow-list.md) para destinos baseados em API devem adicionar os seguintes endereços IP às suas listas de permissões **antes de 15 de setembro de 2025**:
>
>**Endereços IP necessários:**
>
>```
>3.209.222.108
>3.211.230.204
>35.169.227.49
>66.117.18.133
>66.117.18.134
>66.117.18.135
>```
>
>**Esta alteração se aplica aos seguintes tipos de destino:**
>
>- [Destinos de exportação de público-alvo de streaming](../../destinations/destination-types.md#streaming-destinations) ([Público-alvo em tempo real do Pega CDH](/help/destinations/catalog/personalization/pega-v2.md), integrações baseadas em API com o [Salesforce Marketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) e o [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md))
>- Destinos públicos ou privados compilados através de [Destination SDK](../../destinations/destination-sdk/getting-started.md)
>
>**Ação necessária:** se você trabalhou com a Adobe para modificar qualquer endereço IP para destinos de transmissão baseados em API, é necessário adicionar os endereços IP acima ao seu arquivo de incluir na lista de permissões inclui na lista de permissões para garantir fluxos de dados ininterruptos para seus destinos baseados em API.

**Novos destinos**

| Destino | Descrição |
| --- | --- |
| [[!DNL Acxiom Real ID Audience Connection]](../../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) destino | Use o destino [!DNL Acxiom Real ID Audience Connection] para aprimorar públicos com a tecnologia [!DNL Acxiom's] [Real ID](https://www.acxiom.com/real-id/real-id/) e ativar públicos para várias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] e muito mais. |

**Destinos atualizados**

| Destino | Descrição |
| --- | --- |
| Atualização interna de [[!DNL Microsoft Bing]](../../destinations/catalog/advertising/bing.md) | A partir de 11 de agosto de 2025, por um curto período, você pode ter visto dois cartões **[!DNL Microsoft Bing]** lado a lado no catálogo de destinos. Isso se deve a uma atualização interna do serviço de destinos. O conector de destino **[!DNL Microsoft Bing]** existente foi renomeado para **[!UICONTROL (obsoleto) Microsoft Bing]** e um novo cartão com o nome **[!UICONTROL Microsoft Bing]** está disponível para você. <br> A atualização foi concluída e o cartão obsoleto foi removido do catálogo de destino. Use a conexão **[!UICONTROL Microsoft Bing]** no catálogo para novos fluxos de dados de ativação. Se você tiver fluxos de dados ativos para o destino **[!UICONTROL (obsoleto) do Microsoft Bing]**, eles serão atualizados automaticamente, portanto, nenhuma ação é necessária. <br><br>Se você estiver criando fluxos de dados por meio da [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/), atualize o [!DNL flow spec ID] e o [!DNL connection spec ID] para os seguintes valores:<ul><li>ID da especificação de fluxo: `8d42c81d-9ba7-4534-9bf6-cf7c64fbd12e`</li><li>ID de especificação da conexão: `dd69fc59-3bc5-451e-8ec2-1e74a670afd4`</li></ul> Após esta atualização, você pode enfrentar uma **queda no número de perfis ativados** em seus fluxos de dados para [!DNL Microsoft Bing]. Esta queda é causada pela introdução do **requisito de mapeamento ECID** para todas as ativações nesta plataforma de destino. |
| Detalhes de expiração da autenticação para destinos [[!DNL LinkedIn]](../../destinations/catalog/social/linkedin.md) e [LinkedIn Matched Audiences](../../destinations/catalog/social/linkedin-b2b.md) | As informações de expiração da autenticação para destinos [!DNL LinkedIn] agora estão visíveis diretamente na interface do Experience Platform, para que você possa ver quando sua autenticação expirará e a renovará antes de causar interrupções em seus fluxos de dados. É possível monitorar as datas de expiração do token a partir da coluna **[!UICONTROL Data de expiração da conta]** nas guias **[[!UICONTROL Contas]](../../destinations/ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Procurar]](../../destinations/ui/destinations-workspace.md#browse)**. |
| [Públicos-alvo correspondentes do LinkedIn](../../destinations/catalog/social/linkedin-b2b.md) [!DNL IDFA] remoção do suporte à identidade | A partir de setembro de 2025, não será mais possível mapear [!DNL IDFA] como identidade de destino, pois [!DNL IDFA] não é mais suportado pelo destino [!DNL LinkedIn Matched Audiences]. Consulte a [!DNL LinkedIn Matched Audiences]documentação[ da integração de ](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes) para obter mais detalhes. Essa alteração se deve aos requisitos do LinkedIn e não está relacionada a nenhuma atualização de serviço de destino do Experience Platform. |

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Recursos aprimorados de pesquisa, filtragem e marcação para destinos | Melhore seu fluxo de trabalho de gerenciamento de destino com recursos aprimorados de pesquisa, filtragem e marcação nas guias [Procurar](../../destinations/ui/destinations-workspace.md#browse) e [Contas](../../destinations/ui/destinations-workspace.md#accounts). <br> Agora você pode pesquisar fluxos de dados e contas específicos por nome, filtrar por vários critérios, incluindo plataforma de destino, status e datas, e criar marcas personalizadas para organizar seus destinos. A classificação de colunas também está disponível para campos principais, como último tempo de execução do fluxo de dados, facilitando a identificação e o gerenciamento das conexões de destino. <br> ![Demonstração animada de pesquisa de um fluxo de dados de destino na guia Procurar](../../destinations/assets/ui/workspace/search.gif) |

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Esquemas Baseados Em Modelo | Simplifique a modelagem de dados com esquemas baseados em modelo. Agora é possível criar esquemas mais facilmente com exemplos e orientação abrangentes. Esse recurso está disponível no momento para os titulares de licença do Campaign Orchestration e será expandido para os clientes do Data Distiller em GA, tornando a modelagem de dados mais acessível e eficiente. |

Para obter mais informações, leia a [visão geral do XDM](../../xdm/home.md).

<!--
## Real-Time Customer Profile {#profile}

Real-Time Customer Profile provides a unified, actionable view of each customer by consolidating data from all channels into a single profile.

**New or updated features**

| Feature | Description |
| --- | --- |
| Enhanced lookup functionality in the Entities API | The Entities API now supports the following: <ul><li>Person (Profile)</li><li>Experience Events</li><li>Account</li><li>Opportunity</li></ul> This update simplifies API usage and helps ensure optimal performance and reliability. If you previously used lookups for other entity types—including join tables and custom Multi-Entity types—now is a great opportunity to review your API usage and take advantage of the improved experience. For more information, read the [Real-Time CDB B2B Edition architecture upgrade guide](../../rtcdp/b2b-architecture-upgrade.md). |

For more information on Real-Time Customer Profile, read the [Profile overview](../../profile/home.md).

-->

## Sandboxes {#sandboxes}

O Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Eliminação da duplicação de objetos de dependência na importação do fluxo de trabalho | Agora, as ferramentas de sandbox sempre reutilizarão objetos existentes se objetos com o mesmo nome forem detectados, para evitar a proliferação de objetos. Essa alteração se aplica aos seguintes objetos: <ul><li>Esquema</li><li>Grupo de campos</li><li>Público-alvo</li><li>`decisioning_ranking`</li><li>`decisioning_rules`</li></ul> Para obter mais informações, leia o [guia sobre objetos com suporte para ferramentas de sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Todo o suporte à sandbox para compartilhamento de pacotes entre organizações | As ferramentas de sandbox agora oferecem suporte para **todo o tipo de sandbox** no compartilhamento de pacotes da organização. Agora você pode compartilhar pacotes completos de sandbox e de vários objetos entre organizações. Para obter mais informações, leia o [guia sobre objetos com suporte para ferramentas de sandbox](../../sandboxes/ui/sharing-packages-across-orgs.md). |

Para obter mais informações sobre sandboxes, leia a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Estimativas de público | As estimativas de público-alvo agora são exibidas como um **intervalo**, que se baseia no intervalo de confiança dos dados de amostragem. Para saber mais sobre estimativas, leia o [guia do Construtor de segmentos](/help/segmentation/ui/segment-builder.md#audience-properties). |

Para obter mais informações, leia a visão geral](../../segmentation/home.md) do [[!DNL Segmentation Service] .

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Funcionalidade nova ou atualizada**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral da origem do [!DNL Oracle NetSuite]  | A origem [!DNL Oracle NetSuite] agora está disponível. Agora você pode conectar sua conta do [!DNL Oracle NetSuite] à Experience Platform para assimilar dados de atividades e entidades para análise e ativação unificadas. Para obter mais informações, leia a visão geral](../../sources/connectors/marketing-automation/oracle-netsuite.md) do [[!DNL Oracle NetSuite] . |
| Disponibilidade geral da origem do [!DNL PathFactory]  | A origem [!DNL PathFactory] agora está disponível. Você pode conectar sua conta do [!DNL PathFactory] à Experience Platform para assimilar dados de visitantes, sessões e exibições de página para análise e ativação unificadas. Para obter mais informações, leia a visão geral](../../sources/connectors/marketing-automation/pathfactory.md) do [[!DNL PathFactory] . |
| Disponibilidade geral da origem do [!DNL Stripe]  | A origem [!DNL Stripe] agora está disponível. Você pode conectar sua conta do [!DNL Stripe] à Experience Platform para assimilar dados de pagamento e transação para análise e ativação unificadas. Para obter mais informações, leia a visão geral](../../sources/connectors/payments/stripe.md) do [[!DNL Stripe] . |
| Autenticação aprimorada para [!DNL Azure Blob Storage] | Agora você pode usar a autenticação baseada na entidade de serviço para conectar sua origem do [!DNL Azure Blob Storage] à Experience Platform. Use a autenticação baseada na entidade de serviço para segurança aprimorada, rotação de credenciais mais fácil e um controle de acesso mais granular para sua conta. Para obter mais informações, leia a visão geral](../../sources/connectors/cloud-storage/blob.md) do [[!DNL Azure Blob Storage] . |

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

<!--
| [!DNL Marketo] source documentation updates | Get complete visibility into how your [!DNL Marketo] data is transformed when it enters Experience Platform. All field mappings now include detailed explanations of data transformations, so you can understand exactly how your `PersonID` becomes `leadID` and `eventType` becomes `activityType`. |
| [!BADGE Beta]{type=Informative} Support for [!DNL Azure Private Links] in the UI | You can now use [!DNL Azure Private Links] for a select group of sources in the UI. Use this feature to create a private endpoint that which your source can connect to. With private endpoints, you can set up connections and dataflows that bypass the public internet, giving you enhanced security and network isolation for your sensitive data. Support for [!DNL Azure Private Links] is available to the following following sources: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li></ul> For more information, read the guide on [[!DNL Azure Private Links]](../../sources/tutorials/ui/private-link.md). |

| Enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination  | The enhanced [[!DNL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md) destination is an upgraded version of the existing [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector. This new connector brings profile sync capabilities in addition to the existing audience sync capabilities from the legacy connector, providing a tighter integration with [!DNL Marketo Engage]. <br> The [[!DNL (Legacy) (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md) connector will be deprecated in **March 2026**. To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](../../destinations/catalog/adobe/marketo-engage-connection.md)** destination, review the following key points and required actions: <ul><li>All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.</li><li> **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../destinations/ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.</li></ul>|
-->
