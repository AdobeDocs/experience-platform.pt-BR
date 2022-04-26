---
title: Notas de versão da Adobe Experience Platform, abril de 2022
description: As notas de versão de abril de 2022 para o Adobe Experience Platform.
source-git-commit: fe30444fb2d11c38433c73d88ee4c8e9a32bdff8
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de abril de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Fluxos de dados](#dataflows)
- [Experience Data Model (XDM)](#xdm)

## Fluxos de dados {#dataflows}

Na Platform, os dados são assimilados de várias fontes diferentes, analisados no sistema e ativados para uma grande variedade de destinos. A Platform facilita o processo de rastreamento desse fluxo de dados potencialmente não linear ao fornecer transparência com fluxos de dados.

Os fluxos de dados são uma representação de tarefas que movem dados pela plataforma. Esses fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, onde são utilizados pelo Serviço de identidade e pelo Perfil do cliente em tempo real antes de serem ativados para destinos.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Painel de segmentos | Agora você pode usar o painel de monitoramento para monitorar os fluxos de dados para segmentos. Para saber mais, leia o guia em [monitoramento de segmentos na interface do usuário](../../dataflows/ui/monitor-segments.md) |

Para obter informações mais gerais sobre fluxos de dados, consulte [visão geral dos fluxos de dados](../../dataflows/home.md). Para saber mais sobre a segmentação, consulte [visão geral da segmentação](../../segmentation/home.md).

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

