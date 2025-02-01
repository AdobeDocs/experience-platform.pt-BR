---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;forma geográfica;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados da Forma Geográfica
description: Saiba mais sobre o tipo de dados Geo Shape XDM.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Forma Geográfica]

[!UICONTROL Forma Geográfica] é um tipo de dados XDM padrão que descreve a forma de uma área geográfica. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoShape).

![](../images/data-types/geo-shape.png){width=500}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.box` | Matriz de [[!UICONTROL Coordenadas Geográficas]](./geo-coordinates.md) | Descreve uma área geográfica delimitada por um retângulo formado por duas coordenadas. A primeira coordenada é o canto inferior do retângulo e a segunda coordenada é o canto superior. |
| `_schema.circle` | Matriz de [[!UICONTROL Coordenadas Geográficas]](./geo-coordinates.md) | Descreve uma região circular com um raio específico centrado em uma coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Uma série de quatro ou mais coordenadas em que a primeira e a última coordenadas são idênticas. |
| `_schema.description` | String | Uma descrição do que a forma está definindo. |
| `_schema.elevation` | Duplo | A elevação específica ou mínima da forma. Este valor está em conformidade com o datum [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. Em combinação com `ceiling`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional de um local. |
| `_id` | String | Um identificador exclusivo gerado pelo sistema para a forma. |
| `ceiling` | Duplo | A elevação máxima da forma. Esta propriedade só é válida quando usada em combinação com `elevation`. O valor está em conformidade com o datum [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. Em combinação com `elevation`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional de um local. |
