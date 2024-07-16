---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;dispositivo;tipo de dados;tipo de dados;tipo de dados;moeda;
solution: Experience Platform
title: Tipo de dados da moeda
description: Saiba mais sobre o tipo de dados Currency XDM.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# Tipo de dados [!UICONTROL Moeda]

[!UICONTROL Moeda] é um tipo de dados XDM padrão que descreve uma quantidade de moeda, incluindo o tipo de moeda e a data de conversão.

![](../images/data-types/currency.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `amount` | Duplo | O valor da moeda conforme definido por `currencyCode`. |
| `conversionDate` | DateTime | Um carimbo de data e hora de quando a conversão de moeda foi feita. |
| `currencyCode` | String | Um código ISO 4217 indicando o tipo de moeda que `amount` representa. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
