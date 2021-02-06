---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;geo;círculo;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;fields;geo;círculo;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados do círculo geográfico
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do Círculo Geográfico.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# [!UICONTROL Tipo de ] Circledata geográfico

[!UICONTROL O ] Círculo Geográfico é um tipo de dados XDM padrão que descreve a região geográfica circular, considerando um raio específico centrado em um conjunto específico de coordenadas. Este tipo de dados tem por base a especificação pública documentada em [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas do centro do círculo. |
| `_schema.description` | String | Uma descrição do que o círculo contém. |
| `_schema.radius` | Duplo | O comprimento do raio do círculo. Esse valor está em conformidade com o datum [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para o círculo. |
