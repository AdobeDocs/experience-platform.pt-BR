---
title: Notas de versão da Adobe Experience Platform de setembro de 2022
description: As notas de versão de setembro de 2022 da Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 21%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 28 de setembro de 2022**

Novos recursos na Adobe Experience Platform:

- [Controle de acesso baseado em atributos](#abac)

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Logs de auditoria](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de identidade](#identity-service)
- [Query Service](#query-service)
- [Origens](#sources)

## Controle de acesso baseado em atributos {#abac}

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos será ativado a partir de outubro de 2022. Se você quiser ser um dos primeiros usuários, entre em contato com o representante da Adobe.

O controle de acesso baseado em atributos é um recurso do Adobe Experience Platform que oferece às marcas preocupadas com a privacidade maior flexibilidade para gerenciar o acesso do usuário. É possível atribuir objetos individuais, como campos de esquema e segmentos, a funções de usuário. Esse recurso permite conceder ou revogar o acesso a objetos individuais para usuários específicos da Experience Platform em sua organização.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários, dados pessoais confidenciais (SPD), informações de identificação pessoal (PII) e outros tipos personalizados de dados em todos os fluxos de trabalho e recursos da Experience Platform. Admins podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

| Recurso | Descrição |
| --- | --- |
| Controle de acesso baseado em atributos | O controle de acesso baseado em atributos permite rotular campos de esquema do Experience Data Model (XDM) e segmentos com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuários e funções para definir políticas de acesso que cubram campos e segmentos de esquema XDM, a fim de gerenciar melhor o acesso fornecido aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Para obter mais informações, consulte a [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). |
| Permissões | Permissões é a área do Experience Cloud em que os administradores podem definir funções de usuário e políticas de acesso para gerenciar permissões de acesso para recursos e objetos em um aplicativo de produto. Por meio das Permissões, é possível criar e gerenciar funções, atribuir as permissões de recurso desejadas para essas funções e criar políticas para aproveitar rótulos e definir quais funções de usuário têm acesso a recursos específicos do Experience Platform. As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica. Para obter mais informações, consulte o [Guia de IU de permissões](../../access-control/abac/ui/browse.md). |

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte a [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). Para obter um guia abrangente sobre o fluxo de trabalho do controle de acesso baseado em atributos, leia o [guia completo do controle de acesso baseado em atributos](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Os serviços de IA/ML permitem que analistas e profissionais de marketing aproveitem o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam modelos específicos para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento especializado em ciência de dados.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ela pode ser usada por comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
| --- | --- |
| Salvar Instância de Rascunho | Esse novo recurso permite que os analistas de marketing salvem uma configuração de modelo como uma instância de rascunho e continuem a editá-la até que seja concluída antes do treinamento e da pontuação. Os cenários em que esse recurso é útil incluem, quando um usuário tem vários campos para definir no fluxo de trabalho, mas não pode concluí-lo devido a restrições de tempo. Outro cenário é quando uma ou mais estatísticas de conjunto de dados estão sendo processadas e ainda não estão disponíveis. Leia o [guia do usuário da IA de atribuição](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) para saber mais. |
| Políticas de governança | Depois que os usuários enviam para criar uma instância por meio do workflow de configuração, o novo serviço de aplicação de política verifica se há violações de política do uso de dados e exibe os detalhes em um popover. Ele garante que as operações de dados e ações de marketing estejam em conformidade com as políticas de uso de dados configuradas no Adobe Experience Platform. |

Para obter mais informações sobre a IA de atribuição, consulte a [Visão geral da IA de atribuição](../../intelligent-services/attribution-ai/overview.md). Para obter informações sobre políticas de governança de dados, leia a [visão geral das políticas](../../data-governance/policies/overview.md).

### IA do cliente

A IA do cliente, disponível no Real-Time Customer Data Platform, é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala.

| Recurso | Descrição |
| --- | --- |
| Salvar Instância de Rascunho | Esse novo recurso permite que os analistas de marketing salvem uma configuração de modelo como uma instância de rascunho e continuem a editá-la até que seja concluída antes do treinamento e da pontuação. Os cenários em que esse recurso é útil incluem, quando um usuário tem vários campos para definir no fluxo de trabalho, mas não pode concluí-lo devido a restrições de tempo. Outro cenário é quando uma ou mais estatísticas de conjunto de dados estão sendo processadas e ainda não estão disponíveis. Leia o [Guia do usuário da IA do cliente](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) para saber mais. |
| Políticas de governança | Depois que os usuários enviam para criar uma instância por meio do workflow de configuração, o novo serviço de aplicação de política verifica se há violações de política do uso de dados e exibe os detalhes em um popover. Ele garante que as operações de dados e ações de marketing estejam em conformidade com as políticas de uso de dados configuradas no Adobe Experience Platform. |

Para obter mais informações sobre o Customer AI, leia a [Visão geral do Customer AI](../../intelligent-services/customer-ai/overview.md). Para obter informações sobre políticas de governança de dados, leia a [visão geral das políticas](../../data-governance/policies/overview.md).

## Logs de auditoria {#audit-logs}

O Experience Platform permite auditar a atividade do usuário em vários serviços e recursos. Os logs de auditoria fornecem informações sobre quem fez o quê e quando.

**Recursos atualizados**

| Recurso | Nome | Descrição |
| --- | --- | --- |
| Recursos adicionados | <ul><li>Instância do Attribution AI</li><li>Instância da IA do cliente</li><li>Sequência de dados</li></ul> | Os recursos de log de auditoria são registrados automaticamente conforme a atividade ocorre. Se o recurso estiver habilitado, não será necessário habilitar manualmente a coleção de logs. |

{style="table-layout:auto"}

Para obter mais informações sobre os diferentes tipos de evento específicos do recurso rastreados pelos logs de auditoria no Experience Platform, consulte a [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

| Recurso | Descrição |
| --- | --- |
| Rótulo em uso | Quando visualizado na biblioteca de widgets, o rótulo em uso identifica facilmente a presença de widgets existentes no painel. Isso facilita evitar a duplicação, embora ainda seja possível adicionar o mesmo widget mais de uma vez, se desejar. |
| Painéis definidos pelo usuário | Os painéis definidos pelo usuário ajudam a acelerar insights e personalizar visualizações, permitindo que você crie e gerencie painéis personalizados. Com painéis definidos pelo usuário, você pode criar, adicionar e editar widgets personalizados para visualizar as principais métricas relevantes para sua organização. Leia o [guia de recursos](../../dashboards/standard-dashboards.md) para saber mais. |
| Modelo de dados de insights da plataforma de dados do cliente | O recurso Modelo de dados de insights da Plataforma de dados do cliente (CDP) expõe os modelos de dados e o SQL que potencializa os insights para vários widgets de perfil, destino e segmentação. Você pode personalizar esses modelos de consulta SQL para criar relatórios CDP para seus casos de uso de marketing e indicadores principais de desempenho. Esses insights podem ser usados como widgets personalizados para seus painéis definidos pelo usuário. Leia o [guia de recursos do Modelo de Dados de Insights da CDP](../../dashboards/data-models/cdp-insights-data-model-b2c.md) para saber mais. |
| Widget de relatório de sobreposição de público | Este widget está disponível para os painéis [!UICONTROL Profiles] e [!UICONTROL Segments]. O relatório fornece uma lista ordenada de públicos-alvo classificados pelas porcentagens de sobreposição mais alta ou mais baixa para o segmento escolhido. No painel [!UICONTROL Profiles], você pode filtrar e exibir sua sobreposição de público-alvo pela política de mesclagem de todos os segmentos disponíveis. Os painéis de [!UICONTROL Segments] permitem filtrar a sobreposição de público por um segmento específico.<br>Use esta análise para criar segmentos novos e de alto desempenho e evitar o envio do mesmo público para destinos diferentes. O relatório também ajuda a identificar insights ocultos para melhorar a segmentação ou localizar perfis únicos a serem perseguidos. Leia os respectivos guias do widget [perfis](../../dashboards/guides/profiles.md#audience-overlap-report) e [segmentos](../../dashboards/guides/audiences.md#audience-overlap-report) para saber mais. |

Para obter mais informações sobre [!DNL Dashboards], consulte a [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Integração da navegação à esquerda na interface do usuário do Experience Platform | Todos os recursos que antes eram exclusivos da interface da Coleção de dados (incluindo tags, encaminhamento de eventos e sequências de dados) agora também estão disponíveis por meio da navegação à esquerda na Experience Platform, na categoria **[!UICONTROL Data Collection]**. Isso elimina a necessidade de alternar entre interfaces do usuário ao trabalhar com recursos de coleta de dados no Experience Platform. |
| Atribuição de usuário em tags e encaminhamento de eventos | Ao disponibilizar a lista [!UICONTROL Properties] em tags e encaminhamento de eventos, cada propriedade listada agora mostra quando foi atualizada pela última vez e qual usuário fez a atualização. |
| [[!DNL Snap Conversions API] extensão](https://exchange.adobe.com/apps/ec/108550) para encaminhamento de eventos | Agora você pode enviar dados para o [!DNL Snapchat Conversions API] usando uma extensão de [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md). Para obter mais informações sobre como autenticar e usar a API, consulte a [[!DNL Snapchat Marketing API] documentação](https://marketingapi.snapchat.com/docs/conversion.html). |
| [Dicas do Cliente de Usuário-Agente no Web SDK](/help/collection/use-cases/client-hints.md) | O Web SDK agora oferece suporte a [User-Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). As dicas do cliente permitem que os proprietários de sites acessem muitas das informações disponíveis na cadeia de caracteres [!DNL User-Agent], mas com mais privacidade. |
| Migração página por página do Web SDK | Agora você pode migrar suas propriedades da Web existentes de outras bibliotecas da Experience Cloud, como o [!DNL at.js], para a Web SDK, uma página por vez. Isso permite uma abordagem em fases para a migração do Web SDK, sem a necessidade de migrar todas as suas páginas de uma só vez. |
| [[!DNL Adobe Journey Optimizer] suporte para sequências de dados](../../datastreams/overview.md#aep) | O serviço Adobe Experience Platform para sequências de dados agora dá suporte a [!DNL Adobe Journey Optimizer]. Esta opção permite usar canais de entrada baseados na Web e em aplicativos no [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

Para obter mais informações sobre a coleta de dados no Experience Platform, consulte a [visão geral da coleta de dados](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Destination SDK | A Destination SDK agora oferece suporte total para parceiros e clientes que criam destinos produzidos em lote (ou baseados em arquivo) ou privados. Leia as seguintes páginas de documentação para obter mais informações: <ul><li>[Visão geral do Destination SDK](../../destinations/destination-sdk/overview.md)</li><li>[Configurar um destino baseado em arquivo](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[Configurar opções de formatação de arquivo para destinos baseados em arquivo](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[Testar seus destinos baseados em arquivo](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Destinos novos ou atualizados**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | O Adobe Campaign Managed Cloud Services fornece uma plataforma para projetar experiências de clientes entre canais, além de um ambiente para a orquestração visual de campanhas, o gerenciamento de interação em tempo real e a execução entre canais. [Introdução ao Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Observe que esta integração funciona com o [Adobe Campaign versão 8.4 ou superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | O destino [!DNL Salesforce CRM] foi atualizado para oferecer suporte a atualizações de contatos e clientes potenciais, bem como melhorias de desempenho para atualizações mais rápidas. |

{style="table-layout:auto"}

**Documentação nova ou atualizada**

| Documentação | Descrição |
| ----------- | ----------- |
| Documentação da API do serviço de fluxo de destinos | A [documentação de referência da API de Destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/) foi atualizada para incluir orientações sobre como executar operações em destinos baseados em arquivo. As operações para destinos de transmissão serão adicionadas posteriormente. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte à interface do usuário para enumerações e valores sugeridos | Além das enumerações que permitem a validação de dados, agora você pode [adicionar ou remover valores sugeridos](../../xdm/ui/fields/enum.md) para campos de sequência de caracteres padrão ou personalizados, de modo que os usuários do Experience Platform tenham uma lista amigável dos valores a serem selecionados ao criar segmentos. |

**Novos componentes do XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Propriedades de um elemento específico com o qual interagiu que causou o acionamento do evento de apresentação. |
| Grupo de campos | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Rastreia interações de mídia ao longo do tempo. |
| Grupo de campos | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Rastreia informações detalhadas da mídia. |
| Grupo de campos | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Descreve as superfícies de Eventos de experiência no Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Valores adicionados para `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valores removidos para `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Grupo de campos | (Vários) | [Foram atualizadas várias descrições de campo](https://github.com/adobe/xdm/pull/1628/files) entre componentes do Journey Orchestration. |
| Grupo de campos | (Vários) | [Os títulos de vários componentes do Adobe Workfront foram atualizados](https://github.com/adobe/xdm/pull/1634/files) para fins de consistência. |
| Grupo de campos | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Atualização dos namespaces de vários campos para `xdm`. |
| Grupo de campos | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Adição de um novo campo, `isReadSegmentTriggerStartEvent`. |
| Grupo de campos | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | O campo `xdm:uvIndex` foi alterado para um tipo inteiro e o namespace `xdm` foi adicionado a vários campos nos quais estava ausente. |
| Grupo de campos | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` e `xdm:implementationDetails` foram removidos do grupo de campos. |
| Tipo de dados | (Vários) | [Foram atualizados vários nomes de propriedades de mídia](https://github.com/adobe/xdm/pull/1626/files) entre vários tipos de dados para fins de consistência. |
| Tipo de dados | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Adição de nomes conhecidos para flutter. |
| Tipo de dados | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | O tipo de dados agora pode aceitar uma lista de pares de valores-chave de metadados associados ao ponto de interesse. |
| Tipo de dados | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] foi renomeado para [!UICONTROL Proposition Action]. |
| Tipo de dados | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] foi renomeado para [!UICONTROL Proposition Action]. |
| (Vários) | (Vários) | As propriedades experimentais foram [estabilizadas em todos os componentes B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Vários) | (Vários) | As entidades Adobe Journey Optimizer foram [estabilizadas](https://github.com/adobe/xdm/pull/1625/files). |
| (Vários) | (Vários) | Os namespaces de determinados campos em vários componentes experimentais foram [atualizados para consistência](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## Serviço de identidade {#identity-service}

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente pareça ter várias &quot;identidades&quot;.

O Serviço de identidade da Adobe Experience Platform ajuda você a ter uma melhor visão do cliente e do comportamento dele, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para exclusão do conjunto de dados | O Serviço de Identidade agora oferece suporte à exclusão do conjunto de dados ao solicitar por meio da [API do Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), da interface ou da Higiene de Dados. Leia o manual sobre [exclusão de conjuntos de dados na interface](../../catalog/datasets/user-guide.md#delete-a-dataset) para obter mais informações. |

Para saber mais sobre o Serviço de identidade, leia a [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Query Service {#query-service}

O Query Service permite usar SQL padrão para consultar dados no [!DNL Data Lake] da Adobe Experience Platform. Você pode ingressar em qualquer conjunto de dados do [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| API de assinatura em alerta | O Adobe Experience Platform Query Service permite assinar alertas para consultas ad hoc e programadas. Os alertas podem ser recebidos por email, na interface do usuário do Experience Platform ou em ambas. Atualmente, alertas de consulta só podem ser assinados usando a [API de Serviço de Consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Amostras de conjunto de dados | As amostras de conjunto de dados do Serviço de consulta permitem realizar consultas exploratórias sobre grandes volumes de dados com tempo de processamento bastante reduzido, à custa da precisão da consulta. Consulte o [guia de amostras do conjunto de dados](../../query-service/key-concepts/dataset-samples.md) para saber mais. |

Para obter mais informações sobre [!DNL Query Service], consulte a [[!DNL Query Service] visão geral](../../query-service/home.md).

Consulte a [documentação de alertas de consulta](../../query-service/api/alert-subscriptions.md) para saber mais.

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Impacto do preenchimento do segmento do Audience Manager no Perfil do cliente em tempo real | A assimilação de populações consideráveis de segmentos do Audience Manager afeta diretamente a contagem total de perfis ao enviar pela primeira vez um segmento do Audience Manager para o Experience Platform usando a origem do Audience Manager. Isso significa que selecionar todos os segmentos pode levar a uma contagem de perfis que excede seu direito de uso de licença. Para obter mais informações, leia a [visão geral da origem do Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obter informações sobre o uso de sua licença, leia a documentação em [usando o painel de uso de licença](../../dashboards/guides/license-usage.md). |
| Suporte ao Adobe Campaign Managed Cloud Service | Use a fonte do Adobe Campaign Managed Cloud Service para trazer sua entrega do Adobe Campaign v8.4 e os dados de logs de rastreamento para a Experience Platform. Leia o manual sobre [criação de uma conexão de origem do Adobe Campaign Managed Cloud Service na interface](../../sources/tutorials/ui/create/adobe-applications/campaign.md) para obter mais informações. |
| Suporte de API para assimilação sob demanda para origens em lote | Use a assimilação sob demanda para criar execuções de fluxo ad hoc para um determinado fluxo de dados com a API [!DNL Flow Service]. As execuções de fluxo criadas devem ser definidas para assimilação única. Para obter mais informações, leia o manual sobre [criação de uma execução de fluxo para assimilação sob demanda usando a API](../../sources/tutorials/api/on-demand-ingestion.md) para obter mais informações. |
| Suporte de API para repetição de execuções de fluxo de dados com falha para fontes em lote | Use a operação `re-trigger` para repetir seu fluxo de dados com falha por meio da API. Leia o manual sobre [tentativas de execução de fluxo de dados com falha usando a API](../../sources/tutorials/api/retry-flows.md) para obter mais informações. |
| Suporte de API para filtragem de dados em nível de linha para as fontes [!DNL Google BigQuery] e [!DNL Snowflake] | Use operadores lógicos e de comparação para filtrar dados de nível de linha para as fontes [!DNL Google BigQuery] e [!DNL Snowflake]. Leia o manual sobre [filtragem de dados de uma origem usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |

Para saber mais sobre origens, leia a [visão geral de origens](../../sources/home.md).
