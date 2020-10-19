---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de detalhes da interação geográfica
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM Detalhes da Interação Geográfica.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# [!UICONTROL Tipo de dados de detalhes] de interação geográfica

[!UICONTROL Detalhes] de interação geográfica é um tipo de dados XDM padrão que descreve o estado atual da inclusão em uma área definida geograficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Descreve a forma geográfica da área com a qual está sendo interagida. Este campo pode descrever uma caixa, um círculo ou um polígono. |
| `deviceGeoAccuracy` | Duplo | A precisão do dispositivo ou mecanismo de medição geográfica, medida em metros. |
| `distanceToCenter` | Duplo | A distância ao centro da geografia, no caso de um círculo geográfico, medida em metros. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
