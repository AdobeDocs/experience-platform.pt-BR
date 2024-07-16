---
title: Notas de versão de abril de 2022 da Adobe Experience Platform
description: As notas de versão de abril de 2022 da Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2670'
ht-degree: 19%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 27 de abril de 2022**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Fluxos de dados](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [Fontes](#sources)

## [!DNL Dashboards] {#dashboards}

A Platform fornece vários painéis por meio dos quais você pode visualizar informações importantes sobre os dados de sua organização, conforme capturados durante instantâneos diários.

Os painéis fornecem opções de relatório pré-configuradas para os dados de sua organização e são criados diretamente no fluxo de trabalho do profissional de marketing na Platform. Esses painéis estão disponíveis sem a necessidade de suporte de TI adicional ou o tempo e esforço que seriam necessários para exportar e processar dados com projeto e implementação adicionais de data warehouse.

Os seguintes widgets estão disponíveis na Biblioteca de widgets nos respectivos painéis. Consulte a documentação para obter mais informações sobre [como adicionar widgets por meio da Biblioteca de widgets](../../dashboards/customize/widget-library.md).

**Novos widgets**

| Widget | Painel | Descrição |
| ------ | --------- | ----------- |
| [!UICONTROL Tendência de perfis adicionados] | Perfis | Este widget usa um gráfico de linhas para ilustrar o número total de perfis mesclados que foram adicionados ao armazenamento Perfil diariamente nos últimos 30 dias, 90 dias ou 12 meses. |
| [!UICONTROL Públicos mapeados para o status de destino] | Perfis | Este widget exibe o número total de públicos mapeados e não mapeados em uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre seus totais. |
| [!UICONTROL Tamanho do público] | Perfis | Esse widget fornece uma tabela de duas colunas que lista até 20 segmentos e o número total de públicos-alvo contidos em cada segmento. A lista depende da política de mesclagem aplicada e ordenada de cima para baixo de acordo com o número total de públicos-alvo. |
| [!UICONTROL Tendência de contagem de perfis] | Perfis | Esse widget usa um gráfico de linhas para ilustrar a tendência do número total de perfis contidos no sistema ao longo do tempo. Os dados podem ser visualizados por períodos de 30 dias, 90 dias e 12 meses. |
| [!UICONTROL Perfis de identidade únicos por identidade] | Perfis | Este widget usa um gráfico de barras para ilustrar o número total de perfis identificados com apenas um identificador exclusivo. O widget suporta até cinco das identidades mais comuns. |
| [!UICONTROL Status do destino] | Destinos | Este widget exibe o número total de destinos ativados como uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre destinos ativados e desativados. |
| [!UICONTROL Destinos ativos por plataforma de destino] | Destinos | Este widget usa uma tabela de duas colunas para mostrar uma lista de plataformas de destino ativas e o número total de destinos ativos para cada plataforma de destino. |
| [!UICONTROL Públicos ativados em todos os destinos] | Destinos | Este widget fornece o número total de públicos ativados em todos os destinos em uma única métrica. |
| [!UICONTROL Ordem de ativação de público-alvo] | Segmentos | Esse widget fornece uma tabela de três colunas que lista o nome do destino, a plataforma e a data de ativação do público-alvo. |
| [!UICONTROL Tendência de tamanho do público-alvo] | Segmentos | Este widget fornece uma ilustração de gráfico de linhas para o número total de perfis que atendem aos critérios de qualquer definição de segmento durante períodos de 30 dias, 90 dias e 12 meses. |
| [!UICONTROL Tendência de alteração de tamanho do público-alvo] | Segmentos | Este widget fornece uma ilustração de gráfico de linhas da diferença no número total de perfis qualificados para um determinado segmento entre os instantâneos diários mais recentes. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. |
| [!UICONTROL Tendência de tamanho de público por identidade] | Segmentos | Este widget ilustra a tendência do tamanho do público-alvo para um segmento específico com base em um tipo de identidade selecionado. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. |

**Novos recursos** {#new-features}

| Recurso | Painel | Descrição |
| ------- | --------- | ----------- |
| Limpeza de associação de segmento de perfil órfão | Perfis e uso de licença | O Serviço de perfil agora remove os membros restantes do segmento diariamente, para fornecer uma representação mais precisa dos perfis no sistema. Essa limpeza ocorre depois que todos os fragmentos de perfil de um determinado perfil são excluídos. Isso pode mostrar uma queda na métrica &quot;Público-alvo endereçável&quot; no painel de uso da licença e uma queda na métrica &quot;Contagem de perfis&quot; no painel Perfil, já que essas métricas incluíam fragmentos de segmentos restantes antes desta versão. |

{style="table-layout:auto"}

Consulte a documentação para obter mais informações sobre os painéis do [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md) e [[!DNL Segments]](../../dashboards/guides/audiences.md).

## Fluxos de dados {#dataflows}

Na Platform, os dados são assimilados de várias fontes diferentes, analisados no sistema e ativados para uma grande variedade de destinos. O Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear, fornecendo transparência aos fluxos de dados.

Os fluxos de dados são uma representação de trabalhos que movem dados pela Plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, em que são utilizados pelo Serviço de identidade e pelo Perfil do cliente em tempo real antes de serem ativados para destinos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Painel de segmentos | Agora você pode usar o painel de monitoramento para monitorar fluxos de dados para segmentos. Para saber mais, leia o manual sobre [segmentos de monitoramento na interface](../../dataflows/ui/monitor-audiences.md) |

Para obter mais informações sobre fluxos de dados, consulte a [visão geral sobre fluxos de dados](../../dataflows/home.md). Para saber mais sobre segmentação, consulte a [visão geral sobre segmentação](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para origem no Adobe Analytics | A origem do Adobe Analytics agora é compatível com os recursos de Preparo de dados, permitindo mapear os dados do conjunto de relatórios do Analytics para um esquema XDM de destino ao criar um fluxo de dados. Consulte o tutorial sobre [criação de uma conexão de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obter mais informações. |
| Suporte para importar regras de mapeamento existentes | Agora é possível importar regras de mapeamento de um fluxo de dados existente para acelerar suas configurações de fluxo de dados e limitar erros. Consulte o tutorial sobre [importação de regras de mapeamento existentes](../../data-prep/ui/mapping.md) para obter mais informações. |

Para obter mais informações sobre [!DNL Data Prep], consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Conectores de destino avançados empresariais | Agora, três conectores de destino de empresa estão disponíveis para o público geral: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md) e [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> A disponibilidade geral dos conectores de destino corporativos inclui todos os recursos oferecidos anteriormente na fase do Beta e muito mais: <ul><li>Novos recursos de autenticação, incluindo [Assinatura de Acesso Compartilhado nos Hubs de Eventos do Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) e mais [tipos de autenticação](../../destinations/catalog/streaming/http-destination.md#authentication-information) (tokens de portador, OAuth 2) no destino da API HTTP;</li><li>[Preenchendo retroativamente os dados do perfil histórico](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (enviando perfis históricos qualificados para o segmento quando ativados pela primeira vez);</li><li>As métricas de execuções de fluxo de dados agora são compatíveis com esses destinos;</li><li>[Metadados de segmento adicionais](../../destinations/catalog/streaming/http-destination.md#destination-details) incluídos na carga de dados, incluindo nomes de segmentos e carimbos de data/hora de segmentos;</li><li>Incluir na lista de permissões Suporte para [endereços IP estáticos](/help/destinations/catalog/streaming/ip-address-allow-list.md) para clientes que precisam pesquisar Experience Platform.</li></ul> |
| Alertas em contexto para fluxos de dados de destino | Agora você pode [assinar alertas](../../destinations/ui/alerts.md) ao criar um fluxo de dados de destino, para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo de dados. Você pode optar por receber alertas na interface do usuário do Experience Platform ou por email. |

### Processo de liberação para conectores de destino corporativo avançados {#release-process-enterprise-destinations}

Para os destinos do Amazon Kinesis, dos Hubs de eventos do Azure e da API HTTP, durante o processo de lançamento (a partir de 27 de abril), você verá a antiga placa de destino do Beta, bem como a nova placa de destino geralmente disponível (GA) no catálogo de destinos. Quaisquer fluxos de dados configurados por clientes que usam os destinos beta serão migrados nos próximos dias para a versão do GA do mesmo destino. Essa migração deve ser concluída até o final do dia sexta-feira, 29 de abril. Os destinos do Beta continuarão visíveis durante esse curto período de tempo e serão rotulados como **Obsoletos**.

Se você estiver utilizando esses destinos na fase Beta, observe o seguinte:

- Se tiver estado anteriormente no Beta com qualquer um dos três destinos, nenhuma ação será necessária. Todos os fluxos de dados configurados como parte do Beta continuarão funcionando e serão migrados para a versão do GA.
- Se você quiser configurar esses destinos a partir de 27 de abril, faça isso com a nova versão GA dos destinos.
- Os cartões beta marcados como obsoletos serão removidos assim que a operação de lançamento estiver concluída, estimada para o final do dia sexta-feira, 29 de abril. A equipe de engenharia de Experience Platform está monitorando atentamente uma operação de lançamento bem-sucedida.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [!DNL Criteo] | Conecte e ative dados à plataforma de publicidade [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md). |
| [!DNL Sendgrid] | Conecte e ative dados à plataforma [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) para emails transacionais e de marketing. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Adicionar ou remover campos padrão individuais de um esquema | A interface do Editor de esquemas agora permite adicionar partes de grupos de campos padrão aos esquemas, fornecendo mais flexibilidade para os campos que você escolhe incluir, sem precisar criar recursos personalizados do zero.<br><br>Agora você também pode definir campos personalizados ad hoc diretamente na estrutura do esquema e atribuí-los a um grupo de campos personalizado novo ou existente sem precisar criar ou editar o grupo de campos antecipadamente.<br><br>Consulte o manual sobre [criação e edição de esquemas na interface](../../xdm/ui/resources/schemas.md) para obter mais informações sobre esses novos fluxos de trabalho. |

{style="table-layout:auto"}

**Novos componentes do XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Solicitação de operação de limpeza de dados]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Captura os detalhes de uma solicitação de limpeza de dados para excluir ou modificar registros em um conjunto de dados ou sandbox especificado. |
| Descritor | [[!UICONTROL Descritor de Granularidade de Série Temporal]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica a granularidade da série temporal e dos dados de resumo. Quando aplicado a um esquema, o campo `timestamp` do esquema é o primeiro carimbo de data e hora em um período dessa granularidade. |
| Classe | [[!UICONTROL Métricas de resumo XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fornece métricas pré-resumidas com dimensões de agrupamento, como os resultados de um SQL SELECT com um GROUP BY. |
| Grupo de campos | [[!UICONTROL Mapa de resultados da avaliação de políticas de consentimento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Registra o resultado da avaliação da política de consentimento de um indivíduo. |
| Grupo de campos | [[!UICONTROL Pesquisa de sites]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura informações relacionadas à pesquisa do site, como consulta de pesquisa, filtragem e ordenação. |
| Grupo de campos | [[!UICONTROL Mesclar clientes em potencial]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Registra os detalhes de um evento em que dois ou mais leads são mesclados. |
| Grupo de campos | [[!UICONTROL Email Enviado]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Registra os detalhes de um evento em que um email é enviado a um recipient. |
| Grupo de campos | [[!UICONTROL Campos de Costura]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Captura valores calculados por meio do processo de identificação de um evento. |
| Grupo de campos | [[!UICONTROL Detalhes do Destinatário Secundário para Auditoria]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Um grupo de campos do Adobe Journey Optimizer que captura detalhes secundários de um recipient para uma auditoria. |
| Grupo de campos | [[!UICONTROL Detalhes de relação pessoal da conta comercial XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Registra detalhes relacionados a um relacionamento conta-pessoa. |
| Grupo de campos | [[!UICONTROL Detalhes de Pessoa da Conta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Registra detalhes relacionados a um relacionamento conta-pessoa. |
| Tipo de dados | [[!UICONTROL Carrinho]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Captura informações sobre um carrinho de compras de comércio eletrônico. |
| Tipo de dados | [[!UICONTROL Envio]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Registra informações de remessa de um ou mais produtos. |
| Tipo de dados | [[!UICONTROL Pesquisa de sites]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Registra informações sobre a atividade de pesquisa no site. |
| Extensão (Workfront) | [[!UICONTROL Atributos da Tarefa Operacional]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Captura detalhes relacionados a uma tarefa operacional. |
| Extensão (Workfront) | [[!UICONTROL Atributos do Portfolio de trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Captura detalhes relacionados a um portfólio de trabalho. |
| Extensão (Workfront) | [[!UICONTROL Atributos do programa de trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Captura detalhes relacionados a um programa de trabalho. |
| Extensão (Workfront) | [[!UICONTROL Atributos do Projeto de Trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Captura detalhes relacionados a um projeto de trabalho. |

{style="table-layout:auto"}

**Componentes de XDM atualizados**

| Tipo de componente | Nome | Atualizar descrição |
| --- | --- | --- |
| Esquema global | [[!UICONTROL Destinos]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Novos valores de enumeração para `destinationCategory`. |
| Descritor | [[!UICONTROL Descritor de nome amigável]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Adição de suporte para remoção de valores sugeridos (`meta:enum`) que não são necessários de campos padrão. |
| Grupo de campos | [[!UICONTROL Processo de Logon do Usuário]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` campo adicionado. |
| Tipo de dados | [[!UICONTROL Comércio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Vários campos relacionados ao carrinho foram adicionados. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Novos campos adicionados para opções selecionadas e valor do desconto. |
| Extensão (Serviços inteligentes) | [[!UICONTROL Otimização do Tempo de Envio de JourneyAI dos Serviços Inteligentes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Otimizar formato de armazenamento para pontuações de tempo de envio. |
| Extensão (Workfront) | [[!UICONTROL Evento de alteração do Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Vários campos substituídos por um campo `workfront:customData` para campos de formulário personalizados. |
| Extensão (Workfront) | [[!UICONTROL Atributos da Tarefa de Trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Vários campos adicionados. |
| Extensão (Workfront) | [[!UICONTROL Objeto de trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Novos campos para o tipo de objeto pai e campos de formulário personalizados. |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema de XDM](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

Os serviços de IA/ML permitem que analistas e profissionais de marketing aproveitem o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing estabeleçam previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial, sem a necessidade de uma especialização em ciência de dados.

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ela pode ser usada por comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para vários conjuntos de dados | O recurso Conjunto de dados múltiplo agora é compatível com todos os conjuntos de dados de Evento de experiência, bem como com a seleção do Mapa de identidade como uma identidade. Os clientes podem selecionar o Mapa de identidade e qualquer ID associada, desde que haja um namespace de identidade comum entre os conjuntos de dados. O Attribution AI é compatível com os seguintes esquemas: Adobe Analytics, Evento de experiência, Evento de experiência do consumidor. Para obter mais informações sobre o suporte a vários conjuntos de dados no Attribution AI, consulte o [guia do usuário do Attribution AI](../../intelligent-services/attribution-ai/user-guide.md). |

Para obter mais informações sobre [!DNL Intelligent Services], consulte a [[!DNL Intelligent Services] visão geral](../../intelligent-services/home.md).

### IA do cliente

A IA do cliente, disponível no Real-time Customer Data Platform, é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para vários conjuntos de dados | O recurso Conjunto de dados múltiplo agora é compatível com todos os conjuntos de dados de Evento de experiência, bem como com a seleção do Mapa de identidade como uma identidade. Os clientes podem selecionar o Mapa de identidade e qualquer ID associada, desde que haja um namespace de identidade comum entre os conjuntos de dados. A IA do cliente é compatível com os seguintes esquemas: Adobe Analytics, Evento de experiência, Evento de experiência do consumidor e esquema do Adobe Audience Manager. Para obter mais informações sobre o suporte a vários conjuntos de dados na IA do cliente, consulte o [Guia do usuário da IA do cliente](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Novas métricas de avaliação de modelo na IA do cliente | Os novos gráficos de ganhos na IA do cliente permitem que os profissionais de marketing determinem o tamanho do grupo a ser direcionado com base em seus orçamentos e metas de ROI. Novos gráficos de aumento medem a qualidade do modelo, fornecendo melhor visibilidade sobre o aumento que obteriam em relação à definição de metas aleatórias. Para obter mais informações, consulte o documento [descobrir insights com a IA do cliente](../../intelligent-services/customer-ai/user-guide/discover-insights.md). |

Para obter mais informações sobre [!DNL Intelligent Services], consulte a [[!DNL Intelligent Services] visão geral](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B Edition {#B2B}

Criada com base na Real-time Customer Data Platform (Real-Time CDP), a Real-Time CDP B2B Edition foi desenvolvida especificamente para profissionais de marketing que operam em um modelo de serviço B2B. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para a funcionalidade `isDeleted` | Todos os conjuntos de dados [!DNL Marketo], exceto `Activities`, agora oferecem suporte ao mapeamento `isDeleted`. O novo mapeamento é adicionado automaticamente aos fluxos de dados B2B existentes. Você pode usar o mapeamento `isDeleted` para filtrar registros que foram excluídos, de forma que os dados no [!DNL Data Lake] sejam consistentes com os dados de origem. Consulte o [[!DNL Marketo] guia de campos de mapeamento](../../sources/connectors/adobe-applications/mapping/marketo.md) para obter mais informações sobre `isDeleted`. |

Para saber mais sobre o Real-time Customer Data Platform B2B Edition, consulte a [Visão geral B2B](../../rtcdp/b2b-overview.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Compatibilidade com o [!DNL OneTrust Integration] | Agora você pode usar a fonte [!DNL OneTrust Integration] para assimilar dados de consentimento e preferências da sua conta [!DNL OneTrust] na Platform. Consulte a documentação sobre [criação de uma [!DNL OneTrust Integration] conexão de origem](../../sources/connectors/consent-and-preferences/onetrust.md) para obter mais informações. |
| Compatibilidade com o [!DNL Square] | Agora você pode usar a fonte [!DNL Square] para assimilar dados de pagamentos da sua conta [!DNL Square] na Platform. |
| Suporte para exclusão de fluxos de dados de atributos do cliente | Agora é possível excluir fluxos de dados criados com o conector de origem de Atributos do cliente. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
