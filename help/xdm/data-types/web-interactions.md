---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;interação da Web;datatype;data-type;data type;Schema;home;popular topics;;XDM;fields;fields;processors;web intervention;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo de Dados de Interação da Web
topic: overview
description: Este documento fornece uma visão geral do tipo de dados do Experience Data Model (XDM) da interação da Web.
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---


# [!UICONTROL Tipo de dados ] interativos da Web

[!UICONTROL A interação com a Web ] é um tipo de dados padrão do Modelo de Dados de Experiência (XDM) que descreve informações sobre interações que aconteceram em uma página da Web após a conclusão do carregamento inicial da página. Ela se destina à gravação de interações em aplicativos da Web avançados que não acionam uma nova carga de página, como aplicativos da Web de uma única página (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Medição]](./measure.md) | Uma medida que rastreia o clique de um link da Web. |
| `URL` | String | O link ou URL real usado para essa interação da Web. |
| `name` | String | O nome normativo usado para este link da Web. Isso é usado para fins de classificação. |
| `type` | String | O tipo de link. Essa propriedade deve ser igual a um dos seguintes valores de enumeração: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)