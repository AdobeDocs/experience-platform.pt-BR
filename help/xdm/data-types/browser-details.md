---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;navegador;detalhes do navegador;tipo de dados;tipo de dados;tipo de dados;
solution: Experience Platform
title: Tipo de dados Detalhes do navegador
description: Saiba mais sobre o tipo de dados XDM de Detalhes do navegador.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 27%

---

# [!UICONTROL Tipo de dados de detalhes do navegador]

[!UICONTROL Detalhes do navegador] é um tipo de dados XDM padrão que descreve detalhes relacionados a um navegador ou aplicativo.

![](../images/data-types/browser-details.png){width=450}

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `acceptLanguage` | String | Uma marca de idioma IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booleano | Indica se as configurações do usuário permitem a gravação de cookies. |
| `javaEnabled` | Booleano | Indica se o Java foi habilitado no dispositivo em que a observação foi feita. |
| `javaScriptEnabled` | Booleano | Indica se o JavaScript foi habilitado no dispositivo do qual a observação foi feita. |
| `javaScriptVersion` | String | A versão do JavaScript compatível durante a observação. |
| `javaVersion` | String | A versão do Java compatível com a observação. |
| `name` | String | O nome do aplicativo ou navegador. |
| `quicktimeVersion` | String | A versão do Apple Quicktime compatível durante a observação. |
| `thirdPartyCookiesEnabled` | Booleano | Indica se cookies de terceiros foram habilitados no dispositivo do qual a observação foi feita. |
| `userAgent` | String | A string do agente do usuário HTTP da solicitação do cliente. |
| `vendor` | String | O fornecedor do aplicativo ou navegador. |
| `version` | String | A versão do aplicativo ou navegador. |
| `viewportHeight` | Número inteiro | O tamanho vertical em pixels da janela em que o evento foi exibido. Para um evento de visualização da Web, essa é a altura da janela de visualização do navegador. |
| `viewportWidth` | Número inteiro | O tamanho horizontal em pixels da janela em que o evento foi exibido. Para um evento de visualização da Web, essa é a largura da janela de visualização do navegador. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
