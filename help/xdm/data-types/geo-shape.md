---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;forma geográfica;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados da Forma Geográfica
description: Saiba mais sobre o tipo de dados Geo Shape XDM.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 3%

---

# [!UICONTROL Forma geográfica] tipo de dados

[!UICONTROL Forma geográfica] é um tipo de dados XDM padrão que descreve a forma de uma área geográfica. Este tipo de dados baseia-se na especificação pública documentada no [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.box` | Matriz de [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve uma área geográfica delimitada por um retângulo formado por duas coordenadas. A primeira coordenada é o canto inferior do retângulo e a segunda coordenada é o canto superior. |
| `_schema.circle` | Matriz de [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve uma região circular com um raio específico centrado em uma coordenada geográfica. |
| `_schema.polygon` | [[!UICONTROL Círculo geográfico]](./geo-circle.md) | Uma série de quatro ou mais coordenadas em que a primeira e a última coordenadas são idênticas. |
| `_schema.description` | String | Uma descrição do que a forma está definindo. |
| `_schema.elevation` | Duplo | A elevação específica ou mínima da forma. Esse valor está em conformidade com o [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum e é medida em metros. Em combinação com `ceiling`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional de um local. |
| `_id` | String | Um identificador exclusivo gerado pelo sistema para a forma. |
| `ceiling` | Duplo | A elevação máxima da forma. Esta propriedade só é válida quando usada em combinação com `elevation`. O valor está em conformidade com o [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum e é medida em metros. Em combinação com `elevation`, essa propriedade pode ser usada para expressar uma caixa delimitadora tridimensional de um local. |
