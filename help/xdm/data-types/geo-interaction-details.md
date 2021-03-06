---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, beacon, detalhes de interação, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados de detalhes da interação geográfica
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Detalhes da Interação Geográfica.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 4%

---

# [!UICONTROL Interação geográfica ] detalha o tipo de dados

[!UICONTROL A interação geográfica ] detalha um tipo de dados XDM padrão que descreve o estado atual da inclusão em uma área definida geograficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Descreve a forma geográfica da área com a qual a interação está sendo feita. Este campo pode descrever uma caixa, um círculo ou um polígono. |
| `deviceGeoAccuracy` | Duplo | A precisão do dispositivo ou mecanismo de medição geográfica, medida em metros. |
| `distanceToCenter` | Duplo | A distância até ao centro da geografia no caso de um círculo geográfico, medida em metros. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
