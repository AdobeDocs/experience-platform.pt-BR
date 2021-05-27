---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, colocar contexto, placeContext, tipo de dados, tipo de dados, tipo de dados; tipo de dados;
solution: Experience Platform
title: Inserir tipo de dados de contexto
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados Colocar contexto XDM .
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---

# [!UICONTROL Inserir tipo ] de dados de contexto

[!UICONTROL Os ] contextos de local são um tipo de dados XDM padrão que descreve a localização de um evento observado, incluindo informações de ponto de interesse e coordenadas geográficas.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interação de ponto de interesse]](./poi-interaction.md) | Descreve detalhes sobre a interação do ponto de interesse (POI). |
| `activePOIs` | Matriz de [[!UICONTROL Detalhes do ponto de interesse]](./poi-details.md) | Descreve os POIs que causaram o evento. |
| `geo` | [[!UICONTROL Geografia]](./geo.md) | Descreve a localização geográfica onde a experiência foi entregue. |
| `localTime` | DateTime | Um carimbo de data e hora no formato [RFC 3339](https://tools.ietf.org/html/rfc3339), indicando a hora local que usa com um deslocamento de fuso horário declarado. O padrão de formatação é `yyyy-MM-dd'T'HH:mm:ssXXX` (por exemplo, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Número inteiro | O deslocamento do fuso horário local atual, em minutos, do UTC para o valor `localTime`. Isso deve incluir o deslocamento de horário de verão atual, se aplicável. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
