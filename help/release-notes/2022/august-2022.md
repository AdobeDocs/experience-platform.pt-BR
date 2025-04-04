---
title: Notas de versão de agosto de 2022 da Adobe Experience Platform
description: As notas de versão de agosto de 2022 da Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 26%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 24 de agosto de 2022**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Os serviços de IA/ML permitem que analistas e profissionais de marketing aproveitem o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam modelos específicos para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento especializado em ciência de dados.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ela pode ser usada por comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para privacidade | <ul><li> A IA de atribuição agora oferece suporte à definição de funções de usuário e políticas de acesso para gerenciar [permissões](../../../help/access-control/abac/ui/permissions.md) para recursos e objetos em um aplicativo de produto. </li><li>Os recursos de log de auditoria são registrados automaticamente conforme a atividade ocorre.</li><li> Por meio do [controle de acesso baseado em atributos](../../access-control/abac/overview.md), os administradores podem controlar o acesso a objetos e/ou recursos específicos com base em determinados atributos, que podem ser metadados adicionados a um objeto, como rótulos. Os administradores também podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.</li><li>A IA de atribuição aproveita os conjuntos de dados do Experience Platform. Para atender às solicitações de direitos do consumidor que uma marca pode receber, as marcas devem usar o Experience Platform Privacy Service para enviar solicitações do consumidor de acesso e exclusão para remover seus dados no data lake, no Serviço de identidade e no Perfil do cliente em tempo real.  </li><li>Todos os conjuntos de dados usados para entrada/saída de modelos seguirão as diretrizes do Experience Platform. A Criptografia de dados da Experience Platform se aplica a dados inativos e em trânsito. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Observação**: a IA de atribuição não estará disponível para clientes existentes do Healthcare Shield até aviso em contrário.

Para obter mais informações sobre a IA de atribuição, consulte a visão geral da [IA de atribuição](../../intelligent-services/attribution-ai/overview.md).

### IA do cliente

A IA do cliente, disponível no Real-Time Customer Data Platform, é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para privacidade | <ul><li> A IA do cliente agora oferece suporte à definição de funções de usuário e políticas de acesso para gerenciar [permissões](../../../help/access-control/abac/ui/permissions.md) para recursos e objetos em um aplicativo de produto. </li><li>Os recursos de log de auditoria são registrados automaticamente conforme a atividade ocorre.</li><li> Por meio do [controle de acesso baseado em atributos](../../access-control/abac/overview.md), os administradores podem controlar o acesso a objetos e/ou recursos específicos com base em determinados atributos. Esses atributos podem ser metadados adicionados a um objeto, como rótulos. Os administradores também podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.</li><li>A IA do cliente aproveita os conjuntos de dados da Experience Platform. Para atender às solicitações de direitos do consumidor que uma marca pode receber, as marcas devem usar o Experience Platform Privacy Service para enviar solicitações do consumidor de acesso e exclusão para remover seus dados no data lake, no Serviço de identidade e no Perfil do cliente em tempo real. </li><li>Todos os conjuntos de dados usados para entrada/saída de modelos seguirão as diretrizes do Experience Platform. A Criptografia de dados da Experience Platform se aplica a dados inativos e em trânsito. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Observação**: a IA do cliente não estará disponível para os clientes existentes do Healthcare Shield até que seja especificado.

Para obter mais informações sobre a IA do cliente, consulte a visão geral da [IA do cliente](../../intelligent-services/customer-ai/overview.md).

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] através dos quais você pode visualizar insights importantes sobre os dados da sua organização, conforme capturados durante os instantâneos diários.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de ativações programadas | O widget [!UICONTROL Ativações agendadas] fornece um modo de exibição tabulado dos destinos ativados mais recentemente. Para cada segmento, inclui o nome, a plataforma de destino e as datas de início e término da ativação. Esse widget permite descobrir onde e quando o público-alvo está sendo ativado e torna mais transparentes as ativações duplicadas ou desnecessárias. Essas informações acumuladas também destacam onde as ativações foram deixadas de fora. |

Para obter mais informações sobre [!DNL Dashboards], consulte a [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para assimilação de registros com avisos | O Preparo de dados agora localizará avisos (erros não críticos) nos campos e permitirá que o restante da linha seja assimilado. Todos os erros de transformação do mapeador agora são relatados como avisos, e as linhas que são parcialmente assimiladas são consideradas bem-sucedidas, com um aviso.  O monitoramento também é suportado em registros com avisos e detalhes de diagnóstico. Atualmente, a assimilação parcial de registros com avisos está disponível apenas para dados de transmissão. Revise a documentação sobre [assimilando registros com avisos](../../sources/tutorials/ui/monitor-streaming.md) para obter mais informações. |

{style="table-layout:auto"}

Para saber mais sobre [!DNL Data Prep], consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| (Beta) Suporte à personalização baseada em atributos para destinos de personalização | Com a versão beta da personalização baseada em atributos, você verá dois novos cartões no [catálogo de destino](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: este conector está atualmente na versão beta e só está disponível para um número selecionado de clientes. Além da funcionalidade fornecida pela placa Adobe Target V1, o conector Target V2 adiciona uma [etapa de mapeamento](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) ao fluxo de trabalho de ativação, que permite mapear atributos de perfil para o Adobe Target, permitindo a personalização de mesma página e próxima página baseada em atributos.</li><li>**[!UICONTROL Personalization Personalizado com Atributos]**: este conector está atualmente na versão beta e só está disponível para um número selecionado de clientes. Além da funcionalidade fornecida pelo **[!UICONTROL Personalization Personalizado]**, o conector do **[!UICONTROL Personalization Personalizado com Atributos]** adiciona uma [etapa de mapeamento](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) opcional ao fluxo de trabalho de ativação, que permite mapear atributos de perfil para o destino de personalização personalizado, habilitando a personalização de mesma página e próxima página baseada em atributos.</li></ul> <br> Os atributos de perfil podem conter dados confidenciais. Para proteger esses dados, o destino **[!UICONTROL Personalization Personalizado com Atributos]** requer que você use a [API do Edge Network Server](../../server-api/overview.md) para coleta de dados. Além disso, todas as chamadas da API do Servidor devem ser feitas em um [contexto autenticado](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) é um Experience Platform de Execução de Vendas com a maioria dos dados de interação comprador-vendedor B2B do mundo e investimentos significativos em tecnologias de IA proprietárias para traduzir dados de vendas em inteligência. O [!DNL Outreach] ajuda as organizações a automatizar o envolvimento de vendas e agir com base na inteligência de receita para melhorar sua eficiência, previsibilidade e crescimento. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos componentes de XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Classe de Entidade AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | Uma classe baseada em registros para criar esquemas de pesquisa para o Adobe Journey Optimizer. |
| Grupo de campos | [[!UICONTROL Objetos de Trabalho do Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Um grupo de campos do invólucro que faz referência a todos os grupos de campos específicos de objetos de nível inferior do Adobe Workfront. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos Comuns de Eventos de Etapa do Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Duas novas propriedades foram adicionadas: `origTimeStamp` e `experienceID`. |
| Grupo de campos | [[!UICONTROL Detalhes da associação de segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Além do [!UICONTROL Perfil Individual XDM], este grupo de campos agora também pode ser usado em esquemas baseados na classe Conta Comercial XDM. |
| Grupo de campos | (Vários) | Vários grupos de campos relacionados às atividades B2B do Marketo foram atualizados para o status estável. Consulte a seguinte [solicitação de pull](https://github.com/adobe/xdm/pull/1593/files) para obter detalhes. |
| Grupo de campos | (Vários) | Vários grupos de campos relacionados à meteorologia foram atualizados para corrigir erros que estavam ocorrendo para `uvIndex` e `sunsetTime`. Consulte a seguinte [solicitação de pull](https://github.com/adobe/xdm/pull/1602/files) para obter detalhes. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Uma nova propriedade `productImageUrl` foi adicionada. |
| Tipo de dados | [[!UICONTROL Informações detalhadas de dados de QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Uma nova propriedade `framesPerSecond` foi adicionada. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | A `sdkVersion` foi renomeada como `appVersion`. Os campos `meta:enum` e `description` também foram atualizados. |
| Tipos de dados e grupos de campos | (Vários) | Vários tipos de dados de mídia e grupos de campos têm novos campos e descrições atualizadas. Consulte a seguinte [solicitação de pull](https://github.com/adobe/xdm/pull/1582/files) para obter detalhes. |
| (Todos) | (Vários) | Todos os objetos de esquema que contêm um campo `enum` agora também contêm um campo `meta:enum` correspondente para indicar valores de exibição para cada restrição. Consulte a seguinte [solicitação de pull](https://github.com/adobe/xdm/pull/1601/files) para obter detalhes. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Limite rígido das políticas de mesclagem | O Experience Platform agora aplicará um limite rígido de **cinco** políticas de mesclagem por sandbox. Se sua sandbox tiver mais de cinco políticas de mesclagem, você **não** poderá criar novas políticas de mesclagem até que a sandbox tenha menos de cinco políticas de mesclagem. |
| Limpeza de atributo de borda de perfil órfão | Para todas as organizações, o Serviço de perfil agora remove os atributos de borda restantes da região de atividade do usuário diariamente, fornecendo uma representação mais precisa dos perfis no sistema. Essa limpeza ocorre depois que todos os fragmentos de perfil de um determinado perfil são excluídos e deve afetar os perfis que estão sendo mesclados de conjuntos de dados em que `com_adobe_aep_profile_region_dataset` está marcado como `true`. Isso pode mostrar uma queda na métrica &quot;Público-alvo endereçável&quot; no painel de uso da licença e uma queda na métrica &quot;Contagem de perfis&quot; no painel Perfil, já que essas métricas incluíam fragmentos de atributos de borda restantes antes desta versão. |

{style="table-layout:auto"}

Para saber mais sobre o Perfil de cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para 4.000 segmentos | Todas as organizações com o Experience Platform agora podem oferecer suporte a até 4.000 definições de segmento. Para obter mais informações sobre como essa alteração afeta as APIs de trabalho do segmento, leia o [manual do ponto de extremidade de trabalho do segmento](../../segmentation/api/segment-jobs.md) |

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de Origens de Autoatendimento (SDK em Lote) | Desenvolva, teste e integre sua fonte de dados baseada em API REST para assimilar dados em lote no Experience Platform usando especificações de fonte fáceis de configurar. Com a SDK de origens, é possível: <ul><li>Configure uma nova fonte para o catálogo do Experience Platform.</li><li>Defina especificações para sua origem, incluindo informações relacionadas aos tipos de autenticação compatíveis, programação e como os dados de recursos são obtidos.</li><li>Crie documentação voltada para o usuário para sua nova fonte.</li></ul> Para obter mais informações, leia a documentação sobre [Fontes de autoatendimento (SDK em lote)](../../sources/sources-sdk/overview.md). |
| Disponibilidade geral da origem [!DNL Google BigQuery] | Use a origem [!DNL Google BigQuery] para assimilar dados do data warehouse [!DNL Google BigQuery] na Experience Platform. Para obter mais informações, leia a documentação na [[!DNL Google BigQuery] origem](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] origem (Beta) | Use a fonte [!DNL Teradata Vantage] para assimilar dados de ambientes híbridos de várias nuvens para o Experience Platform. Para obter mais informações, leia a documentação na [[!DNL Teradata Vantage] origem](../../sources/connectors/databases/teradata-vantage.md). |
| Suporte entre regiões para origem no Adobe Analytics | Agora é possível assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura). Os conjuntos de relatórios devem ser mapeados para a mesma organização da instância de sandbox da Experience Platform em que a conexão de origem está sendo criada. Para obter mais informações, leia o manual sobre [criação de uma conexão de origem do Adobe Analytics na interface](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
