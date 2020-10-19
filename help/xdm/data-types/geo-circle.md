---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados do Círculo geográfico
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do Círculo Geográfico.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 4%

---


# [!UICONTROL Tipo de dados do Círculo] geográfico

[!UICONTROL Círculo] geográfico é um tipo de dados XDM padrão que descreve a região geográfica circular, considerando um raio específico centrado em um conjunto específico de coordenadas. Este tipo de dados é baseado na especificação pública documentada em [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas do centro do círculo. |
| `_schema.description` | String | Uma descrição do que o círculo contém. |
| `_schema.radius` | Duplo | O comprimento do raio do círculo. Este valor está em conformidade com o dado [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para o círculo. |
