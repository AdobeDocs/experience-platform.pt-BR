---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; campos; esquemas; esquemas; pesquisa; tipo de dados; tipo de dados; tipo de dados;
solution: Experience Platform
title: Tipo de dados de pesquisa
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados Search Experience Data Model (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# [!UICONTROL Search] tipo de dados

[!UICONTROL Search] é um tipo de dados padrão do Experience Data Model (XDM) que contém informações sobre a atividade de pesquisa na Web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `isPaid` | Booleano | Usado para indicar se a pesquisa é paga ou não. |
| `keywords` | String | As palavras-chave da pesquisa. |
| `pageDepth` | Número inteiro | A profundidade da página nos resultados da pesquisa. |
| `position` | Número inteiro | A posição ou classificação da listagem na página de resultados da pesquisa. |
| `searchEngine` | String | O mecanismo de pesquisa usado pela pesquisa. |
| `searchEngineID` | String | O identificador específico do aplicativo usado para identificar o mecanismo de pesquisa. |
| `slot` | String | A seção nomeada da página onde o resultado da pesquisa foi exibido. O valor dessa propriedade deve ser igual a um dos valores de enumeração conhecidos definidos, como `top`, `side` ou `bottom`. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
