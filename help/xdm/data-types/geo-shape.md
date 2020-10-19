---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de Forma geográfica
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM da Forma geográfica.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# [!UICONTROL Tipo de dados de Forma] geográfica

[!UICONTROL Forma] geográfica é um tipo de dados XDM padrão que descreve a forma de uma área geográfica. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.box` | Matriz de coordenadas [[!UICONTROL geográficas]](./geo-coordinates.md) | Descreve uma área geográfica delimitada por um retângulo formado por duas coordenadas. A primeira coordenada é o canto inferior do retângulo e a segunda coordenada é o canto superior. |
| `_schema.circle` | Matriz de coordenadas [[!UICONTROL geográficas]](./geo-coordinates.md) | Descreve uma região circular com um raio específico centrado em uma coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Uma série de quatro ou mais coordenadas em que a primeira e a última coordenadas são idênticas. |
| `_schema.description` | String | Uma descrição do que a forma está definindo. |
| `_schema.elevation` | Duplo | A elevação específica ou mínima da forma. Este valor está em conformidade com o dado [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. Em combinação com `ceiling`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional para um local. |
| `_id` | String | Um identificador exclusivo gerado pelo sistema para a forma. |
| `ceiling` | Duplo | A elevação máxima da forma. Essa propriedade só é válida quando usada em combinação com `elevation`. O valor está em conformidade com o dado [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. Em combinação com `elevation`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional para um local. |
