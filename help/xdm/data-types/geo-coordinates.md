---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;coordenadas;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Coordenadas Geográficas
description: Saiba mais sobre o tipo de dados XDM de coordenadas geográficas.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---

# Tipo de dados [!UICONTROL Coordenadas geográficas]

[!UICONTROL Coordenadas Geográficas] é um tipo de dados XDM padrão que descreve as coordenadas geográficas de um local. Este tipo de dados é baseado na especificação pública documentada em [schema.org](https://schema.org/GeoCoordinates).

![](../images/data-types/geo-coordinates.png){width=400}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema.description` | String | Uma descrição do que as coordenadas identificam. |
| `_schema.elevation` | Duplo | A elevação específica da coordenada definida. O valor deve estar em conformidade com o datum [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e é medido em metros. |
| `_schema.latitude` | Duplo | A coordenada vertical assinada do ponto geográfico. |
| `_schema.longitude` | Duplo | A coordenada horizontal assinada do ponto geográfico. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
