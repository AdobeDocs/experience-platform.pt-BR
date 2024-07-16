---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;círculo;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados do Círculo Geográfico
description: Saiba mais sobre o tipo de dados Geo Circle XDM.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 11%

---

# Tipo de dados [!UICONTROL Círculo Geográfico]

[!UICONTROL Círculo Geográfico] é um tipo de dados XDM padrão que descreve a região geográfica circular, dado um raio específico centrado em um conjunto específico de coordenadas. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas do centro do círculo. |
| `_schema.description` | String | Uma descrição do que o círculo contém. |
| `_schema.radius` | Duplo | O comprimento do raio do círculo. Este valor está em conformidade com o datum [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para o círculo. |
