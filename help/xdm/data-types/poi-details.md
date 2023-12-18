---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;poi;detalhes de poi;ponto de interesse;detalhes do ponto de interesse;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Detalhes do Ponto de Interesse
description: Saiba mais sobre o tipo de dados XDM de detalhes do ponto de interesse.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# [!UICONTROL Detalhes do ponto de interesse] tipo de dados

[!UICONTROL Detalhes do ponto de interesse] é um tipo de dados XDM padrão que descreve os dados geográficos relacionados onde um evento foi observado.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Sinal]](./beacon.md) | Descreve os detalhes do sinal ativo para a interação do POI. |
| `geoInteractionDetails` | [[!UICONTROL Detalhes de interação geográfica]](./geo-interaction-details.md) | Descreve os detalhes geográficos ativos para a interação do POI. |
| `category` | String | Uma categoria geral atribuída para organizar os POIs pelo administrador das definições de POI. |
| `distanceToPOICenter` | Duplo | A distância estimada do centro do POI em metros. |
| `locatingType` | String | O mecanismo usado para determinar a localização. Os valores aceitos incluem: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | String | Um nome dado ao POI. |
| `poiID` | String | Um identificador exclusivo do POI. |
| `type` | String | O tipo geral de POI usando um esquema de digitação selecionado pelo administrador das definições de POI. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
