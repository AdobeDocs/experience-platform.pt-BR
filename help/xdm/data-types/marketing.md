---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, dispositivo, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados de marketing
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados Marketing XDM.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---


#  Tipo de dados de marketing

 O Marketing é um tipo de dados XDM padrão que descreve atividades de marketing que estão ativas com um ponto de contato específico.

![](../images/data-types/marketing.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignGroup` | String | O nome do grupo de campanha (nos casos em que várias campanhas são agrupadas como `50%_DISCOUNT`). |
| `campaignName` | String | O nome da campanha de marketing, como `50%_DISCOUNT_USA` ou `50%_DISCOUNT_ASIA`. |
| `trackingCode` | String | O código de rastreamento que pode ser usado para identificar a campanha de marketing à qual o evento está associado. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
