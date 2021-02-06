---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;Schemas;poi;poi details;point-of-interest details;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de Dados de Detalhes do Ponto de Interesse
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Detalhes do Ponto de Interesse.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---


# [!UICONTROL Tipo de dados do ponto de interesse ] detalha

[!UICONTROL Os ] detalhes do ponto de interesse são um tipo de dados XDM padrão que descreve os dados geográficos relacionados aos quais um evento foi observado.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descreve os detalhes de sinal ativos para a interação POI. |
| `geoInteractionDetails` | [[!UICONTROL Detalhes da interação geográfica]](./geo-interaction-details.md) | Descreve os detalhes geográficos ativos para a interação POI. |
| `category` | String | Uma categoria geral atribuída para organizar os POIs pelo administrador das definições de POI. |
| `distanceToPOICenter` | Duplo | A distância estimada do centro POI, em metros. |
| `locatingType` | String | O mecanismo usado para determinar a localização. Os valores aceitos incluem: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | String | Um nome dado ao POI. |
| `poiID` | String | Um identificador exclusivo do POI. |
| `type` | String | O tipo geral de POI que usa um schema de digitação selecionado pelo administrador das definições de POI. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)