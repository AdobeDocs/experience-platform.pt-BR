---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;interação na web;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de Dados de Interação na Web
description: Este documento fornece uma visão geral do tipo de dados Experience Data Model (XDM) de interação na web.
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---

# [!UICONTROL Interação na Web] tipo de dados

[!UICONTROL Interação na Web] é um tipo de dados padrão do Experience Data Model (XDM) que descreve informações sobre as interações que ocorreram em uma página da Web após a conclusão do carregamento da página inicial. Destina-se a gravar interações em aplicativos avançados da Web que não acionam um novo carregamento de página, como aplicativos web de página única (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Medição]](./measure.md) | Uma medida que rastreia o clique em um link da Web. |
| `URL` | String | O link ou URL real usado para esta interação na web. |
| `name` | String | O nome normativo usado para este link da Web. Isso é usado para fins de classificação. |
| `type` | String | O tipo de link. Essa propriedade deve ser igual a um dos seguintes valores de enumeração: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
