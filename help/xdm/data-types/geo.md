---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; geo; tipo de dados; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados geográficos
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM geográficos.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL Geografia] tipo de dados

[!UICONTROL Geografia] é um tipo de dados XDM padrão que descreve a área geográfica em que um evento foi observado.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas de um local. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
| `city` | String | O nome da cidade. |
| `countryCode` | String | Os dois caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> código do país. |
| `dmaID` | Número inteiro | A pesquisa de mídia da Nielsen designou área de mercado. |
| `msaID` | Número inteiro | A área estatística metropolitana dos Estados Unidos onde ocorreu a observação. |
| `postalCode` | String | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, apenas fará parte do código postal. |
| `stateProvince` | String | O estado ou parte de província da observação. O formato segue o [ISO 3166-2 (país e subdivisão)](https://www.unece.org/cefact/locode/subdivisions.html) padrão. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
