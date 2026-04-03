---
title: Compartilhar identidade entre domínios
description: Mantenha a continuidade da identidade entre os domínios pertencentes à sua organização para melhorar a personalização e os relatórios.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Compartilhar identidade entre domínios

Quando os visitantes se movem entre domínios pertencentes à sua organização, cada domínio mantém sua própria identidade de visitante por padrão. Sem uma entrega explícita, um visitante que clicar de um de seus domínios para outro é tratado como uma pessoa nova e desconhecida no site de destino. Esse tipo de relatório de fragmentos de implementação e reinicia a personalização.

O compartilhamento de identidade entre domínios resolve esse problema, anexando um parâmetro de sequência de consulta `adobe_mc` à URL de destino quando um visitante clica em um link ou é redirecionado. Esse parâmetro carrega a [Experience Cloud ID (ECID)](./overview.md) do visitante, a ID da organização e um carimbo de data e hora. Quando a página de destino é carregada com um parâmetro `adobe_mc` válido, o Web SDK o lê automaticamente e aplica a identidade entregue em sua primeira solicitação Edge Network, para que ambos os domínios compartilhem o mesmo visitante. O parâmetro `adobe_mc` expira após cinco minutos, portanto, a página de destino deve ser carregada imediatamente após o redirecionamento.

Este caso de uso abrange o compartilhamento de identidade entre sites em diferentes domínios. Se você deseja passar a identidade de um aplicativo móvel para um WebView ou página da Web móvel, use o [compartilhamento de identidade de dispositivo móvel para Web](./mobile-to-web.md).

## Pré-requisitos

Antes de começar, verifique se sua implementação atende aos seguintes requisitos:

* O **Web SDK**: [Web SDK](/help/collection/js/js-overview.md) versão **2.11.0 ou posterior**, ou a extensão de marca Web SDK, está instalado nos domínios de origem e de destino.
* **Configuração correspondente**: todos os domínios participantes usam o mesmo [`orgId`](../js/commands/configure/orgid.md) ao configurar o Web SDK.
* **Controle de URL**: seu código controla os links ou redirecionamentos entre domínios para que você possa anexar parâmetros da cadeia de caracteres de consulta à URL de destino.

## Implementar compartilhamento entre domínios

Você deve configurar o compartilhamento de identidade em cada domínio que atue como uma origem em uma transferência entre domínios. Se os visitantes puderem navegar em ambas as direções entre dois domínios, configure ambos os domínios como fontes.

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

Use o comando [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) para anexar o parâmetro `adobe_mc` a links externos. O exemplo a seguir escuta a cliques em elementos de ancoragem e anexa identidade a qualquer link que aponte para um domínio desejado:

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Extensão de tag do Web SDK]

Use a ação [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) para anexar o parâmetro `adobe_mc` a links de saída. É possível criar uma regra com as seguintes condições para alcançar o comportamento desejado:

1. **Evento**: defina a extensão como **[!UICONTROL Core]** e o tipo de evento como **[!UICONTROL Click]**. Em **[!UICONTROL Elements matching the CSS selector]**, digite `a[href]`.
2. **Condição**: defina a extensão como **[!UICONTROL Core]** e o tipo de condição como **[!UICONTROL Value Comparison]**. Defina **[!UICONTROL Left Operand]** como `%this.hostname%`, **[!UICONTROL Operator]** como **[!UICONTROL Matches Regex]** e **[!UICONTROL Right Operand]** como uma expressão regular que corresponda a seus domínios de destino (por exemplo, `example\.com$|example\.org$`).
3. **Ação**: Defina a extensão como **[!UICONTROL Adobe Experience Platform Web SDK]** e o tipo de ação como **[!UICONTROL Redirect with identity]**.

>[!ENDTABS]

## Receber identidade no domínio de destino

Nenhum código adicional é necessário no domínio de destino. Quando o Web SDK está presente na página e a URL contém um parâmetro `adobe_mc` válido, o SDK extrai automaticamente a ECID e a aplica ao mapa de identidade do visitante em sua primeira solicitação do Edge Network.

Verifique se o domínio de destino atende às seguintes condições:

* A extensão de tag do Web SDK ou Web SDK está instalada e configurada com o mesmo [`orgId`](../js/commands/configure/orgid.md) que o domínio de origem. Você pode usar a biblioteca da JavaScript e a extensão de tag da Web SDK alternadamente entre domínios, desde que eles compartilhem o mesmo `orgId`.
* A página carrega e envia sua primeira solicitação Edge Network dentro de **cinco minutos** do redirecionamento, antes que o parâmetro `adobe_mc` expire.
