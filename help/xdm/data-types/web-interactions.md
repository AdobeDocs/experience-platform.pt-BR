---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, campos, esquemas, esquemas, interação da Web, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Interação da Web
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados do Experience Data Model (XDM) de interação da Web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---

# [!UICONTROL Web interaction] tipo de dados

[!UICONTROL Web interaction] é um tipo de dados padrão do Experience Data Model (XDM) que descreve informações sobre interações que aconteceram em uma página da Web depois que o carregamento da página inicial foi concluído. Destina-se a gravar interações em aplicativos da Web avançados que não acionam um novo carregamento de página, como aplicativos da Web de página única (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Measure]](./measure.md) | Uma medida que rastreia o clique de um link da Web. |
| `URL` | String | O link ou URL real usado para essa interação da Web. |
| `name` | String | O nome normativo usado para este link da Web. Isso é usado para fins de classificação. |
| `type` | String | O tipo de link. Essa propriedade deve ser igual a um dos seguintes valores de enumeração: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)
