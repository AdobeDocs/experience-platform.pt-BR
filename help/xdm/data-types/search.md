---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;pesquisar;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Pesquisar tipo de dados
description: Saiba mais sobre o tipo de dados do Search Experience Data Model (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---

# [!UICONTROL Pesquisar] tipo de dados

[!UICONTROL Pesquisar] é um tipo de dados padrão do Experience Data Model (XDM) que contém informações sobre a atividade de pesquisa na web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `isPaid` | Booleano | Usado para indicar se a pesquisa é paga ou não. |
| `keywords` | String | As palavras-chave para a pesquisa. |
| `pageDepth` | Número inteiro | A profundidade da página nos resultados da pesquisa. |
| `position` | Número inteiro | A posição ou classificação da lista na página de resultados da pesquisa. |
| `searchEngine` | String | O mecanismo de pesquisa usado pela pesquisa. |
| `searchEngineID` | String | O identificador específico do aplicativo usado para identificar o mecanismo de pesquisa. |
| `slot` | String | A seção nomeada da página onde o resultado da pesquisa apareceu. O valor dessa propriedade deve ser igual a um dos valores de enumeração conhecidos definidos, como `top`, `side`ou `bottom`. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
