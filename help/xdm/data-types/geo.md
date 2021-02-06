---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;geo;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;processors;geo;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de dados geográficos
topic: overview
description: Este documento fornece uma visão geral do tipo de dados Geo XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 4%

---


# [!UICONTROL Tipo de ] Geodata

 Geois é um tipo de dados XDM padrão que descreve a área geográfica em que um evento foi observado.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas de um lugar. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
| `city` | String | O nome da cidade. |
| `countryCode` | String | O código de dois caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> do país. |
| `dmaID` | Número inteiro | A investigação sobre os meios de comunicação social Nielsen designou a área de mercado. |
| `msaID` | Número inteiro | A área metropolitana de estatística dos Estados Unidos onde ocorreu a observação. |
| `postalCode` | String | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, este código só contém uma parte do código postal. |
| `stateProvince` | String | A parte do estado ou província da observação. O formato segue o padrão [ISO 3166-2 (país e subdivisão)](http://www.unece.org/cefact/locode/subdivisions.html). |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)