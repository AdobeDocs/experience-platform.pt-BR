---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, campos, esquemas, esquemas, navegador, detalhes do navegador, tipo de dados, tipo de dados, tipo de dados;
solution: Experience Platform
title: Tipo de dados de detalhes do navegador
description: Este documento fornece uma visão geral do tipo de dados XDM de detalhes do navegador.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 12%

---

# [!UICONTROL Detalhes do navegador] tipo de dados

[!UICONTROL Detalhes do navegador] é um tipo de dados XDM padrão que descreve detalhes relacionados a um navegador ou aplicativo.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `acceptLanguage` | String | Uma tag de idioma IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica se as configurações do usuário permitem a gravação de cookies. |
| `javaEnabled` | Booleano | Indica se o Java foi ativado no dispositivo de onde a observação foi feita. |
| `javaScriptEnabled` | Booleano | Indica se o JavaScript foi ativado no dispositivo do qual a observação foi feita. |
| `javaScriptVersion` | String | A versão do JavaScript suportada durante a observação. |
| `javaVersion` | String | A versão do Java suportada durante a observação. |
| `name` | String | O nome do aplicativo ou do navegador. |
| `quicktimeVersion` | String | A versão do Apple Quicktime suportada durante a observação. |
| `thirdPartyCookiesEnabled` | Booleano | Indica se cookies de terceiros foram ativados no dispositivo a partir do qual a observação foi feita. |
| `userAgent` | String | A sequência do agente do usuário HTTP da solicitação do cliente. |
| `vendor` | String | O fornecedor do aplicativo ou navegador. |
| `version` | String | A versão do aplicativo ou do navegador. |
| `viewportHeight` | Número inteiro | O tamanho vertical em pixels da janela em que o evento foi exibido. Para um evento de exibição da Web, essa é a altura da janela de visualização do navegador. |
| `viewportWidth` | Número inteiro | O tamanho horizontal em pixels da janela em que o evento foi exibido. Para um evento de exibição da Web, essa é a largura da janela de visualização do navegador. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
