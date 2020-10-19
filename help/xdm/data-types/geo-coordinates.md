---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de Coordenadas geográficas
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Coordenadas Geográficas.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---


# [!UICONTROL Tipo de dados de Coordenadas] geográficas

[!UICONTROL Coordenadas] geográficas é um tipo de dados XDM padrão que descreve as coordenadas geográficas de um local. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.description` | String | Uma descrição do que as coordenadas identificam. |
| `_schema.elevation` | Duplo | A elevação específica da coordenada definida. O valor deve estar em conformidade com os dados [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_schema.latitude` | Duplo | A coordenada vertical assinada do ponto geográfico. |
| `_schema.longitude` | Duplo | A coordenada horizontal assinada do ponto geográfico. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
