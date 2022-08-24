---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 70bc3d8743dfa6c14e8a5c467775faa0c3c5a767
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 8%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de agosto de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Os serviços de IA/ML capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que analistas de marketing configurem modelos específicos às necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento em ciência de dados.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para privacidade | <li>O Attribution AI agora oferece suporte à definição de funções de usuário e políticas de acesso para gerenciar [permissões](../../../help/access-control/abac/ui/permissions.md) para recursos e objetos em um aplicativo de produto.</li><li>Os recursos do log de auditoria são registrados automaticamente conforme a atividade ocorre.</li><li>Através de [controle de acesso baseado em atributo](../../../help/access-control/abac/overview.md), os administradores podem controlar o acesso a objetos e/ou recursos específicos com base em determinados atributos, que podem ser metadados adicionados a um objeto, como rótulos. Os administradores também podem definir funções de usuário que tenham acesso apenas a campos e dados específicos que correspondam a esses campos.</li><li>[Higiene de dados](../../../help/hygiene/home.md) no Attribution AI permitem usar somente dados atualizados para treinamento adicional e pontuação. Da mesma forma, quando você solicita excluir dados, o Attribution AI se abstém de usar os dados excluídos.</li><li>O Attribution AI usa conjuntos de dados da plataforma. Para ajudar a facilitar a conformidade com o GDPR, você pode usar o Adobe Experience Platform Privacy Service para configurar protocolos para atender às solicitações do cliente para acessar e excluir seus dados no lago de dados, no Serviço de identidade e no Perfil do cliente em tempo real. Todos os dados são criptografados em trânsito e em repouso.</li> |

{style=&quot;table-layout:auto&quot;}

**Observação**: O Attribution AI não estará disponível para clientes do Healthcare Shield até o final do quarto trimestre de 2022.

Para obter mais informações sobre o Attribution AI, consulte o [Attribution AI](../../intelligent-services/attribution-ai/overview.md) visão geral.

### Customer AI

O Customer AI disponível no Real-time Customer Data Platform é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para privacidade | <li>O Customer AI agora oferece suporte à definição de funções de usuário e políticas de acesso para gerenciar [permissões](../../../help/access-control/abac/ui/permissions.md) para recursos e objetos em um aplicativo de produto.</li><li>Os recursos do log de auditoria são registrados automaticamente conforme a atividade ocorre.</li><li> Através de [controle de acesso baseado em atributo](../../access-control/abac/overview.md), os administradores podem controlar o acesso a objetos e/ou recursos específicos com base em determinados atributos. Esses atributos podem ser metadados adicionados a um objeto, como rótulos. Os administradores também podem definir funções de usuário que têm acesso somente a campos e dados específicos que correspondam a esses campos.</li><li>[Higiene de dados](../../../help/hygiene/home.md) no Customer AI permitem usar somente dados atualizados para treinamento e pontuação adicionais. Da mesma forma, quando você solicita a exclusão de dados, o Customer AI se abstém de usar os dados excluídos.</li><li>O Customer AI aproveita os conjuntos de dados da plataforma. Para ajudar a facilitar a conformidade com o GDPR, você pode usar o Adobe Experience Platform Privacy Service para configurar protocolos para atender às solicitações do cliente para acessar e excluir seus dados no lago de dados, no Serviço de identidade e no Perfil do cliente em tempo real. Todos os dados são criptografados em trânsito e em repouso.</li> |

{style=&quot;table-layout:auto&quot;}

**Observação**: O Customer AI não estará disponível para clientes do Healthcare Shield até o final do quarto trimestre de 2022.

Para obter mais informações sobre a API do cliente, consulte o [Customer AI](../../intelligent-services/customer-ai/overview.md) visão geral.

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] através da qual você pode visualizar informações importantes sobre os dados de sua organização, conforme capturado durante os instantâneos diários.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Dispositivo de ativações agendadas | O [!UICONTROL Ativações programadas] O widget fornece uma exibição em tabela dos destinos ativados mais recentemente. Para cada segmento, inclui o nome, a plataforma de destino e a data de início e término da ativação. Este widget permite descobrir rapidamente onde e quando o público-alvo está sendo ativado e torna as ativações duplicadas ou desnecessárias mais transparentes. Essas informações acumuladas também destacam onde quaisquer ativações foram deixadas de fora. |

Para obter mais informações sobre [!DNL Dashboards]consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para assimilar registros com avisos | A Preparação de dados agora localiza avisos (erros não críticos) nos campos e permitirá que o restante da linha seja assimilado. Todos os erros de transformação do mapeador agora são relatados como avisos e linhas que são parcialmente assimiladas são consideradas bem-sucedidas, com um aviso.  Também há suporte para monitoramento em registros com avisos e detalhes de diagnóstico. A assimilação parcial de registros com avisos está atualmente disponível apenas para dados de transmissão. Revise a documentação em [assimilação de registros com avisos](../../sources/tutorials/ui/monitor-streaming.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre [!DNL Data Prep], consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

<!--

**New or updated features**

| Feature | Description |
| ----------- | ----------- |
|  ||

{style="table-layout:auto"}

-->

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) é uma Sales Execution Platform com os dados de interação mais vendidos pelo comprador B2B no mundo e investimentos significativos em tecnologias de IA proprietárias para traduzir dados de vendas em inteligência. [!DNL Outreach] ajuda as organizações a automatizarem o envolvimento de vendas e agirem com a inteligência de receita para melhorar sua eficiência, previsibilidade e crescimento. |

{style=&quot;table-layout:auto&quot;}

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

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
| Limite rígido das políticas de mesclagem | A plataforma agora imporá um limite rígido de **cinco** mesclar políticas por sandbox. Se a sandbox tiver mais de cinco políticas de mesclagem, você **not** poder criar novas políticas de mesclagem até que a sandbox tenha menos de cinco políticas de mesclagem. |
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

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).