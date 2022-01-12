---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; geo; círculo; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados do círculo geográfico
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de círculo geográfico.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL Círculo geográfico] tipo de dados

[!UICONTROL Círculo geográfico] é um tipo de dados XDM padrão que descreve a região geográfica circular, considerando um raio específico centrado em um conjunto específico de coordenadas. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas do centro do círculo. |
| `_schema.description` | String | Uma descrição do que contém o círculo. |
| `_schema.radius` | Duplo | O comprimento do raio do círculo. Esse valor está em conformidade com a [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) dados e medidos em metros. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para o círculo. |
