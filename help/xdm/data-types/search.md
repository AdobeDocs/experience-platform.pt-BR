---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;search;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de pesquisa
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Search Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---


# [!UICONTROL Tipo ] de dados de pesquisa

[!UICONTROL A ] pesquisa é um tipo de dados padrão do Experience Data Model (XDM) que contém informações sobre a atividade de pesquisa na Web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `isPaid` | Booleano | Usado para indicar se a pesquisa é paga ou não. |
| `keywords` | String | As palavras-chave para a pesquisa. |
| `pageDepth` | Número inteiro | A profundidade da página nos resultados da pesquisa. |
| `position` | Número inteiro | A posição ou classificação da listagem na página de resultados da pesquisa. |
| `searchEngine` | String | O mecanismo de pesquisa usado pela pesquisa. |
| `searchEngineID` | String | O identificador específico do aplicativo usado para identificar o mecanismo de pesquisa. |
| `slot` | String | A seção nomeada da página onde o resultado da pesquisa foi exibido. O valor dessa propriedade deve ser igual a um dos valores de enumeração conhecidos definidos, como `top`, `side` ou `bottom`. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)