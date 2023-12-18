---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;Detalhes da página da Web;tipo de dados;tipo de dados;tipo de dados;página da Web
solution: Experience Platform
title: Tipo de Dados de Detalhes da Página da Web
description: Saiba mais sobre os detalhes da página da Web do tipo de dados do Experience Data Model (XDM).
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# [!UICONTROL Detalhes da página da Web] tipo de dados

[!UICONTROL Detalhes da página da Web] é um tipo de dados padrão do Experience Data Model (XDM) que descreve detalhes sobre uma página da Web que acabou de ser carregada e visualizada, conforme registrado por um ExperienceEvent.

O tipo de dados é destinado aos detalhes completos da página e aos carregamentos iniciais da página de aplicativos web de página única (SPA). Para interações que ocorrem em uma página carregada que não acionam um novo carregamento de página, consulte a [interação na web](./web-interaction.md) tipo de dados.

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL Medir]](./measure.md) | O número de visualizações em uma página da Web. |
| `URL` | String | O URL normativo ou usual da página da Web. Este pode ou não ser o URL real usado para acessar a página. Para registrar o URL usado para acessar a página, use `webLink`. O formato URI deve seguir o [RFC 3986](https://tools.ietf.org/html/rfc3986) padrão. |
| `isErrorPage` | Booleano | Essa propriedade usa um sinalizador para indicar se a página é uma página de erro ou não. Esse sinalizador é usado para categorizar amplamente as interações na web. O erro é definido pelo aplicativo e pode corresponder a uma página com um código de erro HTTP. |
| `isHomePage` | Booleano | Essa propriedade usa um sinalizador para indicar se a página é uma página inicial ou não. Esse sinalizador é usado para categorizar amplamente as interações na web. A definição de página inicial é determinada pelo aplicativo. |
| `name` | String | O nome normativo da página da Web. Esse nome não é necessariamente o título da página ou associado diretamente ao conteúdo da página, mas é usado para organizar as páginas de um site para fins de classificação. |
| `server` | String | O servidor normativo ou usual que hospeda a página da Web. Esse pode ou não ser o host ou servidor que realmente serviu a interação da página. |
| `siteSection` | String | O nome normativo da seção do site onde esta página da Web reside. Isso pode ser usado para classificar ou categorizar a interação. |
| `viewName` | String | O nome da exibição em uma página. Essa propriedade geralmente é usada com aplicativos de página única ou páginas que têm guias ou controles que alteram a maioria do layout da página. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
