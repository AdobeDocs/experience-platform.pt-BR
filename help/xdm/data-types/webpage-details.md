---
keywords: Experience Platform;home;popular tópicos;schema;Schema;XDM;campos;schemas;Schemas;Detalhes da página da Web;datatype;data-type;data-type;data-type;webpage;;home;popular tópicos;;;campos;campos;;detalhes da página da Web;datatype;data-type;data-type;data type;webpage
solution: Experience Platform
title: Tipo de dados de detalhes da página da Web
topic: overview
description: Este documento fornece uma visão geral dos detalhes da página da Web sobre o tipo de dados do Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---


# [!UICONTROL A página da Web ] detalha o tipo de dados

[!UICONTROL Os ] detalhes da página da Web são um tipo de dados padrão do Experience Data Model (XDM), que descreve os detalhes sobre uma página da Web que acabou de ser carregada e visualizada, conforme registrado por um ExperienceEvent.

O tipo de dados destina-se a detalhes completos da página e cargas iniciais de página de aplicativos da Web de uma única página (SPA). Para interações que ocorrem em uma página carregada que não acionam um novo carregamento de página, consulte o tipo de dados [interação da Web](./web-interactions.md).

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Medição]](./measure.md) | O número de visualizações em uma página da Web. |
| `URL` | String | O URL normal ou normativo da página da Web. Esse pode ou não ser o URL real usado para acessar a página. Para gravar o URL usado para acessar a página, use `webLink`. O formato URI deve seguir o padrão [RFC 3986](https://tools.ietf.org/html/rfc3986). |
| `isErrorPage` | Booleano | Essa propriedade usa um sinalizador para indicar se a página é uma página de erro ou não. Esse sinalizador é usado para categorizar amplamente as interações da Web. O erro é definido pelo aplicativo e pode corresponder a uma página fornecida com um código de erro HTTP. |
| `isHomePage` | Booleano | Essa propriedade usa um sinalizador para indicar se a página é um home page ou não. Esse sinalizador é usado para categorizar amplamente as interações da Web. A definição de home page é determinada pelo aplicativo. |
| `name` | String | O nome normativo da página da Web. Esse nome não é necessariamente o título da página ou está diretamente associado ao conteúdo da página, mas é usado para organizar as páginas de um site para fins de classificação. |
| `server` | String | O servidor normal ou normativo que hospeda a página da Web. Pode ser ou não o host ou servidor que serviu a interação da página. |
| `siteSection` | String | O nome normativo da seção do site onde esta página da Web está. Isso pode ser usado para classificar ou categorizar a interação. |
| `viewName` | String | O nome da visualização, em uma página. Essa propriedade costuma ser usada com aplicativos de página única ou páginas que têm guias ou controles que alteram a maioria do layout da página. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)