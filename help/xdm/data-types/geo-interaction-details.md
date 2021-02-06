---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;beacon;detalhes de interação;datatype;data-type;data type;Schema;home;popular topics;;social;social;social;topics;data-type;data type;data type;
solution: Experience Platform
title: Tipo de Dados de Detalhes da Interação Geográfica
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM Detalhes da Interação Geográfica.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# [!UICONTROL A interação geográfica ] detalha o tipo de dados

[!UICONTROL Os ] detalhes da interação geográfica são um tipo de dados XDM padrão que descreve o estado atual da inclusão em uma área definida geograficamente.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Descreve a forma geográfica da área com a qual está sendo interagida. Este campo pode descrever uma caixa, um círculo ou um polígono. |
| `deviceGeoAccuracy` | Duplo | A precisão do dispositivo ou mecanismo de medição geográfica, medida em metros. |
| `distanceToCenter` | Duplo | A distância ao centro da geografia, no caso de um círculo geográfico, medida em metros. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
