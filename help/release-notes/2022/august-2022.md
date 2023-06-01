---
title: Notas de versão da Adobe Experience Platform de agosto de 2022
description: As notas de versão de agosto de 2022 do Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: 7f5a1d8e50ff030b2abe04b5155f28b8c8b6fbf9
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 6%

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

Os serviços de IA/ML permitem que analistas e profissionais de marketing aproveitem o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam modelos específicos para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento especializado em ciência de dados.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para privacidade | <ul><li> O Attribution AI agora permite definir funções de usuário e políticas de acesso para gerenciar [permissões](../../../help/access-control/abac/ui/permissions.md) para recursos e objetos em um aplicativo do produto. </li><li>Os recursos de log de auditoria são registrados automaticamente conforme a atividade ocorre.</li><li> Até [controle de acesso baseado em atributos](../../access-control/abac/overview.md), os administradores podem controlar o acesso a objetos e/ou recursos específicos com base em determinados atributos, que podem ser metadados adicionados a um objeto, como rótulos. Os administradores também podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.</li><li>O Attribution AI aproveita conjuntos de dados da plataforma. Para dar suporte às solicitações de direitos do consumidor que uma marca pode receber, as marcas devem usar o Platform Privacy Service para enviar solicitações do consumidor de acesso e exclusão para remover seus dados no data lake, no Serviço de identidade e no Perfil do cliente em tempo real.  </li><li>Todos os conjuntos de dados usados para entrada/saída de modelos seguirão as diretrizes da plataforma. A Criptografia de dados da plataforma se aplica a dados inativos e em trânsito. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Nota**: o Attribution AI não estará disponível para os clientes existentes do Healthcare Shield até notificação posterior.

Para obter mais informações sobre o Attribution AI, consulte [Attribution AI](../../intelligent-services/attribution-ai/overview.md) visão geral.

### IA do cliente

A IA do cliente, disponível no Real-time Customer Data Platform, é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para privacidade | <ul><li> A IA do cliente agora permite definir funções de usuário e políticas de acesso para gerenciar o [permissões](../../../help/access-control/abac/ui/permissions.md) para recursos e objetos em um aplicativo do produto. </li><li>Os recursos de log de auditoria são registrados automaticamente conforme a atividade ocorre.</li><li> Até [controle de acesso baseado em atributos](../../access-control/abac/overview.md), os administradores podem controlar o acesso a objetos e/ou recursos específicos com base em determinados atributos. Esses atributos podem ser metadados adicionados a um objeto, como rótulos. Os administradores também podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.</li><li>A IA do cliente aproveita os conjuntos de dados da plataforma. Para dar suporte às solicitações de direitos do consumidor que uma marca pode receber, as marcas devem usar o Platform Privacy Service para enviar solicitações do consumidor de acesso e exclusão para remover seus dados no data lake, no Serviço de identidade e no Perfil do cliente em tempo real. </li><li>Todos os conjuntos de dados usados para entrada/saída de modelos seguirão as diretrizes da plataforma. A Criptografia de dados da plataforma se aplica a dados inativos e em trânsito. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**Nota**: a IA do cliente não estará disponível para clientes existentes do Healthcare Shield até aviso em contrário.

Para obter mais informações sobre a IA do cliente, consulte [IA do cliente](../../intelligent-services/customer-ai/overview.md) visão geral.

## [!DNL Dashboards] {#dashboards}

O Adobe Experience Platform fornece vários [!DNL dashboards] por meio do qual você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Widget de ativações programadas | A variável [!UICONTROL Ativações programadas] O widget fornece uma exibição tabulada dos destinos ativados mais recentemente. Para cada segmento, inclui o nome, a plataforma de destino e as datas de início e término da ativação. Esse widget permite descobrir onde e quando o público-alvo está sendo ativado e torna mais transparentes as ativações duplicadas ou desnecessárias. Essas informações acumuladas também destacam onde as ativações foram deixadas de fora. |

Para obter mais informações sobre [!DNL Dashboards], consulte o [[!DNL Dashboards] visão geral](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para assimilação de registros com avisos | O Preparo de dados agora localizará avisos (erros não críticos) nos campos e permitirá que o restante da linha seja assimilado. Todos os erros de transformação do mapeador agora são relatados como avisos, e as linhas que são parcialmente assimiladas são consideradas bem-sucedidas, com um aviso.  O monitoramento também é suportado em registros com avisos e detalhes de diagnóstico. Atualmente, a assimilação parcial de registros com avisos está disponível apenas para dados de transmissão. Revise a documentação em [assimilando registros com avisos](../../sources/tutorials/ui/monitor-streaming.md) para obter mais informações. |

{style="table-layout:auto"}

Para saber mais sobre [!DNL Data Prep], consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| (Beta) Suporte à personalização com base em atributos para destinos de personalização | Com a versão beta da personalização baseada em atributos, você verá dois novos cartões na [catálogo de destino](../../destinations/catalog/overview.md): <ul><li>**[!UICONTROL Adobe Target V2]**: no momento, esse conector está na versão beta e só está disponível para um número selecionado de clientes. Além da funcionalidade fornecida pela placa Adobe Target V1, o conector Target V2 adiciona uma [etapa de mapeamento](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) ao fluxo de trabalho de ativação, que permite mapear atributos de perfil para o Adobe Target, permitindo a personalização de mesma página e próxima página baseada em atributos.</li><li>**[!UICONTROL Personalização personalizada com atributos]**: no momento, esse conector está na versão beta e só está disponível para um número selecionado de clientes. Além da funcionalidade fornecida pelo **[!UICONTROL Personalização personalizada]**, o **[!UICONTROL Personalização personalizada com atributos]** O conector adiciona um [etapa de mapeamento](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) ao fluxo de trabalho de ativação, que permite mapear atributos de perfil para o destino de personalização personalizado, permitindo a personalização baseada em atributos de mesma página e próxima página.</li></ul> <br> Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, a variável **[!UICONTROL Personalização personalizada com atributos]** o destino exige que você use o [API do servidor de rede de borda](../../server-api/overview.md) para coleta de dados. Além disso, todas as chamadas à API do servidor devem ser feitas em um [contexto autenticado](../../server-api/authentication.md). |

{style="table-layout:auto"}

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) O é uma Plataforma de execução de vendas com a maioria dos dados de interação comprador-vendedor B2B no mundo e investimentos significativos em tecnologias de IA proprietárias para traduzir dados de vendas em inteligência. [!DNL Outreach] O ajuda as organizações a automatizar o engajamento de vendas e agir com base na inteligência de receita para melhorar a eficiência, a previsibilidade e o crescimento. |

{style="table-layout:auto"}

Para obter informações mais gerais sobre destinos, consulte o [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos das ações do cliente, definir públicos do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Classe | [[!UICONTROL Classe de entidade do AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Uma classe baseada em registros para criar esquemas de pesquisa para o Adobe Journey Optimizer. |
| Grupo de campos | [[!UICONTROL Objetos de trabalho do Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Um grupo de campos do invólucro que faz referência a todos os grupos de campos específicos de objetos de nível inferior do Adobe Workfront. |

{style="table-layout:auto"}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Grupo de campos | [[!UICONTROL Campos Comuns de Evento de Etapa do Journey Orchestration]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Duas novas propriedades foram adicionadas: `origTimeStamp` e `experienceID`. |
| Grupo de campos | [[!UICONTROL Detalhes da associação do segmento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Além de [!UICONTROL Perfil individual XDM], esse grupo de campos agora também pode ser usado em esquemas baseados na classe Conta de negócios XDM. |
| Grupo de campos | (Múltiplos) | Vários grupos de campos relacionados às atividades B2B do Marketo foram atualizados para o status estável. Consulte o seguinte [pull request](https://github.com/adobe/xdm/pull/1593/files) para obter detalhes. |
| Grupo de campos | (Múltiplos) | Vários grupos de campos relacionados ao clima foram atualizados para corrigir erros que estavam ocorrendo para `uvIndex` e `sunsetTime`. Consulte o seguinte [pull request](https://github.com/adobe/xdm/pull/1602/files) para obter detalhes. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Uma nova propriedade `productImageUrl` foi adicionado. |
| Tipo de dados | [[!UICONTROL Informações detalhadas de Dados de Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Uma nova propriedade `framesPerSecond` foi adicionado. |
| Tipo de dados | [[!UICONTROL Informações de detalhes da sessão]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | A `sdkVersion` foi renomeada como `appVersion`. `meta:enum` e `description` Os campos do também foram atualizados. |
| Tipos de dados e grupos de campos | (Múltiplos) | Vários tipos de dados de mídia e grupos de campos têm novos campos e descrições atualizadas. Consulte o seguinte [pull request](https://github.com/adobe/xdm/pull/1582/files) para obter detalhes. |
| (Todas) | (Múltiplos) | Todos os objetos de esquema que contêm um `enum` O campo agora também contém um campo correspondente `meta:enum` para indicar os valores de exibição para cada restrição. Consulte o seguinte [pull request](https://github.com/adobe/xdm/pull/1601/files) para obter detalhes. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema XDM](../../xdm/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ter uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. O Perfil permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Limite rígido das políticas de mesclagem | A Platform agora aplicará um limite rígido de **cinco** políticas de mesclagem por sandbox. Se sua sandbox tiver mais de cinco políticas de mesclagem, você **não** ser capaz de criar novas políticas de mesclagem até que a sandbox tenha menos de cinco políticas de mesclagem. |
| Limpeza de atributo de borda de perfil órfão | Para todas as organizações, o Serviço de perfil agora remove os atributos de borda restantes da região de atividade do usuário diariamente, fornecendo uma representação mais precisa dos perfis no sistema. Essa limpeza ocorre depois que todos os fragmentos de perfil de um determinado perfil são excluídos e deve afetar os perfis que estão sendo mesclados de conjuntos de dados em que `com_adobe_aep_profile_region_dataset` está marcado como `true`. Isso pode mostrar uma queda na métrica &quot;Público-alvo endereçável&quot; no painel de uso da licença e uma queda na métrica &quot;Contagem de perfis&quot; no painel Perfil, já que essas métricas incluíam fragmentos de atributos de borda restantes antes desta versão. |

{style="table-layout:auto"}

Para saber mais sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados de perfil, comece lendo o [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas na sua base de clientes. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para 4.000 segmentos | Todas as organizações com a Platform agora podem oferecer suporte a até 4.000 definições de segmento. Para obter mais informações sobre como essa alteração afeta as APIs de trabalho do segmento, leia a [manual de endpoint do trabalho de segmento](../../segmentation/api/segment-jobs.md) |

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [Visão geral da segmentação](../../segmentation/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de Fontes de autoatendimento (SDK em lote) | Desenvolva, teste e integre sua fonte de dados baseada em API REST para assimilar dados em lote no Experience Platform usando especificações de fonte fáceis de configurar. Com o SDK de origens, você pode: <ul><li>Configure uma nova fonte para o catálogo de Experience Platform.</li><li>Defina especificações para sua origem, incluindo informações relacionadas aos tipos de autenticação compatíveis, programação e como os dados de recursos são obtidos.</li><li>Crie documentação voltada para o usuário para sua nova fonte.</li></ul> Para obter mais informações, leia a documentação em [Fontes de autoatendimento (SDK em lote)](../../sources/sources-sdk/overview.md). |
| Disponibilidade geral de [!DNL Google BigQuery] origem | Use o [!DNL Google BigQuery] fonte para assimilar dados de seu [!DNL Google BigQuery] data warehouse para Experience Platform. Para obter mais informações, leia a documentação no [[!DNL Google BigQuery] origem](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] origem (Beta) | Use o [!DNL Teradata Vantage] fonte para assimilar dados de ambientes híbridos de várias nuvens para o Experience Platform. Para obter mais informações, leia a documentação no [[!DNL Teradata Vantage] origem](../../sources/connectors/databases/teradata-vantage.md). |
| Suporte entre regiões para origem no Adobe Analytics | Agora é possível assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura). Os conjuntos de relatórios devem ser mapeados para a mesma organização da instância de sandbox de Experience Platform em que a conexão de origem está sendo criada. Para obter mais informações, leia o guia em [criação de uma conexão de origem do Adobe Analytics na interface](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
