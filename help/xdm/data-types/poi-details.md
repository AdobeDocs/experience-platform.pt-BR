---
keywords: Experience Platform, home, tópicos populares, schema, esquema, XDM, campos, esquemas, esquemas, poi, detalhes do ponto de interesse, detalhes do ponto de interesse, tipo de dados, tipo de dados, tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados de detalhes do ponto de interesse
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Detalhes do Ponto de Interesse.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 5%

---

# [!UICONTROL Tipo de dados de ] detalhes do ponto de interesse

[!UICONTROL O ponto de interesse ] detalha um tipo de dados XDM padrão que descreve os dados geográficos relacionados aos quais um evento foi observado.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descreve os detalhes do sinal ativo para a interação de POI. |
| `geoInteractionDetails` | [[!UICONTROL Detalhes da interação geográfica]](./geo-interaction-details.md) | Descreve os detalhes geográficos ativos da interação de POI. |
| `category` | String | Uma categoria geral atribuída para organizar os POIs pelo administrador das definições de POI. |
| `distanceToPOICenter` | Duplo | A distância estimada do centro do POI, em metros. |
| `locatingType` | String | O mecanismo usado para determinar a localização. Os valores aceitos incluem: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | String | Um nome dado ao POI. |
| `poiID` | String | Um identificador exclusivo do POI. |
| `type` | String | O tipo geral do POI usando um schema de digitação selecionado pelo administrador das definições do POI. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
