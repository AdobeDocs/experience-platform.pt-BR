---
title: Notas de versão da Adobe Experience Platform, abril de 2022
description: As notas de versão de abril de 2022 para o Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 6c2271e4c5be924dcd8c137cb40bef72e104c7e2
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 3%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de abril de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [Fluxos de dados](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [Real-time Customer Data Platform Edição B2B](#B2B)
- [Fontes](#sources)

## [!DNL Dashboards] {#dashboards}

A Platform fornece vários painéis através dos quais você pode visualizar informações importantes sobre os dados de sua organização, conforme capturado durante os instantâneos diários.

Os painéis fornecem opções de relatório pré-configuradas para os dados de sua organização e são incorporados diretamente no fluxo de trabalho do profissional de marketing na Platform. Esses painéis estão disponíveis sem a necessidade de suporte adicional de TI ou o tempo e esforço necessários para exportar e processar dados com o projeto e a implementação adicionais do data warehouse.

Os seguintes widgets estão disponíveis por meio da biblioteca de widgets em seus respectivos painéis. Consulte a documentação para obter mais informações sobre [como adicionar widgets através da biblioteca de widgets](../../dashboards/customize/widget-library.md).

| Recurso | Painel | Descrição |
| --------------------------------------------------------- | ------------- | ----------- |
| [!UICONTROL Tendência de adição de perfis] | Perfis | Esse widget usa um gráfico de linhas para ilustrar o número total de perfis mesclados que foram adicionados à Loja de perfis diariamente nos últimos 30 dias, 90 dias ou 12 meses. |
| [!UICONTROL Públicos-alvo mapeados para o status de destino] | Perfis | Esse widget exibe o número total de públicos-alvo mapeados e não mapeados em uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre seus totais. |
| [!UICONTROL Tamanho dos públicos-alvo] | Perfis | Este widget fornece uma tabela de duas colunas que lista até 20 segmentos e o número total de públicos-alvo contidos em cada segmento. A lista depende da política de mesclagem aplicada e ordenada de cima para baixo de acordo com o número total de públicos-alvo. |
| [!UICONTROL Tendência da contagem de perfis] | Perfis | Este widget usa um gráfico de linhas para ilustrar a tendência no número total de perfis contidos no sistema ao longo do tempo. Os dados podem ser visualizados por períodos de 30 dias, 90 dias e 12 meses. |
| [!UICONTROL Perfis de identidade únicos por identidade] | Perfis | Esse widget usa um gráfico de barras para ilustrar o número total de perfis identificados com apenas um único identificador exclusivo. O widget suporta até cinco das identidades mais comuns. |
| [!UICONTROL Status do destino] | Destinos | Esse widget exibe o número total de destinos ativados como uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre destinos ativados e desativados. |
| [!UICONTROL Destinos ativos por plataforma de destino] | Destinos | Esse widget usa uma tabela de duas colunas para mostrar uma lista de plataformas de destino ativas e o número total de destinos ativos para cada plataforma de destino. |
| [!UICONTROL Públicos-alvo ativados em todos os destinos] | Destinos | Este widget fornece o número total de públicos-alvo ativados em todos os destinos em uma única métrica. |
| [!UICONTROL Ordem de ativação do público-alvo] | Segmentos | Este widget fornece uma tabela de três colunas que lista o nome do destino, a plataforma e a data de ativação do público-alvo. |
| [!UICONTROL Tendência do tamanho do público-alvo] | Segmentos | Este widget fornece uma ilustração de gráfico de linha para o número total de perfis que atendem aos critérios de qualquer definição de segmento ao longo de períodos de 30 dias, 90 dias e 12 meses. |
| [!UICONTROL Tendência de alteração do tamanho do público-alvo] | Segmentos | Este widget fornece um gráfico de linhas que ilustra a diferença no número total de perfis que se qualificaram para um determinado segmento entre os instantâneos diários mais recentes. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. |
| [!UICONTROL Tendência do tamanho do público-alvo por identidade] | Segmentos | Este widget ilustra a tendência do tamanho do público-alvo para um segmento específico com base em um tipo de identidade selecionado. O período da análise de tendência pode ser visualizado em períodos de 30 dias, 90 dias e 12 meses. |

Consulte a documentação para obter mais informações sobre [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md)e [[!DNL Segments]](../../dashboards/guides/segments.md) painéis.

## Fluxos de dados {#dataflows}

Na Platform, os dados são assimilados de várias fontes diferentes, analisados no sistema e ativados para uma grande variedade de destinos. A Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear ao fornecer transparência com fluxos de dados.

Os fluxos de dados são uma representação de tarefas que movem dados pela plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, onde são utilizados pelo Serviço de identidade e pelo Perfil do cliente em tempo real antes de serem ativados para destinos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Painel de segmentos | Agora você pode usar o painel de monitoramento para monitorar os fluxos de dados para segmentos. Para saber mais, leia o guia em [monitoramento de segmentos na interface do usuário](../../dataflows/ui/monitor-segments.md) |

Para obter informações mais gerais sobre fluxos de dados, consulte [visão geral dos fluxos de dados](../../dataflows/home.md). Para saber mais sobre a segmentação, consulte [visão geral da segmentação](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para fonte Adobe Analytics | A fonte Adobe Analytics agora é compatível com os recursos de Preparação de dados, permitindo mapear os dados do conjunto de relatórios do Analytics para um esquema XDM de destino ao criar um fluxo de dados. Veja o tutorial em [criação de uma conexão de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obter mais informações. |
| Suporte para importar regras de mapeamento existentes | Agora é possível importar regras de mapeamento de um fluxo de dados existente para acelerar suas configurações de fluxo de dados e limitar erros. Veja o tutorial em [importação de regras de mapeamento existentes](../../data-prep/ui/mapping.md) para obter mais informações. |

Para obter mais informações sobre [!DNL Data Prep]consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ----------- | ----------- |
| Conectores avançados de destino empresarial | Três conectores de destino empresarial estão disponíveis: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)e [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> A disponibilidade geral dos conectores de destino da empresa inclui todos os recursos oferecidos anteriormente na fase Beta e muito mais: <ul><li>Novos recursos de autenticação, incluindo [Assinatura de Acesso Compartilhado nos Hubs de Eventos do Azure](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) e mais [tipos de autenticação](../../destinations/catalog/streaming/http-destination.md#authentication-information) (tokens do portador, OAuth 2) no destino da API HTTP;</li><li>[Preenchimento retroativo de dados de perfil históricos](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (envio de perfis históricos qualificados para o segmento quando ativados pela primeira vez);</li><li>Agora, as métricas de execução do fluxo de dados são compatíveis com esses destinos;</li><li>[Metadados de segmento adicionais](../../destinations/catalog/streaming/http-destination.md#destination-details) incluídos na carga de dados, incluindo nomes de segmentos e carimbos de data e hora do segmento;</li><li>Suporte para [endereços IP estáticos](/help/destinations/catalog/streaming/ip-address-allow-list.md) para clientes que precisam lista de permissões o Experience Platform.</li></ul> |
| Alertas no contexto para fluxos de dados de destino | Agora você pode [inscrever-se em alertas](../../destinations/ui/alerts.md) ao criar um fluxo de dados de destino, para receber mensagens de alerta relacionadas ao status, sucesso ou falha da execução do fluxo de dados. Você pode optar por receber alertas na interface do usuário do Experience Platform ou por email. |

<!--

### Release process for advanced enterprise destination connectors {#release-process-enterprise-destinations}

For the Amazon Kinesis, Azure Event Hubs, and HTTP API destinations, during the release process (starting April 27th), you will see both the former Beta destination card, as well as the new generally available (GA) destination card in the destinations catalog. Any dataflows configured by customers using the beta destinations will be migrated in the next couple of days to the GA version of the same destination. This migration should ultimately be completed by the end of day Friday April 29th. The Beta destinations will be continue to be visible during this short time-window and labeled as **Deprecated**.

If you have been utilizing these destinations in the Beta phase, please note the following:

- If have been previously in Beta with any of the 3 destinations, no action is needed. All dataflows set up as part of Beta will continue to be functional and will be migrated to the GA version.
- If you want to set up these destinations beginning April 27th, please do so with the new GA version of the destinations.
- The beta cards marked as deprecated will be removed once the release operation is complete, estimated by the end of day Friday April 29th. The Experience Platform engineering team is monitoring closely for a successful release operation.

-->

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| [!DNL Criteo] | Conecte e ative dados no [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) plataforma de publicidade. |
| [!DNL Sendgrid] | Conecte e ative dados no [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) plataforma para emails transacionais e de marketing. |

Para obter informações mais gerais sobre destinos, consulte [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Adicionar ou remover campos padrão individuais de um esquema | A interface do Editor de esquemas agora permite adicionar partes de grupos de campos padrão aos seus esquemas, fornecendo mais flexibilidade para os campos que você escolher incluir sem precisar criar recursos personalizados do zero.<br><br>Agora, também é possível definir campos personalizados ad-hoc diretamente na estrutura do schema e atribuí-los a um grupo de campos personalizado novo ou existente, sem precisar criar ou editar o grupo de campos antecipadamente.<br><br>Consulte o guia sobre [criar e editar esquemas na interface do usuário](../../xdm/ui/resources/schemas.md) para obter mais informações sobre esses novos workflows. |

{style=&quot;table-layout:auto&quot;}

**Novos componentes XDM**

| Tipo de componente | Nome | Descrição |
| --- | --- | --- |
| Schema global | [[!UICONTROL Solicitação de Operação de Higiene de Dados]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Captura os detalhes de uma solicitação de limpeza de dados para excluir ou modificar registros em um conjunto de dados ou sandbox especificado. |
| Descritor | [[!UICONTROL Descritor de granularidade da série de tempo]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indica a granularidade das séries de tempo e dos dados de resumo. Quando aplicado a um schema, o schema `timestamp` é o primeiro carimbo de data e hora em um período dessa granularidade. |
| Classe | [[!UICONTROL Métricas de resumo XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fornece métricas pré-resumidas com dimensões de agrupamento, como os resultados de um SQL SELECT com um GROUP BY. |
| Grupo de campos | [[!UICONTROL Mapa de resultados da avaliação das políticas de consentimento]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura o resultado da avaliação da política de consentimento para um indivíduo. |
| Grupo de campos | [[!UICONTROL Pesquisa do site]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura informações relacionadas à pesquisa do site, como consulta de pesquisa, filtragem e pedido. |
| Grupo de campos | [[!UICONTROL Mesclar leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Captura os detalhes de um evento em que dois ou mais leads são mesclados. |
| Grupo de campos | [[!UICONTROL Email enviado]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Captura os detalhes de um evento em que um email é enviado a um recipient. |
| Grupo de campos | [[!UICONTROL Compilação de campos]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Captura valores calculados pelo processo de identificação de um evento. |
| Grupo de campos | [[!UICONTROL Detalhe do Recipient Secundário para Auditoria]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Um grupo de campos Adobe Journey Optimizer que captura um detalhe de recipient secundário para uma auditoria. |
| Grupo de campos | [[!UICONTROL Detalhes da Relação de Pessoa da Conta Comercial XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Captura detalhes relacionados a um relacionamento conta-pessoa. |
| Grupo de campos | [[!UICONTROL Detalhes da Pessoa da Conta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Captura detalhes relacionados a um relacionamento conta-pessoa. |
| Tipo de dados | [[!UICONTROL Carrinho]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Captura informações sobre um carrinho de compras de comércio eletrônico. |
| Tipo de dados | [[!UICONTROL Envio]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Captura informações de envio para um ou mais produtos. |
| Tipo de dados | [[!UICONTROL Pesquisa do site]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Captura informações da atividade de pesquisa do site. |
| Extensão (Workfront) | [[!UICONTROL Atributos da Tarefa Operacional]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Captura detalhes relacionados a uma tarefa operacional. |
| Extensão (Workfront) | [[!UICONTROL Atributos do Portfolio de trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Captura detalhes relacionados a um portfólio de trabalho. |
| Extensão (Workfront) | [[!UICONTROL Atributos do programa de trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Captura detalhes relacionados a um programa de trabalho. |
| Extensão (Workfront) | [[!UICONTROL Atributos do projeto de trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Captura detalhes relacionados a um projeto de trabalho. |

{style=&quot;table-layout:auto&quot;}

**Componentes XDM atualizados**

| Tipo de componente | Nome | Atualizar descrição |
| --- | --- | --- |
| Schema global | [[!UICONTROL Destinos ]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Novos valores de enum para `destinationCategory`. |
| Descritor | [[!UICONTROL Descritor de nome amigável]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Adição de suporte para remoção de valores sugeridos (`meta:enum`) que não são necessárias de campos padrão. |
| Grupo de campos | [[!UICONTROL Processo de logon do usuário]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` campo adicionado. |
| Tipo de dados | [[!UICONTROL Comércio]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Vários campos relacionados ao carrinho foram adicionados. |
| Tipo de dados | [[!UICONTROL Item da lista de produtos]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Novos campos adicionados para opções selecionadas e valor do desconto. |
| Extensão (Serviços inteligentes) | [[!UICONTROL Otimização do tempo de envio da Inteligência Services JourneyAI]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Otimizar o formato de armazenamento para pontuações de tempo de envio. |
| Extensão (Workfront) | [[!UICONTROL Evento Workfront Change]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Vários campos foram substituídos por um `workfront:customData` campo para campos de formulário personalizados. |
| Extensão (Workfront) | [[!UICONTROL Atributos da Tarefa de Trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Vários campos foram adicionados. |
| Extensão (Workfront) | [[!UICONTROL Objeto de Trabalho]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Novos campos para o tipo de objeto pai e campos de formulário personalizados. |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre o XDM na Platform, consulte o [Visão geral do sistema XDM](../../xdm/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de experiência em ciência de dados.

O Attribution AI e o Customer AI permitem que os clientes configurem modelos avançados de AI/ML para atribuição de marketing e propensão do cliente. O recurso Conjunto de dados múltiplo ajuda os clientes a trazer vários conjuntos de dados no momento da configuração do modelo, sem a necessidade de compilar e preparar os dados antecipadamente.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para vários conjuntos de dados | O recurso Conjunto de vários dados agora é compatível com todos os conjuntos de dados de eventos de experiência, bem como com a seleção do Mapa de identidade como uma identidade. Os clientes podem selecionar o Mapa de identidade e quaisquer IDs associadas, desde que haja um namespace de identidade comum em todos os conjuntos de dados. O Attribution AI é compatível com os seguintes esquemas: Adobe Analytics, Evento de experiência, Evento de experiência do consumidor. O Customer AI é compatível com todos esses esquemas e com o esquema Adobe Audience Manager. Para obter mais informações sobre o suporte a vários conjuntos de dados no Attribution AI e no Customer AI, consulte [Guia do usuário do Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) e [Guia do usuário de IA do cliente](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Novas métricas de avaliação de modelo no Customer AI | Os novos gráficos de Ganhos no Customer AI permitem que os profissionais de marketing determinem o tamanho do grupo para direcionar com base em seus objetivos de orçamento e ROI. Os novos gráficos de incentivo medem a qualidade do modelo, fornecendo melhor visibilidade sobre o aumento que obteriam sobre o direcionamento aleatório. Para obter mais informações, consulte o [descubra insights com a Customer AI](../../intelligent-services/customer-ai/user-guide/discover-insights.md) documento. |

Para obter mais informações sobre [!DNL Intelligent Services]consulte o [[!DNL Intelligent Services] visão geral](../../intelligent-services/home.md).

## Real-time Customer Data Platform Edição B2B {#B2B}

Baseada na Real-time Customer Data Platform (CDP em tempo real), a CDP B2B Edition em tempo real é projetada especificamente para profissionais de marketing que operam em um modelo de serviço de negócios para empresas. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem com precisão públicos-alvo específicos e os envolvam em todos os canais disponíveis.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para `isDeleted` funcionalidade | Todos [!DNL Marketo] conjuntos de dados, exceto `Activities` agora oferecem suporte para `isDeleted` mapeamento. O novo mapeamento é adicionado automaticamente aos seus fluxos de dados B2B existentes. Você pode usar o `isDeleted` mapeamento para filtrar registros que foram excluídos para que seus dados no [!DNL Data Lake] O é consistente com os dados de origem. Consulte a [[!DNL Marketo] guia de campos de mapeamento](../../sources/connectors/adobe-applications/mapping/marketo.md) para obter mais informações sobre `isDeleted`. |

Para saber mais sobre o Real-time Customer Data Platform B2B Edition, consulte o [Visão geral do B2B](../../rtcdp/b2b-overview.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para [!DNL OneTrust Integration] | Agora você pode usar o [!DNL OneTrust Integration] fonte para assimilar dados de consentimento e preferências da [!DNL OneTrust] para a Platform. Consulte a documentação em [criar um [!DNL OneTrust Integration] conexão de origem](../../sources/connectors/consent-and-preferences/onetrust.md) para obter mais informações. |
| Suporte para [!DNL Square] | Agora você pode usar o [!DNL Square] origem para assimilar dados de pagamentos do seu [!DNL Square] para a Platform. |
| Suporte para excluir fluxos de dados de atributos do cliente | Agora é possível excluir os fluxos de dados criados com o conector de origem dos Atributos do cliente. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
