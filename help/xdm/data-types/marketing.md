---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;dispositivo;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados de marketing
description: Saiba mais sobre o tipo de dados XDM de marketing.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# [!UICONTROL Marketing] tipo de dados

[!UICONTROL Marketing] é um tipo de dados XDM padrão que descreve atividades de marketing ativas com um ponto de contato específico.

![](../images/data-types/marketing.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `campaignGroup` | String | O nome do grupo de campanhas (nos casos em que várias campanhas são agrupadas como `50%_DISCOUNT`). |
| `campaignName` | String | O nome da campanha de marketing, como `50%_DISCOUNT_USA` ou `50%_DISCOUNT_ASIA`. |
| `trackingCode` | String | O código de rastreamento que pode ser usado para identificar a campanha de marketing à qual o evento está associado. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
