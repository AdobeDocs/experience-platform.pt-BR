---
title: Notas de versão da Adobe Experience Platform de setembro de 2022
description: As notas de versão de setembro de 2022 para o Adobe Experience Platform.
source-git-commit: 45281721c6fb26c303bb820fa39f5c6ed71b55f9
workflow-type: tm+mt
source-wordcount: '3059'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 28 de setembro de 2022**

Novos recursos no Adobe Experience Platform:

- [Controle de acesso baseado em atributos](#abac)
- [Higiene dos dados](#data-hygiene)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Logs de auditoria](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Coleta de dados](#data-collection)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## Controle de acesso baseado em atributos {#abac}

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos será ativado a partir de outubro de 2022. Se você deseja adotar precocemente, entre em contato com o representante do Adobe.

O controle de acesso baseado em atributos é um recurso da Adobe Experience Platform que oferece às marcas conscientes da privacidade mais flexibilidade para gerenciar o acesso do usuário. Objetos individuais, como campos de esquema e segmentos, podem ser atribuídos a funções de usuário. Esse recurso permite que você conceda ou revogue o acesso a objetos individuais para usuários específicos da Plataforma em sua organização.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários, os dados pessoais confidenciais (SPD), as informações de identificação pessoal (PII) e outros tipos personalizados de dados em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que têm acesso apenas a campos e dados específicos que correspondem a esses campos.

| Recurso | Descrição |
| --- | --- |
| Controle de acesso baseado em atributos | O controle de acesso baseado em atributos permite rotular campos de esquema do Experience Data Model (XDM) e segmentos com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuário e função para definir políticas de acesso que abrangem campos e segmentos de esquema XDM para gerenciar melhor o acesso dado aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Para obter mais informações, consulte o [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). |
| Permissões | Permissões é a área do Experience Cloud, onde os administradores podem definir funções de usuário e políticas de acesso para gerenciar permissões de acesso para recursos e objetos em um aplicativo de produto. Por meio das Permissões, é possível criar e gerenciar funções, atribuir as permissões de recurso desejadas para essas funções e criar políticas para aproveitar rótulos e definir quais funções de usuário têm acesso a recursos específicos da Plataforma. As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica. Para obter mais informações, consulte o [Guia da interface do usuário de permissões](../../access-control/abac/ui/browse.md). |

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte o [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). Para obter um guia abrangente sobre o fluxo de trabalho de controle de acesso baseado em atributos, leia o [guia completo do controle de acesso baseado em atributos](../../access-control/abac/end-to-end-guide.md).

## Higiene dos dados {#data-hygiene}

O Adobe Experience Platform fornece um conjunto robusto de ferramentas para gerenciar operações de dados grandes e complicadas a fim de orquestrar experiências do consumidor. À medida que os dados são assimilados no sistema ao longo do tempo, torna-se cada vez mais importante gerenciar seus armazenamentos de dados para que eles sejam usados conforme esperado, atualizados quando for necessário corrigir dados incorretos e excluídos quando as políticas organizacionais o considerarem necessário.

Os recursos de higiene dos dados da Adobe Experience Platform permitem que você limpe seus dados agendando expirações automatizadas do conjunto de dados e excluindo programaticamente os dados do consumidor por identidade.

>[!IMPORTANT]
>
>Os recursos de higiene de dados só estão disponíveis para organizações que compraram o Adobe Healthcare Shield.

Consulte a documentação a seguir para começar a usar a higiene dos dados:

- [Visão geral da higiene de dados](../../hygiene/home.md): Saiba mais sobre as noções básicas sobre os recursos de higiene de dados da Platform.
- [[!UICONTROL Higiene de dados] Guia da interface do usuário](../../hygiene/ui/overview.md): Saiba como agendar as expirações do conjunto de dados e as solicitações de exclusão do consumidor na interface do usuário da plataforma.
- [Guia da API de higiene de dados](../../hygiene/api/overview.md): Todas as atividades de higiene de dados que você pode executar na interface do usuário também podem ser programáticas

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Os serviços de IA/ML capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que analistas de marketing configurem modelos específicos às necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento em ciência de dados.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
| --- | --- |
| Salvar instância de rascunho | Esse novo recurso permite que analistas de marketing salvem uma configuração de modelo como uma instância de rascunho e continuem a editá-la até que ela seja concluída antes do treinamento e da pontuação. Os cenários em que esse recurso é útil incluem, quando um usuário tem vários campos para definir no fluxo de trabalho, mas não pode concluí-lo devido a restrições de tempo. Outro cenário é quando uma ou mais estatísticas de conjunto de dados estão sendo processadas e ainda não estão disponíveis. Leia o [Guia do usuário do Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) para saber mais. |
| Políticas de governança | Depois que os usuários enviam para criar uma instância por meio do fluxo de trabalho de configuração, o novo serviço de aplicação de política verifica se há violações de política do uso de dados e exibe os detalhes em uma janela. Ela garante que as operações de dados e as ações de marketing sejam compatíveis com as políticas de uso de dados configuradas no Adobe Experience Platform. |

Para obter mais informações sobre o Attribution AI, a variável [Visão geral do Attribution AI](../../intelligent-services/attribution-ai/overview.md). Para obter informações sobre políticas de governança de dados, leia a [visão geral das políticas](../../data-governance/policies/overview.md).

### Customer AI

O Customer AI disponível no Real-time Customer Data Platform é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala.

| Recurso | Descrição |
| --- | --- |
| Salvar instância de rascunho | Esse novo recurso permite que analistas de marketing salvem uma configuração de modelo como uma instância de rascunho e continuem a editá-la até que ela seja concluída antes do treinamento e da pontuação. Os cenários em que esse recurso é útil incluem, quando um usuário tem vários campos para definir no fluxo de trabalho, mas não pode concluí-lo devido a restrições de tempo. Outro cenário é quando uma ou mais estatísticas de conjunto de dados estão sendo processadas e ainda não estão disponíveis. Leia o [Guia do usuário de IA do cliente](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) para saber mais. |
| Políticas de governança | Depois que os usuários enviam para criar uma instância por meio do fluxo de trabalho de configuração, o novo serviço de aplicação de política verifica se há violações de política do uso de dados e exibe os detalhes em uma janela. Ela garante que as operações de dados e as ações de marketing sejam compatíveis com as políticas de uso de dados configuradas no Adobe Experience Platform. |

Para obter mais informações sobre a API do cliente, leia o [Visão geral do Customer AI](../../intelligent-services/customer-ai/overview.md). Para obter informações sobre políticas de governança de dados, leia a [visão geral das políticas](../../data-governance/policies/overview.md).

## Logs de auditoria {#audit-logs}

O Experience Platform permite auditar a atividade do usuário para vários serviços e recursos. Os logs de auditoria fornecem informações sobre quem fez o quê e quando.

**Recursos atualizados**

| Recurso | Nome | Descrição |
| --- | --- | --- |
| Recursos adicionados | <ul><li>Instância do Attribution AI</li><li>Instância do Customer AI</li><li>Datastream</li></ul> | Os recursos do log de auditoria são registrados automaticamente conforme a atividade ocorre. Se o recurso estiver ativado, não é necessário ativar manualmente a coleta de log. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre os diferentes tipos de eventos específicos de recursos rastreados por logs de auditoria na Platform, consulte o [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, como capturados durante os instantâneos diários.

| Recurso | Descrição |
| --- | --- |
| Rótulo em uso | Quando visualizado na biblioteca de widgets, o rótulo em uso identifica facilmente a presença de widgets existentes no painel. Isso facilita evitar a duplicação, embora você ainda possa adicionar o mesmo widget mais de uma vez, se desejar. |
| Painéis definidos pelo usuário | Painéis definidos pelo usuário ajudam a agilizar insights e personalizar visualizações, permitindo que você crie e gerencie painéis personalizados. Com painéis definidos pelo usuário, você pode criar, adicionar e editar widgets de sobreposição para visualizar métricas principais relevantes para sua organização. Leia o [guia de recursos](../../dashboards/user-defined-dashboards.md) para saber mais. |
| Modelo de dados de insights da plataforma de dados do cliente | O recurso Modelo de dados de insights da CDP (Plataforma de dados do cliente) expõe os modelos de dados e o SQL que alimenta os insights de vários perfis, destinos e widgets de segmentação. Você pode personalizar esses modelos de consulta SQL para criar relatórios de CDP para seus casos de uso de indicador de desempenho principal e de marketing. Esses insights podem ser usados como widgets personalizados para seus painéis definidos pelo usuário. Leia o [Guia de recursos do Modelo de dados de insights de CDP](../../dashboards/cdp-insights-data-model.md) para saber mais. |
| Dispositivo de relatório de sobreposição de público-alvo | Este widget está disponível para ambos [!UICONTROL Perfis] e [!UICONTROL Segmentos] painéis. O relatório fornece uma lista ordenada de públicos-alvo classificados pelas porcentagens de sobreposição mais alta ou mais baixa para o segmento escolhido. No [!UICONTROL Perfis] no painel, é possível filtrar e exibir a sobreposição do público-alvo por política de mesclagem de todos os segmentos disponíveis. O [!UICONTROL Segmentos] painéis permitem filtrar a sobreposição de público-alvo por um segmento específico.<br>Use essa análise para criar segmentos novos e de alto desempenho e evitar o envio do mesmo público-alvo para destinos diferentes. O relatório também ajuda a identificar insights ocultos para melhorar a segmentação ou localizar perfis únicos a serem perseguidos. Leia as respectivas [perfis](../../dashboards/guides/profiles.md#audience-overlap-report) e [segmentos](../../dashboards/guides/segments.md#audience-overlap-report) guias de widget para saber mais. |

Para obter mais informações sobre [!DNL Dashboards]consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não-Adobe.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Integração de navegação à esquerda na interface do usuário da plataforma | Todos os recursos que antes eram exclusivos da interface do usuário da coleta de dados (incluindo tags, encaminhamento de eventos e datastreams) agora também estão disponíveis por meio da navegação à esquerda no Experience Platform, na categoria **[!UICONTROL Coleta de dados]**. Isso elimina a necessidade de alternar entre interfaces do usuário ao trabalhar com recursos de coleta de dados na Plataforma. |
| Atribuição de usuário em tags e encaminhamento de evento | Quando disponível [!UICONTROL Propriedades] nas tags e no encaminhamento de eventos, cada propriedade listada agora mostra quando foi atualizada pela última vez e qual usuário fez a atualização. |
| [[!DNL User-Agent Client Hints] no SDK da Web](../../edge/fundamentals/user-agent-client-hints.md) | O SDK da Web agora é compatível [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). As dicas do cliente permitem que os proprietários do site acessem grande parte das mesmas informações disponíveis no [!DNL User-Agent] , mas de uma maneira mais preservada da privacidade. |
| [Migração de página por página do SDK da Web](../../edge/home.md#migrating-to-web-sdk) | Agora é possível migrar as propriedades da Web existentes de outras bibliotecas do Experience Cloud, como [!DNL at.js], para o SDK da Web, uma página de cada vez. Isso permite uma abordagem em fases para a migração do SDK da Web, sem a necessidade de migrar todas as suas páginas de uma só vez. |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

Para obter mais informações sobre a coleta de dados no Platform, consulte o [visão geral da coleta de dados](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| SDK de destino | O Destination SDK agora oferece suporte total para parceiros e clientes que criam destinos em lote (ou baseados em arquivos) produzidos ou privados. Leia as seguintes páginas de documentação para obter mais informações: <ul><li>[Visão geral do Destination SDK](/help/destinations/destination-sdk/overview.md)</li><li>[Configurar um destino com base em arquivo](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Configurar opções de formatação de arquivo para destinos com base em arquivo](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Teste os destinos com base em arquivo](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Destinos novos ou atualizados**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | O Adobe Campaign Managed Cloud Services fornece uma plataforma para projetar experiências de clientes entre canais e um ambiente para a orquestração visual de campanhas, o gerenciamento de interação em tempo real e a execução entre canais. [Introdução ao Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Observe que essa integração funciona com [Adobe Campaign versão 8.4 ou superior](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | O [!DNL Salesforce CRM] O destino foi atualizado para oferecer suporte a atualizações de contatos e leads, bem como aprimoramentos de desempenho para atualizações mais rápidas. |

{style=&quot;table-layout:auto&quot;}

**Documentação nova ou atualizada**

| Documentação | Descrição |
| ----------- | ----------- |
| Documentação da API do Serviço de fluxo de destinos | O [Documentação de referência da API de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/) O foi atualizado para incluir orientação sobre como executar operações em destinos com base em arquivos. As operações para destinos de transmissão serão adicionadas posteriormente. |

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte à interface do usuário para enumerações e valores sugeridos | Além dos enumerações que permitem a validação de dados, agora é possível [adicionar ou remover valores sugeridos](../../xdm/ui/fields/enum.md) para campos de sequência padrão ou personalizados, de modo que os usuários da plataforma tenham uma lista amigável de valores para selecionar ao criar segmentos. |

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos de classificação AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | As propriedades de um elemento específico com o qual foi interagido e o qual o evento de proposta foi acionado. |
| Grupo de campos | [[!UICONTROL Detalhes da interação do MediaAnalytics]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Rastreia interações de mídia ao longo do tempo. |
| Grupo de campos | [[!UICONTROL Informações de detalhes da mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Rastreia informações de detalhes da mídia. |
| Grupo de campos | [[!UICONTROL Adobe CJM ExperienceEvent - Superfícies]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Descreve superfícies para Eventos de experiência no Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Comportamento | [[!UICONTROL Série cronológica]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Valores adicionados para `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Valores removidos para `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Grupo de campos | (Várias) | [Várias descrições de campo atualizadas](https://github.com/adobe/xdm/pull/1628/files) em componentes Journey Orchestration. |
| Grupo de campos | (Várias) | [Atualização dos títulos de vários componentes do Adobe Workfront](https://github.com/adobe/xdm/pull/1634/files) para fins de consistência. |
| Grupo de campos | [[!UICONTROL Campos de classificação AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | Atualização dos namespaces de vários campos para `xdm`. |
| Grupo de campos | [[!UICONTROL Campos comuns do evento Journey Orchestration Step]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Adição de um novo campo, `isReadSegmentTriggerStartEvent`. |
| Grupo de campos | [[!UICONTROL Previsão de Penas]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Alterado o `xdm:uvIndex` para um tipo inteiro e adicionado o `xdm` namespace para vários campos em que estava ausente. |
| Grupo de campos | [[!UICONTROL Informações de detalhes da mídia]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` e `xdm:implementationDetails` foram removidas do grupo de campos. |
| Tipo de dados | (Várias) | [Atualização de vários nomes de propriedade de mídia](https://github.com/adobe/xdm/pull/1626/files) em vários tipos de dados para fins de consistência. |
| Tipo de dados | [[!UICONTROL Detalhes da implementação]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Adição de nomes conhecidos para flutter. |
| Tipo de dados | [[!UICONTROL Detalhes do ponto de interesse]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | O tipo de dados agora pode aceitar uma lista de pares de valores-chave de metadados associados ao ponto de interesse. |
| Tipo de dados | [[!UICONTROL Ação da proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] foi renomeado para [!UICONTROL Ação da proposta]. |
| Tipo de dados | [[!UICONTROL Tipo de evento de proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] foi renomeado para [!UICONTROL Ação da proposta]. |
| (Várias) | (Várias) | As propriedades experimentais foram [estabilizado em todos os componentes B2B](https://github.com/adobe/xdm/pull/1617/files). |
| (Várias) | (Várias) | As entidades da Adobe Journey Optimizer foram [estabilizado](https://github.com/adobe/xdm/pull/1625/files). |
| (Várias) | (Várias) | Os namespaces de determinados campos em vários componentes experimentais foram [atualizado para consistência](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Serviço de identidade {#identity-service}

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em diferentes sistemas, fazendo com que cada cliente pareça ter várias &quot;identidades&quot;.

O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para exclusão de conjunto de dados | O Serviço de identidade agora oferece suporte à exclusão do conjunto de dados ao solicitar por meio do [API do Serviço de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), da interface do usuário ou da higiene de dados. Leia o guia em [exclusão de conjuntos de dados na interface do usuário](../../catalog/datasets/user-guide.md#delete-a-dataset) para obter mais informações. |

Para saber mais sobre o Serviço de identidade, leia a [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Serviço de query {#query-service}

O Serviço de Consulta permite que você use o SQL padrão para consultar dados no Adobe Experience Platform [!DNL Data Lake]. É possível unir qualquer conjunto de dados da [!DNL Data Lake] e capture os resultados do query como um novo conjunto de dados para usar nos relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| API de assinatura de alerta | O Adobe Experience Platform Query Service permite assinar alertas para consultas ad hoc e programadas. Os alertas podem ser recebidos por email, na interface do usuário da plataforma ou em ambos. Atualmente, os alertas de consulta só podem assinar o usando o [API do serviço de consulta](https://developer.adobe.com/experience-platform-apis/references/query-service/). Consulte a [documentação dos alertas de consulta](../../query-service/api/alert-subscriptions.md) para saber mais. |
| Amostras do conjunto de dados | Amostras de conjunto de dados do Serviço de query permitem realizar consultas exploratórias em grandes dados com um tempo de processamento muito reduzido ao custo da precisão da consulta. Consulte a [guia de amostras do conjunto de dados](../../query-service/sql/dataset-samples.md) para saber mais. |

Para obter mais informações sobre [!DNL Query Service]consulte o [[!DNL Query Service] visão geral](../../query-service/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Impacto da população do segmento Audience Manager no Perfil do cliente em tempo real | A assimilação de populações de segmentos de Audience Manager consideráveis afeta diretamente a contagem total de perfis ao enviar um segmento de Audience Manager para a Platform pela primeira vez usando a fonte de Audience Manager. Isso significa que a seleção de todos os segmentos pode levar a uma contagem de Perfis além do seu direito de uso de licença. Para obter mais informações, leia a [Visão geral da fonte de Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obter informações sobre o uso da licença, leia a documentação em [uso do painel de uso da licença](../../dashboards/guides/license-usage.md). |
| Suporte para Adobe Campaign Managed Cloud Service | Use a fonte Adobe Campaign Managed Cloud Service para trazer seus dados de delivery e logs de rastreamento do Adobe Campaign v8.4 para o Experience Platform. Leia o guia em [criação de uma conexão de origem Cloud Service gerenciada da Adobe Campaign na interface do usuário](../../sources/tutorials/ui/create/adobe-applications/campaign.md) para obter mais informações. |
| Suporte a API para assimilação sob demanda para fontes em lote | Use a assimilação sob demanda para criar execuções de fluxo ad hoc para um determinado fluxo de dados com o [!DNL Flow Service] API. As execuções de fluxo criadas devem ser definidas para assimilação única. Para obter mais informações, leia o guia sobre [criação de uma execução de fluxo para assimilação sob demanda usando a API](../../sources/tutorials/api/on-demand-ingestion.md) para obter mais informações. |
| Suporte à API para tentativa de repetição de execuções de fluxo de dados com falha para fontes em lote | Use o `re-trigger` para tentar novamente o fluxo de dados com falha por meio da API. Leia o guia em [tentativa de executar o fluxo de dados com falha usando a API](../../sources/tutorials/api/retry-flows.md) para obter mais informações. |
| Suporte a API para filtrar dados em nível de linha para a variável [!DNL Google BigQuery] e [!DNL Snowflake] fontes | Use operadores lógicos e de comparação para filtrar dados em nível de linha para a variável [!DNL Google BigQuery] e [!DNL Snowflake] fontes. Leia o guia em [filtragem de dados de uma fonte usando a API](../../sources/tutorials/api/filter.md) para obter mais informações. |

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).