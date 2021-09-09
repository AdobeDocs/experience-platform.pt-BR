---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, dispositivo, tipo de dados, tipo de dados, tipo de dados, moeda;
solution: Experience Platform
title: Tipo de dados da moeda
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados Moeda XDM.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

#  Tipo de dados de moeda

 Moeda é um tipo de dados XDM padrão que descreve uma quantidade de moeda, incluindo o tipo de moeda e a data de conversão.

![](../images/data-types/currency.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `amount` | Duplo | A quantidade de moeda definida pelo `currencyCode`. |
| `conversionDate` | DateTime | Um carimbo de data e hora de quando a conversão de moeda foi feita. |
| `currencyCode` | String | Um código ISO 4217 que indica o tipo de moeda que `amount` representa. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
