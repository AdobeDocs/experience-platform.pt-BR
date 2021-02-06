---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;geo;geo;geo;geo;shape;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de forma geográfica
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM da Forma geográfica.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---


# [!UICONTROL Tipo de ] Shapedata geográfico

[!UICONTROL O Geo ] Shapis é um tipo de dados XDM padrão que descreve a forma de uma área geográfica. Este tipo de dados tem por base a especificação pública documentada em [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.box` | Matriz de [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve uma área geográfica delimitada por um retângulo formado por duas coordenadas. A primeira coordenada é o canto inferior do retângulo e a segunda coordenada é o canto superior. |
| `_schema.circle` | Matriz de [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve uma região circular com um raio específico centrado em uma coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Uma série de quatro ou mais coordenadas em que a primeira e a última coordenadas são idênticas. |
| `_schema.description` | String | Uma descrição do que a forma está definindo. |
| `_schema.elevation` | Duplo | A elevação específica ou mínima da forma. Esse valor está em conformidade com o datum [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. Em combinação com `ceiling`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional para um local. |
| `_id` | String | Um identificador exclusivo gerado pelo sistema para a forma. |
| `ceiling` | Duplo | A elevação máxima da forma. Esta propriedade só é válida quando usada em combinação com `elevation`. O valor está em conformidade com o datum [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. Em combinação com `elevation`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional para um local. |
