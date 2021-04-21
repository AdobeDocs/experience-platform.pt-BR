---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; geo; coordenadas; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados de coordenadas geográficas
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM das coordenadas geográficas.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

# [!UICONTROL Geo Coordinates] tipo de dados

[!UICONTROL Geo Coordinates] é um tipo de dados XDM padrão que descreve as coordenadas geográficas de um local. Esse tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.description` | String | Uma descrição do que as coordenadas identificam. |
| `_schema.elevation` | Duplo | A elevação específica da coordenada definida. O valor deve estar em conformidade com o datum [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_schema.latitude` | Duplo | A coordenada vertical assinada do ponto geográfico. |
| `_schema.longitude` | Duplo | A coordenada horizontal assinada do ponto geográfico. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
