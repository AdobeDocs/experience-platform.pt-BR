---
keywords: Experience Platform, home, tópicos populares, schema, esquema, XDM, campos, esquemas, esquemas, poi, interação, ponto de interesse, ponto de interesse, tipo de dados, tipo de dados, tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Interação de Ponto de Interesse
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de Interação de Ponto de Interesse.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---

# [!UICONTROL Point of interest interaction] tipo de dados

[!UICONTROL Point of interest interaction] é um tipo de dados XDM padrão que descreve o dispositivo sem fio que comunica informações de identidade para aplicativos móveis, à medida que os dispositivos móveis estão dentro do alcance.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Descreve os detalhes do POI que causou o evento. |
| `poiEntries` | Objeto | Descreve o número de vezes que uma pessoa entrou no POI. Contém duas propriedades: <ul><li>`id`: Um identificador exclusivo para a medida.</li><li>`value`: O valor quantificável da medida.</li></ul> |
| `poiExits` | Objeto | Descreve o número de vezes que uma pessoa saiu do POI. Contém duas propriedades: <ul><li>`id`: Um identificador exclusivo para a medida.</li><li>`value`: O valor quantificável da medida.</li></ul> |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
