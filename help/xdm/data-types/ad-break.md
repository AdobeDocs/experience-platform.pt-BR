---
title: Tipo de dados de ad break
description: Este documento fornece uma visão geral do tipo de dados Ad break Experience Data Model (XDM).
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 4%

---

# [!UICONTROL Intervalo comercial] tipo de dados

[!UICONTROL Intervalo comercial] é um tipo de dados padrão do Experience Data Model (XDM) que descreve como um anúncio cronometrado é inserido em uma mídia cronometrada.

![Estrutura do tipo de dados](../images/data-types/ad-break.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc.title` | String | Um nome amigável para o ad break. |
| `_id` | String | Um identificador exclusivo para o ad break. |
| `offset` | Número inteiro | O deslocamento, em segundos, do intervalo comercial desde o início do conteúdo principal. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
