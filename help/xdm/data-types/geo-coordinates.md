---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;campos;schemas;geo;coordenadas;datatype;data-type;data type;Schema;home;popular topics;;;XDM;fields;details;geo;details;Coordination;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados de coordenadas geográficas
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Coordenadas Geográficas.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---


# [!UICONTROL Tipo ] de dados de coordenadas geográficas

[!UICONTROL A ] Coordenadoria geográfica é um tipo de dados XDM padrão que descreve as coordenadas geográficas de um local. Este tipo de dados tem por base a especificação pública documentada em [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.description` | String | Uma descrição do que as coordenadas identificam. |
| `_schema.elevation` | Duplo | A elevação específica da coordenada definida. O valor deve estar em conformidade com a data [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_schema.latitude` | Duplo | A coordenada vertical assinada do ponto geográfico. |
| `_schema.longitude` | Duplo | A coordenada horizontal assinada do ponto geográfico. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
