---
title: Notas de versão da Adobe Experience Platform de agosto de 2022
description: As notas de versão de agosto de 2022 para o Adobe Experience Platform.
source-git-commit: 5967dee9c8b1c05ebd103998021e02a47ac3982c
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 6%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de agosto de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Preparação de dados](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para assimilar registros com avisos | A Preparação de dados agora localiza avisos (erros não críticos) nos campos e permitirá que o restante da linha seja assimilado. Todos os erros de transformação do mapeador agora são relatados como avisos e linhas que são parcialmente assimiladas são consideradas bem-sucedidas, com um aviso.  Também há suporte para monitoramento em registros com avisos e detalhes de diagnóstico. A assimilação parcial de registros com avisos está atualmente disponível apenas para dados de transmissão. Revise a documentação em [assimilação de registros com avisos](../../sources/tutorials/ui/monitor-streaming.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre [!DNL Data Prep], consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Schema global | [[!UICONTROL Esquema de entidade AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Descreve entidades desnormalizadas para o Adobe Journey Optimizer. |
| Classe | [[!UICONTROL Entidades de Execução AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Descreve entidades de execução do Adobe Journey Optimizer para usar na segmentação. |
| Grupo de campos | [[!UICONTROL Objetos de trabalho do Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Um grupo de campos wrapper que faz referência a todos os grupos de campos específicos de objetos de nível inferior para o Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos comuns do evento Journey Orchestration Step]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Duas novas propriedades foram adicionadas: `origTimeStamp` e `experienceID`. |
| Grupo de campos | [[!UICONTROL Detalhes da associação ao segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Além de [!UICONTROL Perfil individual XDM], esse grupo de campos agora também pode ser usado em esquemas com base na classe de conta comercial XDM. |
| Grupo de campos | (Várias) | Vários grupos de campos relacionados às atividades do Marketo B2B foram atualizados para o status estável. Veja o seguinte [solicitação pull](https://github.com/adobe/xdm/pull/1593/files) para obter detalhes. |
| Grupo de campos | (Várias) | Vários grupos de campos relacionados ao clima foram atualizados para corrigir erros que estavam ocorrendo para `uvIndex` e `sunsetTime`. Veja o seguinte [solicitação pull](https://github.com/adobe/xdm/pull/1602/files) para obter detalhes. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Uma nova propriedade `productImageUrl` foi adicionada. |
| Tipo de dados | [[!UICONTROL Informações de detalhes de dados de Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Uma nova propriedade `framesPerSecond` foi adicionada. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | A `sdkVersion` foi renomeada como `appVersion`. `meta:enum` e `description` os campos também foram atualizados. |
| Tipos de dados e grupos de campos | (Várias) | Vários tipos de dados de mídia e grupos de campos têm novos campos e descrições atualizadas. Veja o seguinte [solicitação pull](https://github.com/adobe/xdm/pull/1582/files) para obter detalhes. |
| (Todas) | (Várias) | Todos os objetos de esquema que contêm uma `enum` agora, também contém um `meta:enum` campo para indicar valores de exibição para cada restrição. Veja o seguinte [solicitação pull](https://github.com/adobe/xdm/pull/1601/files) para obter detalhes. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Limpeza de atributo de borda de perfil órfão | Para todas as organizações, o Serviço de perfil agora remove os atributos de borda esquerda da região da atividade do usuário diariamente para fornecer uma representação mais precisa dos perfis em seu sistema. Essa limpeza ocorre depois que todos os fragmentos de perfil de um determinado perfil são excluídos e deve afetar os perfis que estão sendo mesclados de conjuntos de dados em que `com_adobe_aep_profile_region_dataset` está marcado como `true`. Isso pode mostrar uma queda na métrica &quot;Público-alvo endereçável&quot; no painel de uso da licença e pode mostrar uma queda na métrica &quot;Contagem de perfil&quot; no painel Perfil, já que essas métricas incluíam fragmentos de atributo de borda esquerda antes desta versão. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo o [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para 4000 segmentos | Todas as organizações com a Platform agora podem oferecer suporte a até 4000 definições de segmento. Para obter mais informações sobre como essa alteração afeta as APIs de tarefas do segmento, leia o [guia do endpoint de tarefas do segmento](../../segmentation/api/segment-jobs.md) |

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de fontes de autoatendimento (SDK em lote) | Desenvolva, teste e integre sua fonte de dados baseada em REST API para assimilar dados em lote no Experience Platform usando as especificações de origem fáceis de configurar. Com o SDK de fontes, é possível: <ul><li>Configure uma nova fonte para o catálogo de Experience Platform.</li><li>Defina as especificações para a sua fonte, incluindo informações relacionadas aos tipos de autenticação suportados, programação e como os dados de recursos são buscados.</li><li>Crie uma documentação voltada para o usuário para sua nova fonte.</li></ul> Para obter mais informações, leia a documentação em [Fontes de autoatendimento (SDK em lote)](../../sources/sources-sdk/overview.md). |
| Disponibilidade geral [!DNL Google BigQuery] source | Use o [!DNL Google BigQuery] fonte para assimilar dados da sua [!DNL Google BigQuery] data warehouse para Experience Platform. Para obter mais informações, leia a documentação sobre o [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] fonte (Beta) | Use o [!DNL Teradata Vantage] origem para assimilar dados de ambientes híbridos de várias nuvens para o Experience Platform. Para obter mais informações, leia a documentação sobre o [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Suporte entre regiões para origem do Adobe Analytics | Agora é possível assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura). Os conjuntos de relatórios devem ser mapeados para a mesma organização da instância Sandbox do Experience Platform na qual a conexão de origem está sendo criada. Para obter mais informações, leia o guia sobre [criação de uma conexão de origem do Adobe Analytics na interface do usuário](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Suporte a API para assimilação sob demanda | Use a assimilação sob demanda para criar execuções de fluxo ad hoc para um determinado fluxo de dados com o [!DNL Flow Service] API. As execuções de fluxo criadas devem ser definidas para assimilação única. Para obter mais informações, leia o guia sobre [criação de uma execução de fluxo para assimilação sob demanda usando a API](../../sources/tutorials/api/on-demand-ingestion.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
