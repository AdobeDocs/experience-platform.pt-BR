---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de junho de 2023 para o Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b9d78cd726430b0c7690fdb814d0888aaad832f6
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 5%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 21 de junho de 2023**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Coleta de dados](#data-collection)
- [Serviço de query](#query-service)
- [Fontes](#sources)

## Coleta de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente do lado do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Extensão | [!DNL Google Cloud Platform] extensão de encaminhamento de eventos | A variável [[!DNL Google Cloud Platform]](../../tags/extensions/server/google-cloud-platform/overview.md) a extensão de encaminhamento de eventos permite encaminhar dados do evento para a Google para ativação via [!DNL Google Pub/Sub]. |
| Extensão | [!DNL Cloud connector for Google Analytics 4 (ga4)] extensão | A variável [[!DNL Cloud connector for Google Analytics 4 (ga4)]](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.109820.html) a extensão de encaminhamento de eventos permite rastrear a análise por meio da nova [!DNL Google Analytics 4 (ga4)] padrão. |
| Segredo | Segredo JWT do OAuth 2 | A variável [Segredo JWT do OAuth 2](../../tags/ui/event-forwarding/secrets.md) permite usar o Adobe e [!DNL Google] Tokens de serviço para suportar interações servidor-servidor no encaminhamento de eventos. |
| Tags e encaminhamento de eventos | Atribuição de usuário | A atribuição de usuário fornece dados essenciais de atividade em toda a [Tags](../../tags/home.md) e [Encaminhamento de evento](../../tags/ui/event-forwarding/overview.md) IU.<br><br>Os dados incluem quem fez quais alterações e em que momento. Esses dados estão visíveis na interface do usuário de Tags e Encaminhamento de eventos nas seguintes telas:<br><ul><li> Visão geral das propriedades</li><li> Extensões instaladas</li><li>Comparação e revisão de regras</li><li>Revisão de comparação dos Elementos de dados</li><li>Análise de comparação de extensões</li><li>Alterações no recurso da biblioteca</li><li>Última criação e publicação da biblioteca</li></ul> |

{style="table-layout:auto"}

Para saber mais sobre a coleta de dados, leia a [visão geral da coleção de dados](../../tags/home.md).

## Serviço de query {#query-service}

O Serviço de consulta permite usar o SQL padrão para consultar dados no data lake da Adobe Experience Platform. Você pode unir qualquer conjunto de dados do data lake e capturar os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou para assimilação no Perfil do cliente em tempo real. &#x200B;
**Recursos atualizados**
&#x200B; | Recurso | Descrição | | — | — | | &#x200B;Modelos integrados | O Serviço de consulta agora oferece suporte ao uso de modelos que fazem referência a outros modelos no seu SQL. Reduza a carga de trabalho e evite erros aproveitando modelos em linha em suas consultas. Você pode reutilizar instruções ou condições e fazer referência a modelos aninhados para obter maior flexibilidade no SQL. Não há limite no tamanho das consultas que podem ser armazenadas como modelos ou no número de modelos que podem ser referenciados da sua consulta original. Para obter mais informações, leia a [guia de modelo em linha](../../query-service/essential-concepts/inline-templates.md). | | Atualizações da interface de consulta programada | Gerencie todas as consultas agendadas de um local na interface do usuário com o [[!UICONTROL Guia Consultas programadas]](../../query-service/ui/monitor-queries.md#inline-actions). A variável [!UICONTROL Consultas programadas] A interface do usuário foi aprimorada com a adição de ações de consulta em linha e da nova coluna de status de consulta. As adições recentes incluem a capacidade de ativar, desativar e excluir um agendamento ou assinar alertas para execuções de consultas futuras diretamente da [!UICONTROL Consultas programadas] exibição. <p>![As ações em linha destacadas no [!UICONTROL Consultas programadas] exibição.](../../query-service/images/ui/monitor-queries/disable-inline.png "As ações em linha destacadas no [!UICONTROL Consultas programadas] exibição."){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}
&#x200B; Para obter mais informações sobre o Serviço de consulta, consulte [Visão geral do Serviço de consulta](../../query-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e permite estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte à exclusão de fluxos de dados de origem de classificação do Adobe Analytics | Agora é possível excluir fluxos de dados de origem que usam classificações do Adobe Analytics como origem. Em **[!UICONTROL Origens]** > **[!UICONTROL Fluxos de dados]**, selecione o fluxo de dados desejado e selecione excluir. Para obter mais informações, leia o guia em [criação de uma conexão de origem para dados de classificações do Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/classifications.md). |
| Suporte à filtragem para [!DNL Microsoft Dynamics] uso da API | Usar operadores lógicos e de comparação para filtrar dados no nível da linha para a variável [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) origem. Para obter mais informações, leia o guia em [filtragem de dados de uma origem usando a API](../../sources/tutorials/api/filter.md). |
| [!BADGE Beta]{type=Informative}[!DNL RainFocus] | Agora você pode usar o [!DNL RainFocus] integração de fontes para trazer dados de análise e gerenciamento de eventos de sua [!DNL RainFocus] conta para Experience Platform. Para obter mais informações, leia a [[!DNL RainFocus] visão geral da origem](../../sources/connectors/analytics/rainfocus.md). |
| Suporte para Adobe Commerce | Agora você pode usar a integração de fontes da Adobe Commerce para trazer dados de sua conta da Adobe Commerce para o Experience Platform. Para obter mais informações, leia a [Visão geral da origem do Adobe Commerce](../../sources/connectors/adobe-applications/commerce.md). |
| Suporte para [!DNL Mixpanel] | Agora você pode usar o [!DNL Mixpanel] integração de fontes para trazer dados do analytics de sua [!DNL Mixpanel] para Experience Platform usando APIs ou a interface do usuário. Para obter mais informações, leia a [[!DNL Mixpanel] visão geral da origem](../../sources/connectors/analytics/mixpanel.md). |
| Suporte para [!DNL Zendesk] | Agora você pode usar o [!DNL Zendesk] integração de fontes para trazer os dados de sucesso do cliente de sua [!DNL Zendesk] para Experience Platform usando APIs ou a interface do usuário. Para obter mais informações, leia a [[!DNL Zendesk] visão geral da origem](../../sources/connectors/customer-success/zendesk.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).
