---
title: Tipo de dados do ad break
description: Este documento fornece uma visão geral do tipo de dados Ad break Experience Data Model (XDM).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 6%

---

# [!UICONTROL Pausa do anúncio] tipo de dados

[!UICONTROL Pausa do anúncio] é um tipo de dados padrão do Experience Data Model (XDM) que descreve como um anúncio cronometrado é inserido em uma mídia programada.

![Estrutura do tipo de dados](../images/data-types/ad-break.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc.title` | String | Um nome amigável para o ad break. |
| `_id` | String | Um identificador exclusivo para o ad break. |
| `offset` | Número inteiro | O deslocamento, em segundos, do ad break a partir do início do conteúdo principal. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
