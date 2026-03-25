---
title: Notas da versão de março de 2026 da Adobe Experience Platform
description: As notas da versão de março de 2026 da Adobe Experience Platform.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 30b66420e9cee6b4d85cf41a31e9595d5a240fda
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 18%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/latest)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/pt-br/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: quarta-feira, 24 de março de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Gerenciamento avançado do ciclo de vida de dados](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Datastreams](#datastreams)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#real-time-customer-profile)
- [Serviço de segmentação](#segmentation-service)
- [Fontes](#sources)

## Gerenciamento avançado do ciclo de vida de dados {#advanced-data-lifecycle-management}

O Experience Platform fornece um conjunto de recursos de higiene de dados que permitem gerenciar os dados armazenados por meio de exclusões programáticas de registros e conjuntos de dados do consumidor. Usando o espaço de trabalho Ciclo de vida dos dados na interface ou as chamadas para a API de higiene de dados, você pode gerenciar com eficiência seus armazenamentos de dados. Use esses recursos para garantir que as informações sejam usadas conforme esperado, sejam atualizadas quando dados incorretos precisarem de correção e sejam excluídas quando as políticas organizacionais considerarem necessário.

| Recurso | Descrição |
| --- | --- |
| Exclusão de registro de vários conjuntos de dados e somente perfil (somente API) | Você pode enviar uma única ID de conjunto de dados, uma lista separada por vírgulas de IDs de conjunto de dados ou o literal `ALL` em `datasetId` para excluir identidades em um, em vários ou em todos os conjuntos de dados. Você também pode limitar a exclusão a serviços relacionados ao perfil definindo `targetServices` como `["identity","profile","ajo"]`, o que deixa o datalake inalterado; essa funcionalidade está disponível somente por meio da API da Higiene de Dados. Consulte o [Guia de exclusão de ordens de serviço de registro](../../hygiene/api/workorder.md) para obter mais detalhes. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral avançada do gerenciamento do ciclo de vida dos dados](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

O Agent Orchestrator permite criar e implantar agentes alimentados por IA que podem automatizar fluxos de trabalho e interagir com clientes em vários canais.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| [Adobe Marketing Agent para [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | O Adobe Marketing Agent para [!DNL Microsoft 365 Copilot] é seu agente incorporado que traz a inteligência de marketing da Adobe diretamente para as ferramentas do dia a dia, como [!DNL Teams], [!DNL Word], [!DNL PowerPoint] e outros aplicativos do [!DNL Microsoft 365]. Você pode usar esse agente para obter insights de campanha confiáveis dos aplicativos da Adobe enquanto planeja campanhas, revisa públicos, colabora com colegas para responder às perguntas dos clientes e tomar decisões informadas por dados sem sair do fluxo de trabalho do [!DNL Microsoft 365]. |

{style="table-layout:auto"}

Para obter mais informações, leia a [documentação do Agent Orchestrator](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Datastreams {#datastreams}

Uma sequência de dados representa a configuração do lado do servidor ao implementar os SDKs da Web e móvel da Adobe Experience Platform e a API do servidor do Adobe Experience Platform Edge Network. O comando de configuração do fluxo de dados nos SDKs lida com todos os serviços com os quais um cliente interage.

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral das configurações de fluxo de dados dinâmico | As configurações dinâmicas de sequência de dados agora estão disponíveis no geral. As configurações dinâmicas da sequência de dados permitem definir conjuntos de regras configuráveis pelo usuário para cada serviço ativado para a sequência de dados, que determinam qual solução da Experience Cloud deve receber cada tipo de dados. Consulte o [guia de configurações da sequência de dados dinâmica](../../datastreams/configure-dynamic-datastream.md) para obter mais informações. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral dos fluxos de dados](../../datastreams/overview.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| Conexão [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | A nova conexão do Adobe Advertising DSP oferece a mesma funcionalidade da conexão herdada, além de suporte para identidades adicionais. Com o novo conector, você também pode exportar identidades baseadas em cookies para o Adobe Advertising DSP. |
| Conexão [FreeWheel](../../destinations/catalog/advertising/freewheel.md) | Envie [!DNL Real-Time CDP] públicos-alvo para o FreeWheel como arquivos em lotes diários, para que você possa direcioná-los em ofertas e campanhas do FreeWheel na CTV, vídeo e exibição. Entre em contato com a equipe de conta da Adobe para obter acesso. |
| Suporte a público-alvo externo para [o Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) e [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Agora é possível ativar públicos-alvo de origens além do Serviço de segmentação para o Trade Desk CRM, Critério e Pinterest, incluindo públicos-alvo de upload personalizados (importados do CSV), públicos-alvo semelhantes, públicos-alvo federados e públicos-alvo criados em outros aplicativos da Experience Platform, como o [!DNL Adobe Journey Optimizer]. Esta atualização está sendo lançada até o final de março. Consulte a seção [públicos-alvo suportados](../../destinations/catalog/advertising/criteo.md#supported-audiences) na página do catálogo de cada destino para obter detalhes. |
| Limite aumentado para públicos-alvo de upload personalizados | Agora você pode ativar até 20 públicos-alvo de upload personalizados por instância de destino. Anteriormente, esse limite era de 10. Consulte as [medidas de proteção de destinos](../../destinations/guardrails.md#batch-file-based-activation) para obter detalhes. |
| [Exportar arquivo agora](../../destinations/ui/export-file-now.md) e [suporte à API de ativação ad hoc](../../destinations/api/ad-hoc-activation-api.md) para públicos externos | Agora você pode usar o Export file now (UI) e a API de ativação ad-hoc com públicos externos (como upload personalizado, semelhante, federado e públicos de outros aplicativos da Experience Platform) ao ativar para destinos baseados em arquivo em lote. Esta atualização está sendo lançada até o final de março. |

{style="table-layout:auto"}

**Correções e melhorias**

| Correção | Descrição |
| --- | --- |
| hash do número de telefone do conector [TikTok](../../destinations/catalog/social/tiktok.md) | Correção de um problema em que uma configuração incorreta no cartão de destino significava que as identidades destacadas de números de telefone não eram ativadas para o TikTok. Para se beneficiar dessa correção, configure um novo fluxo de ativação ou remova o mapeamento do número de telefone do fluxo existente, salve-o e adicione-o novamente. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Ações de entidade XDM e suporte à exclusão | Acesse ações para esquemas, classes, grupos de campos e tipos de dados diretamente dos menus de tabela em linha e dos menus de cabeçalho de página de detalhes. Se você tiver as permissões necessárias, também poderá excluir as entidades da sua organização quando elas não forem usadas por conjuntos de dados e não estiverem habilitadas para Perfil. Consulte o [Guia da interface do usuário XDM](../../xdm/ui/explore.md) para obter mais detalhes. |

Para obter mais informações, leia a [visão geral do XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#real-time-customer-profile}

O Perfil do cliente em tempo real permite ter uma visão holística de cada cliente individual ao combinar dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Eventos | Agora é possível definir o período de pesquisa de eventos ao navegar pelos perfis. Isso permite que você veja os eventos aos quais o perfil está associado pelo período especificado. Para obter mais informações, leia o [Guia da Interface do Usuário do Perfil](/help/profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Para obter mais informações, leia a visão geral[&#128279;](../../profile/home.md) do [!DNL Real-Time Customer Profile] .

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os públicos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Tipo de assimilação | Agora é possível visualizar o tipo de assimilação dos atributos. Isso permite que você saiba a origem dos seus dados, permitindo criar públicos-alvo melhores. Para obter mais informações sobre esse recurso, leia o [Guia do Construtor de segmentos](/help/segmentation/ui/segment-builder.md). |
| Dados de resumo | Agora você pode exibir os dados de resumo dos seus atributos para públicos-alvo com base em conta e pessoas. Para obter mais informações sobre este recurso nos públicos-alvo da conta, leia o [guia do Construtor de público-alvo](/help/rtcdp/segmentation/audience-builder.md). Para obter mais informações sobre este recurso em públicos com base em pessoas, leia o [Guia do Construtor de segmentos](/help/segmentation/ui/segment-builder.md). |

Para obter mais informações, leia a visão geral[&#128279;](../../segmentation/home.md) do [!DNL Segmentation Service] .

## Fontes

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| [!DNL Talon.One] | Agora você pode conectar o Experience Platform ao [!DNL Talon.One] usando as novas fontes de [!DNL Talon.One] [lote](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) e [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md). Use as novas fontes para assimilar dados do perfil de fidelidade, bem como eventos de transação e atividade de fidelidade para a Experience Platform. |
| Novos endereços IP para incluir na lista de permissões | Novos endereços IP para GBR9: Reino Unido foram adicionados à lista de endereços que você deve incluir na lista de permissões para garantir conexões de origem em lote bem-sucedidas com o Experience Platform no Azure. Exiba a lista no [guia de incluo na lista de permissões de endereços IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) para obter mais informações. |
| Suporte aprimorado para a captura de dados do Change | Agora você pode usar o Change Data Capture com as fontes [!DNL Marketo Engage], [!DNL Microsoft Dynamics] e [!DNL Salesforce CRM]. |
| Guia de autenticação aprimorado para [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | O guia de autenticação para a origem [!DNL Google BigQuery] foi expandido com as seguintes informações: <ul><li>Os escopos necessários para o token de atualização.</li><li>As funções IAM necessárias para a identidade [!DNL Google].</li><li>Orientação adicional sobre o uso de `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->
