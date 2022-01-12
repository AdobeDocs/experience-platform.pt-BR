---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; geo; forma geográfica; tipo de dados; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados da forma geográfica
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Forma Geográfica.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL Forma geográfica] tipo de dados

[!UICONTROL Forma geográfica] é um tipo de dados XDM padrão que descreve a forma de uma área geográfica. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.box` | Matriz de [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve uma área geográfica delimitada por um retângulo formado por duas coordenadas. A primeira coordenada é o canto inferior do retângulo, e a segunda coordenada é o canto superior. |
| `_schema.circle` | Matriz de [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve uma região circular com um raio específico centrado em uma coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Uma série de quatro ou mais coordenadas em que a primeira e a última coordenadas são idênticas. |
| `_schema.description` | String | Uma descrição do que a forma está definindo. |
| `_schema.elevation` | Duplo | A elevação específica ou mínima da forma. Esse valor está em conformidade com a [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) dados e medidos em metros. Em combinação com `ceiling`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional para um local. |
| `_id` | String | Um identificador exclusivo gerado pelo sistema para a forma. |
| `ceiling` | Duplo | A elevação máxima da forma. Esta propriedade só é válida quando usada em combinação com `elevation`. O valor está em conformidade com o [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) dados e medidos em metros. Em combinação com `elevation`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional para um local. |
