---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, campos, esquemas, esquemas, esquemas, detalhes da página da Web, tipo de dados, tipo de dados, tipo de dados, página da Web
solution: Experience Platform
title: Tipo de dados de detalhes da página da Web
topic-legacy: overview
description: Este documento fornece uma visão geral dos detalhes da página da Web Tipo de dados do Experience Data Model (XDM).
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 4%

---

# [!UICONTROL Página da Web ] detalha o tipo de dados

[!UICONTROL A página da Web ] detalha um tipo de dados padrão do Experience Data Model (XDM) que descreve detalhes sobre uma página da Web que acabou de ser carregada e visualizada, conforme registrada por um ExperienceEvent.

O tipo de dados destina-se aos detalhes completos da página e aos carregamentos iniciais da página de aplicativos web de página única (SPA). Para interações que estão acontecendo em uma página carregada que não acionam um novo carregamento de página, consulte o tipo de dados [interação da Web](./web-interaction.md) .

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Medição]](./measure.md) | O número de visualizações em uma página da Web. |
| `URL` | String | O URL normal ou normal da página da Web. Pode ou não ser o URL real usado para acessar a página. Para registrar o URL usado para acessar a página, use `webLink`. O formato URI deve seguir o padrão [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booleano | Essa propriedade usa um sinalizador para indicar se a página é uma página de erro ou não. Esse sinalizador é usado para classificar amplamente interações da Web. O erro é definido pelo aplicativo e pode corresponder a uma página servida com um código de erro HTTP. |
| `isHomePage` | Booleano | Essa propriedade usa um sinalizador para indicar se a página é uma página inicial ou não. Esse sinalizador é usado para classificar amplamente interações da Web. A definição de página inicial é determinada pelo aplicativo. |
| `name` | String | O nome normativo da página da Web. Esse nome não é necessariamente o título da página ou está diretamente associado ao conteúdo da página, mas é usado para organizar as páginas de um site para fins de classificação. |
| `server` | String | O servidor normal ou normativo que hospeda a página da Web. Pode ser ou não o host ou servidor que realmente atendeu à interação da página. |
| `siteSection` | String | O nome normativo da seção do site em que esta página da Web está. Isso pode ser usado para classificar ou categorizar a interação. |
| `viewName` | String | O nome da exibição em uma página. Essa propriedade geralmente é usada com aplicativos de página única ou páginas que têm guias ou controles que alteram a maioria do layout da página. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
