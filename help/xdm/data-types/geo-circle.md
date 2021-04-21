---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; geo; círculo; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados do círculo geográfico
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de círculo geográfico.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# [!UICONTROL Geo Circle] tipo de dados

[!UICONTROL Geo Circle] é um tipo de dados XDM padrão que descreve a região geográfica circular, considerando um raio específico centrado em um conjunto específico de coordenadas. Esse tipo de dados é baseado na especificação pública documentada em [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descreve as coordenadas geográficas do centro do círculo. |
| `_schema.description` | String | Uma descrição do que contém o círculo. |
| `_schema.radius` | Duplo | O comprimento do raio do círculo. Esse valor está em conformidade com o datum [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para o círculo. |
