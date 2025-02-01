---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;geo;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados geográficos
description: Saiba mais sobre o tipo de dados Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 34%

---

# Tipo de dados [!UICONTROL Geo]

[!UICONTROL Geo] é um tipo de dados XDM padrão que descreve a área geográfica em que um evento foi observado.

![](../images/data-types/geo.png){width=400}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordenadas geográficas]](./geo-coordinates.md) | Descreve as coordenadas geográficas de um local. |
| `_id` | String | Uma ID exclusiva gerada pelo sistema para as coordenadas. |
| `city` | String | O nome da cidade. |
| `countryCode` | String | O código <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> de dois caracteres para o país. |
| `dmaID` | Número inteiro | A área de mercado designada de pesquisa de mídia da Nielsen. |
| `msaID` | Número inteiro | A área estatística metropolitana dos Estados Unidos onde ocorreu a observação. |
| `postalCode` | String | O código postal do local. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `stateProvince` | String | A parte do estado ou província da observação. O formato segue o padrão [ISO 3166-2 (país e subdivisão)](https://www.unece.org/cefact/locode/subdivisions.html). |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
