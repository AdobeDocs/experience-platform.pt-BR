---
title: Compartilhamento de ID de dispositivo móvel para Web e entre domínios
description: Saiba como manter IDs de visitante móveis em propriedades da Web e entre domínios
keywords: Identidade;móvel;id;compartilhamento;domínio;domínio cruzado;sdk;plataforma;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Compartilhamento de ID de dispositivo móvel para Web e entre domínios

## Visão geral

O SDK da Web da Adobe Experience Platform oferece suporte a recursos de compartilhamento de ID de visitante que permitem aos clientes fornecer experiências personalizadas com mais precisão, entre aplicativos móveis e conteúdo da Web móvel, e entre domínios.

## Casos de uso {#use-cases}

### Forneça personalização consistente entre aplicativos para dispositivos móveis e sites para dispositivos móveis

Uma empresa de roupas quer personalizar a experiência de seus clientes com base em seus interesses e manter a personalização precisa em um aplicativo móvel que também carrega WebViews. Ao usar o recurso de compartilhamento de ID de dispositivo móvel para Web, eles podem garantir que as ofertas mais precisas sejam apresentadas aos clientes, usando o mesmo identificador de visitante no aplicativo e o conteúdo da Web móvel ao passar o [!DNL ECID] ao URL da internet móvel.

### Oferecer personalização consistente entre domínios

Um varejista com várias lojas online deseja personalizar a experiência do comprador em seus domínios, com base nos interesses do cliente. Usando o recurso de compartilhamento de ID entre domínios do SDK da Web, o varejista pode fornecer ofertas precisas com base nos interesses do cliente em todos os domínios.

### Melhorar os relatórios de atividade do visitante

Um varejista de tecnologia deseja melhorar o relatório de atividades do visitante com informações sobre quando seus visitantes mudam do aplicativo móvel para o site móvel ou para outros domínios. Usando o recurso de compartilhamento de ID entre domínios do SDK da Web, a equipe de marketing pode rastrear com precisão os visitantes em suas propriedades da Web e gerar relatórios de atividades.

## Pré-requisitos {#prerequisites}

Para usar o compartilhamento de ID móvel para Web e entre domínios, você deve usar [!DNL Web SDK] versão 2.11.0 ou posterior.

Para implementações móveis da Rede de borda, esse recurso é compatível com o [Identidade da rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) extensão a partir da versão 1.1.0 (iOS e Android).

Esse recurso também é compatível com o [!DNL VisitorAPI.js] versão 1.7.0 ou posterior.

## Compartilhamento de ID de dispositivo móvel para Web {#mobile-to-web}

Use o `getUrlVariables` API do [Identidade da rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) extensão para recuperar os identificadores como parâmetros de consulta e anexá-los ao seu URL ao abrir [!DNL webViews].

Nenhuma configuração adicional é necessária para que o SDK da Web aceite `ECID` valores na sequência de consulta.

O parâmetro da cadeia de caracteres de consulta inclui:

* `MCID`: A ID do Experience Cloud (`ECID`)
* `MCORGID`: O EXPERIENCE CLOUD `orgID` que deve corresponder ao `orgID` configurado no [!DNL Web SDK].
* `TS`: um parâmetro de carimbo de data e hora que não pode ter mais de cinco minutos.


O compartilhamento do Mobile para a Web ID usa o `adobe_mc` parâmetro. Quando a variável `adobe_mc` estiver presente e for válido, a variável `ECID` da sequência de consulta é automaticamente adicionado ao mapa de identidade na primeira solicitação feita à Rede de borda. Todas as interações subsequentes da Rede de borda usarão essa `ECID`.

Para obter mais informações sobre como transmitir IDs de visitante de um aplicativo móvel para um WebView, consulte a documentação em [manipulação de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Compartilhamento de ID entre domínios {#cross-domain-sharing}

Para compartilhamento de ID entre domínios, o SDK da Web versão 2.11.0 adiciona suporte para o `appendIdentityToUrl` comando. Quando usado, esse comando gera o `adobe_mc` parâmetro da sequência de consulta.

O comando aceita um objeto com uma propriedade, `url`e retorna um objeto com a propriedade `url`.

Esse comando não aguarda por nenhuma atualização de consentimento. Se o consentimento não foi fornecido, o URL é retornado inalterado.

Se um `ECID` não for fornecida, a variável `/acquire` O endpoint será chamado para gerar um `ECID`.

Veja abaixo um exemplo de como um cliente pode implementar o compartilhamento de ID entre domínios em seu site.

Esse código adiciona um ouvinte de eventos para todos os cliques na página e se o clique estava em um link para um domínio correspondente (neste caso, `adobe.com` ou `behance.com`), adiciona a identidade à URL e redireciona o usuário para lá.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## Uso da extensão Tags {#tags-extension}

Semelhante ao uso de [!DNL Web SDK], não há nenhuma configuração adicional necessária no [!DNL Tags] extensão para usar identidades transmitidas pelo URL.

Para usar o compartilhamento de ID móvel para Web e entre domínios por meio da extensão Tags, você deve usar a versão 2.12.0 ou posterior da extensão Tags.

Para compartilhar identidades da página atual com outros domínios, há uma nova ação disponível no [!DNL Web SDK] [!DNL Tags] extensão. Esta ação foi projetada para ser usada com um **[!UICONTROL Núcleo - Clique]** tipo de evento e uma condição de comparação de valor.

Siga as etapas descritas [aqui](../../tags/ui/managing-resources/rules.md) para criar uma regra com a seguinte configuração:

* [!UICONTROL Configuração de evento]:
   * **[!UICONTROL Extensão: principal]**
   * **[!UICONTROL Tipo de evento: clique]**
   * Selecionar **[!UICONTROL Quando o usuário clica em > elementos específicos]**
   * Digite o **[!UICONTROL Seletor]**: `a[href]`. Esse evento será acionado sempre que uma tag de âncora for clicada na página com um `href` propriedade.

     ![Imagem da interface do usuário mostrando a configuração do evento com as configurações descritas acima](assets/id-sharing-event-configuration.png)

* [!UICONTROL Configuração de condição]
   * **[!UICONTROL Tipo de lógica]**: [!UICONTROL Regular]
   * **[!UICONTROL Extensão]**: [!UICONTROL Núcleo]
   * **[!UICONTROL Tipo de condição]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Operando esquerdo]**: [!UICONTROL `%this.hostname%`]. Este é um elemento de dados especial que funciona com [!UICONTROL Núcleo - Clique] e resolve para o nome do host do link que foi clicado.
   * **[!UICONTROL Operador]**: [!UICONTROL Corresponde a Regex]
   * **[!UICONTROL Operando Direito]**: digite uma expressão regular que corresponda aos domínios com os quais você deseja compartilhar identidades. Por exemplo, para corresponder links com nomes de host que terminam com `adobe.com` ou `behance.com`, use esta expressão regular: `behance.com$|adobe.com$`. A página vinculada precisa ter a [!DNL Web SDK] ou [!DNL Visitor ID] instalado para aceitar a identidade.

     ![Imagem da interface do usuário mostrando a configuração de condição com as configurações descritas acima](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Configuração de ação]
   * **[!UICONTROL Extensão]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo de ação]**: [!UICONTROL Redirecionar com identidade]
   * **[!UICONTROL Instância]**: selecione a instância. Na maioria dos casos, você terá apenas uma instância configurada. Se você tiver várias instâncias, selecione aquela com a identidade que deseja compartilhar.

     ![Imagem da interface do usuário mostrando a configuração da ação com as configurações descritas acima](assets/id-sharing-action-configuration.png)

A variável **[!UICONTROL Redirecionar com identidade]** Essa ação fará com que o navegador pare de navegar até o link. Em seguida, chamará o `appendIdentityToUrl` no [!DNL Web SDK] instância.

Por fim, redireciona o usuário para a variável [!DNL URL] com o `adobe_mc` parâmetro da sequência de consulta anexado.
