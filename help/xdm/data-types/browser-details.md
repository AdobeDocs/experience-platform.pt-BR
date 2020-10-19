---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de dados de detalhes do navegador
topic: overview
description: Este documento fornece uma visão geral do tipo de dados XDM de detalhes do navegador.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 8%

---


# [!UICONTROL Tipo de dados de detalhes] do navegador

[!UICONTROL Os detalhes] do navegador são um tipo de dados XDM padrão que descreve os detalhes relacionados a um navegador ou aplicativo.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `acceptLanguage` | String | Uma tag de idioma IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica se as configurações do usuário permitem a gravação de cookies. |
| `javaEnabled` | Booleano | Indica se o Java foi ativado no dispositivo a partir do qual a observação foi feita. |
| `javaScriptEnabled` | Booleano | Indica se o JavaScript foi ativado no dispositivo a partir do qual a observação foi feita. |
| `javaScriptVersion` | String | A versão do JavaScript suportada durante a observação. |
| `javaVersion` | String | A versão do Java é suportada durante a observação. |
| `name` | String | O nome do aplicativo ou navegador. |
| `quicktimeVersion` | String | A versão do Apple Quicktime é compatível durante a observação. |
| `thirdPartyCookiesEnabled` | Booleano | Indica se cookies de terceiros foram ativados no dispositivo a partir do qual a observação foi feita. |
| `userAgent` | String | A sequência HTTP user-agent da solicitação do cliente. |
| `vendor` | String | O fornecedor do aplicativo ou navegador. |
| `version` | String | A versão do aplicativo ou navegador. |
| `viewportHeight` | Número inteiro | O tamanho vertical em pixels da janela em que o evento foi exibido. Para um evento de visualização da Web, esta é a altura do visor do navegador. |
| `viewportWidth` | Número inteiro | O tamanho horizontal em pixels da janela em que o evento foi exibido. Para um evento de visualização da Web, esta é a largura da janela do navegador. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)