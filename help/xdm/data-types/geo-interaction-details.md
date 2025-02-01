---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;beacon;detalhes de interação;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Detalhes da Interação Geográfica
description: Saiba mais sobre o tipo de dados XDM de Detalhes de interação geográfica.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 13%

---

# [!UICONTROL Detalhes de interação geográfica] tipo de dados

[!UICONTROL Detalhes de interação geográfica] é um tipo de dados XDM padrão que descreve o estado atual de inclusão em uma área definida geograficamente.

![](../images/data-types/geo-interaction-details.png){width=400}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma geográfica]](./geo-shape.md) | Descreve a forma geográfica da área com a qual você está interagindo. Esse campo pode descrever uma caixa, um círculo ou um polígono. |
| `deviceGeoAccuracy` | Duplo | A precisão do dispositivo ou mecanismo de geomedição, medida em metros. |
| `distanceToCenter` | Duplo | A distância até o centro da área geográfica, no caso de um geocírculo, medida em metros. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
