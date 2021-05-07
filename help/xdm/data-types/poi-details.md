---
keywords: Experience Platform, home, tópicos populares, schema, esquema, XDM, campos, esquemas, esquemas, poi, detalhes do ponto de interesse, detalhes do ponto de interesse, tipo de dados, tipo de dados, tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados de detalhes do ponto de interesse
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Detalhes do Ponto de Interesse.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 4%

---

# [!UICONTROL Point of interest details] tipo de dados

[!UICONTROL Point of interest details] é um tipo de dados XDM padrão que descreve os dados geográficos relacionados aos quais um evento foi observado.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descreve os detalhes do sinal ativo para a interação de POI. |
| `geoInteractionDetails` | [[!UICONTROL Geo interaction details]](./geo-interaction-details.md) | Descreve os detalhes geográficos ativos da interação de POI. |
| `category` | String | Uma categoria geral atribuída para organizar os POIs pelo administrador das definições de POI. |
| `distanceToPOICenter` | Duplo | A distância estimada do centro do POI, em metros. |
| `locatingType` | String | O mecanismo usado para determinar a localização. Os valores aceitos incluem: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | String | Um nome dado ao POI. |
| `poiID` | String | Um identificador exclusivo do POI. |
| `type` | String | O tipo geral do POI usando um schema de digitação selecionado pelo administrador das definições do POI. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
