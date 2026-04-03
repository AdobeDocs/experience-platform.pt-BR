---
title: Compartilhar identidade de aplicativos móveis para web/WebViews móveis
description: Transmita a identidade de um aplicativo móvel para um conteúdo da Web móvel ou WebView, para que os relatórios e a personalização possam continuar no contexto da Web.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Compartilhar identidade de aplicativos móveis para web/WebViews móveis

Quando um visitante muda de um aplicativo móvel para um WebView ou página da Web móvel, o aplicativo e os contextos da Web mantêm sua própria identidade. Sem uma entrega explícita, a experiência da Web trata o visitante como uma pessoa nova e desconhecida, que fragmenta os relatórios e reinicia a personalização.

O compartilhamento de identidade móvel para Web resolve isso transmitindo a [Experience Cloud ID (ECID)](./overview.md) do visitante do aplicativo móvel para o destino da Web por meio de um parâmetro de sequência de consulta `adobe_mc`. O parâmetro carrega a ECID, a ID da organização da Experience Cloud e um carimbo de data e hora. Quando o destino da Web é carregado com um parâmetro `adobe_mc` válido, o Web SDK o lê automaticamente e aplica a identidade entregue em sua primeira solicitação do Edge Network, para que ambos os contextos compartilhem o mesmo visitante.

Use esse padrão quando o aplicativo móvel abrir um WebView ou uma página da Web móvel que sua organização controla e você quiser que a atividade do aplicativo e da Web permaneçam vinculadas ao mesmo visitante. Se a sua meta é a continuidade de identidade entre sites em domínios diferentes, use o [compartilhamento entre domínios](cross-domain-sharing.md).

## Pré-requisitos

Antes de começar, verifique se sua implementação atende aos seguintes requisitos:

* **Aplicativo móvel**: o Adobe Experience Platform Mobile SDK com a [Identidade da extensão do Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) versão **1.1.0 ou posterior** (iOS e Android).
* **Destino da Web**: o [Web SDK](/help/collection/js/js-overview.md) versão **2.11.0 ou posterior** ou a extensão de marca do Web SDK.
* **Controle de URL**: seu código controla a URL que o aplicativo passa para o WebView ou o navegador para que você possa acrescentar parâmetros de cadeia de caracteres de consulta a ele.
* **Configuração correspondente**: a mesma ID de organização da Experience Cloud está configurada nas implementações para dispositivos móveis e Web.

## Recuperar identidade do aplicativo móvel {#retrieve-identity}

Use a API [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) da extensão Identity for Edge Network para recuperar a identidade do visitante como uma cadeia de caracteres de consulta. Você pode anexar essa string ao URL antes de abrir o WebView ou o navegador.

A string retornada contém os seguintes parâmetros codificados por URL:

| Parâmetro | Descrição |
| --- | --- |
| `MCID` | A Experience Cloud ID (ECID). |
| `MCORGID` | Sua ID da organização da Experience Cloud. Esse parâmetro deve corresponder à organização configurada no Web SDK na página de destino. |
| `TS` | Um carimbo de data e hora. O destino deve receber este valor dentro de **cinco minutos** ou a entrega será rejeitada. |

Os seguintes exemplos de código mostram como uma entrega pode ser em seu aplicativo móvel:

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Receber identidade no lado da Web {#receive-identity}

Nenhum código adicional é necessário no destino da Web. Quando o Web SDK está presente na página e a URL contém um parâmetro `adobe_mc` válido, o SDK extrai automaticamente a ECID e a aplica ao mapa de identidade do visitante na primeira solicitação do Edge Network.

Se o destino da Web usar a extensão de tag da Web SDK e você precisar redirecionar o visitante para outra página, preservando a identidade, use a ação [Redirecionar com identidade](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) para encaminhar o parâmetro `adobe_mc` para a próxima página.

>[!NOTE]
>
>O parâmetro `adobe_mc` expira após **cinco minutos**. Certifique-se de que o destino da Web carregue e envie sua primeira solicitação do Edge Network imediatamente após o URL ser aberto.
