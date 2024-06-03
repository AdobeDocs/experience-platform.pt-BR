---
title: Grupo de campos de esquema de extensão completa do Adobe Analytics ExperienceEvent
description: Saiba mais sobre o grupo de campos de esquema Extensão completa do Adobe Analytics ExperienceEvent.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: 5eb15a7dfff7e6d8ba815ae4f89142ba50166620
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 5%

---

# [!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent] grupo de campos de esquema

[!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), que captura métricas comuns coletadas pelo Adobe Analytics.

Este documento descreve a estrutura e o caso de uso do grupo de campos de extensão do Analytics.

>[!NOTE]
>
>Devido ao tamanho e ao número de elementos repetidos neste grupo de campos, muitos dos campos mostrados neste guia foram recolhidos para economizar espaço. Para explorar a estrutura completa desse grupo de campos, você pode [pesquisar na interface do Platform](../../ui/explore.md) ou exiba o esquema completo na caixa [repositório XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Estrutura do grupo de campos

O grupo de campos fornece um único `_experience` objeto a um esquema, que contém um único `analytics` objeto.

![Campos de nível superior do grupo de campos do Analytics](../../images/field-groups/analytics-full-extension/full-schema.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `customDimensions` | Objeto | Captura dimensões personalizadas que são rastreadas pelo Analytics. Consulte a [subseção abaixo](#custom-dimensions) para obter mais informações sobre o conteúdo desse objeto. |
| `endUser` | Objeto | Registra os detalhes de interação da Web para o usuário final que acionou o evento. Consulte a [subseção abaixo](#end-user) para obter mais informações sobre o conteúdo desse objeto. |
| `environment` | Objeto | Registra informações sobre o navegador e o sistema operacional que acionou o evento. Consulte a [subseção abaixo](#environment) para obter mais informações sobre o conteúdo desse objeto. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Objeto | O grupo de campos fornece campos de objeto para capturar até 1000 eventos personalizados. Consulte a [subseção abaixo](#events) para obter mais informações sobre esses campos. |
| `session` | Objeto | Registra informações sobre a sessão que acionou o evento. Consulte a [subseção abaixo](#session) para obter mais informações sobre o conteúdo desse objeto. |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` captura personalizado [dimensões](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html) que são rastreados pelo Analytics.

![campo customDimensions](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `eVars` | Objeto | Um objeto que captura até 250 variáveis de conversão ([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=pt-BR)). As propriedades desse objeto são digitadas `eVar1` para `eVar250` e aceitam somente strings para seus tipos de dados. |
| `hierarchies` | Objeto | Um objeto que captura até cinco variáveis de hierarquia personalizadas ([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=pt-BR)). As propriedades desse objeto são digitadas `hier1` para `hier5`, que são objetos com as seguintes subpropriedades:<ul><li>`delimiter`: o delimitador original usado para gerar a lista fornecida em `values`.</li><li>`values`: uma lista delimitada de nomes de nível de hierarquia, representados como uma string.</li></ul> |
| `listProps` | Objeto | Um objeto que captura até 75 [propriedades de lista](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). As propriedades desse objeto são digitadas `prop1` para `prop75`, que são objetos com as seguintes subpropriedades:<ul><li>`delimiter`: o delimitador original usado para gerar a lista fornecida em `values`.</li><li>`values`: uma lista delimitada de valores para a prop, representada como uma string.</li></ul> |
| `lists` | Objeto | Um objeto que captura até três [listas](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). As propriedades desse objeto são digitadas `list1` para `list3`. Cada uma dessas propriedades contém uma única `list` matriz de [[!UICONTROL Par de valores da chave]](../../data-types/key-value-pair.md) tipos de dados. |
| `props` | Objeto | Um objeto que captura até 75 [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=pt-BR). As propriedades desse objeto são digitadas `prop1` para `prop75` e aceitam somente strings para seus tipos de dados. |
| `postalCode` | String | Um CEP ou código postal fornecido pelo cliente. |
| `stateProvince` | String | Um estado ou província fornecido pelo cliente. |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` captura os detalhes de interação na web para o usuário final que acionou o evento.

![campo endUser](../../images/field-groups/analytics-full-extension/endUser.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Informações da Web]](../../data-types/web-information.md) | As informações relacionadas à página da Web, link e referenciador do primeiro Evento de experiência para este usuário final. |
| `firstTimestamp` | Número inteiro | Um carimbo de data e hora Unix para o primeiro ExperienceEvent para esse usuário final. |

## `environment` {#environment}

`environment` captura informações sobre o navegador e o sistema operacional que acionaram o evento.

![campo de ambiente](../../images/field-groups/analytics-full-extension/environment.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `browserIDStr` | String | O identificador Adobe Analytics do navegador usado (conhecido como [dimensão tipo de navegador](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | String | O identificador Adobe Analytics do sistema operacional usado (conhecido como [dimensão de tipo de sistema operacional](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Campos de evento personalizados {#events}

O grupo de campos de extensão do Analytics fornece dez campos de objeto que capturam até 100 [métricas de evento personalizadas](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) cada, para um total de 1000 para o grupo de campos.

Cada objeto de evento de nível superior contém os objetos de evento individuais para seu respectivo intervalo. Por exemplo, `event101to200` contém os eventos chaveados de `event101` para `event200`.

Cada objeto de evento usa o [[!UICONTROL Medir]](../../data-types/measure.md) tipo de dados, que fornece um identificador exclusivo e um valor quantificável.

![Campo de evento personalizado](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` captura informações sobre a sessão que acionou o evento.

![campo de sessão](../../images/field-groups/analytics-full-extension/session.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `search` | [[!UICONTROL Pesquisa]](../../data-types/search.md) | Captura informações relacionadas à pesquisa na web ou celular para a entrada da sessão. |
| `web` | [[!UICONTROL Informações da Web]](../../data-types/web-information.md) | Captura informações sobre cliques em links, detalhes da página da Web, informações de referenciador e detalhes do navegador para a entrada da sessão. |
| `depth` | Número inteiro | A profundidade da sessão atual (como o número de página) do usuário final. |
| `num` | Número inteiro | O número da sessão atual do usuário final. |
| `timestamp` | Número inteiro | Um carimbo de data e hora Unix para a entrada da sessão. |

## Próximas etapas

Este documento abordou a estrutura e o caso de uso do grupo de campos de extensão do Analytics. Para obter mais detalhes sobre o próprio grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Se você estiver usando esse grupo de campos para coletar dados do Analytics usando o SDK da Web da Adobe Experience Platform, consulte o guia em [configurar um fluxo de dados](../../../datastreams/overview.md) para saber como mapear dados para o XDM no lado do servidor.
