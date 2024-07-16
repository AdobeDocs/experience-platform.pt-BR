---
title: Tipo de dados de ad break
description: Saiba mais sobre o tipo de dados Ad break Experience Data Model (XDM).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 21%

---

# Tipo de dados [!UICONTROL Ad break]

[!UICONTROL Ad break] é um tipo de dados padrão do Experience Data Model (XDM) que descreve como um anúncio cronometrado é inserido em uma mídia cronometrada.

![Estrutura de tipo de dados](../images/data-types/ad-break.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc.title` | String | Um nome amigável para o ad break. |
| `_id` | String | Um identificador exclusivo para o ad break. |
| `offset` | Número inteiro | O deslocamento, em segundos, do intervalo comercial desde o início do conteúdo principal. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
