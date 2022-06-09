---
title: Compartilhamento de IDs entre dispositivos móveis e domínios
description: Saiba como persistir as IDs de visitante de dispositivos móveis para propriedades da Web e entre domínios
keywords: Identidade, móvel, id, compartilhamento, domínio, entre domínios, sdk, plataforma;
source-git-commit: 55e28f749741c653a230b42fabf5a047ba8c7d01
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Compartilhamento de IDs entre dispositivos móveis e domínios

## Visão geral

O SDK da Web da Adobe Experience Platform é compatível com os recursos de compartilhamento de ID de visitante que permitem que os clientes forneçam experiências personalizadas com mais precisão, entre aplicativos móveis e conteúdo da Web móvel e entre domínios.

## Casos de uso {#use-cases}

### Oferecer personalização consistente entre aplicativos móveis e sites móveis

Uma empresa de roupas deseja personalizar a experiência de seus clientes com base em seus interesses e manter a personalização precisa em um aplicativo móvel que também carrega WebViews. Ao usar o recurso de compartilhamento de IDs entre dispositivos móveis da Web, é possível garantir que as ofertas mais precisas sejam apresentadas aos clientes, usando o mesmo identificador de visitante no aplicativo e no conteúdo da Web móvel, passando a variável [!DNL ECID] para o URL da Web móvel.

### Fornecer personalização consistente entre domínios

Um varejista com várias lojas online deseja personalizar a experiência do comprador em seus domínios, com base nos interesses do cliente. Usando o recurso de compartilhamento de ID entre domínios do SDK da Web, o varejista pode fornecer ofertas precisas com base nos interesses do cliente, em todos os domínios.

### Aprimorar os relatórios de atividade do visitante

Um varejista de tecnologia deseja melhorar o relatório de atividade do visitante com informações sobre quando seus visitantes mudam do aplicativo móvel para o site móvel ou para outros domínios. Usando o recurso de compartilhamento de ID entre domínios do SDK da Web, a equipe de marketing pode rastrear com precisão os visitantes em suas propriedades da Web e gerar relatórios de atividade.

## Pré-requisitos {#prerequisites}

Para usar o compartilhamento de IDs entre domínios e entre dispositivos móveis, é necessário atualizar para [!DNL Web SDK] versão 2.11.0 ou posterior.

Para implementações móveis de rede de borda, esse recurso é compatível com o [Identidade da rede Edge](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) extensão a partir da versão 1.1.0 (iOS e Android).

## Compartilhamento de IDs da Web para dispositivos móveis {#mobile-to-web}

Use o `getUrlVariables` API do [Identidade da rede Edge](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) para recuperar os identificadores como parâmetros de consulta e anexá-los ao URL ao abrir [!DNL webViews].

Nenhuma configuração adicional é necessária para o SDK da Web aceitar `ECID` na string de consulta.

O parâmetro da string de consulta inclui:

* `MCID`: A ID do Experience Cloud (`ECID`)
* `MCORGID`: O Experience Cloud `orgID` que deve corresponder ao `orgID` configurado no [!DNL Web SDK].
* `TS`: Um parâmetro de carimbo de data e hora que não pode ter mais de cinco minutos.


O compartilhamento de IDs de dispositivo móvel para Web usa o `adobe_mc` parâmetro. Quando a variável `adobe_mc` está presente e é válido, a variável `ECID` A partir da string de consulta é automaticamente adicionada ao mapa de identidade na primeira solicitação feita para a Edge Network. Todas as interações subsequentes da rede de borda usarão essa função `ECID`.

Para obter mais informações sobre como transmitir IDs de visitante de um aplicativo móvel para um WebView, consulte a documentação em [manuseio de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Compartilhamento de ID entre domínios {#cross-domain-sharing}

Para compartilhamento de ID entre domínios, o SDK da Web versão 2.11.0 adiciona suporte para a variável `appendIdentityToUrl` comando. Quando usado, esse comando gera a variável `adobe_mc` parâmetro da string de consulta.

O comando aceita um objeto com uma propriedade, `url`e retorna um objeto com a propriedade `url`.

Este comando não espera por nenhuma atualização de consentimento. Se o consentimento não tiver sido fornecido, o URL retornará inalterado.

Se uma `ECID` não for fornecida, a variável `/acquire` endpoint será chamado para gerar um `ECID`.

Veja abaixo um exemplo de como um cliente pode implementar o compartilhamento de ID entre domínios no site.

Esse código adiciona um ouvinte de eventos para todos os cliques na página e se o clique estava em um link para um domínio correspondente (nesse caso, `adobe.com` ou `behance.com`), adiciona a identidade ao URL e redireciona o usuário lá.

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

Semelhante ao uso da variável [!DNL Web SDK], não é necessária uma configuração adicional no [!DNL Tags] para usar identidades transmitidas pelo URL.

Para usar o compartilhamento de IDs entre domínios e dispositivos móveis na Web por meio da extensão de Tags, é necessário usar a versão 2.12.0 ou posterior da extensão de Tags.

Para compartilhar identidades da página atual com outros domínios, há uma nova ação disponível no [!DNL Web SDK] [!DNL Tags] extensão. Essa ação foi projetada para ser usada com uma **[!UICONTROL Principal - Clique]** tipo de evento e uma condição de comparação de valor.

Siga as etapas descritas [here](../../tags/ui/managing-resources/rules.md) para criar uma regra com a seguinte configuração:

* [!UICONTROL Configuração de evento]:
   * **[!UICONTROL Extensão: principal]**
   * **[!UICONTROL Tipo de evento: Clique em]**
   * Selecionar **[!UICONTROL Quando o usuário clica em > elementos específicos]**
   * Digite no **[!UICONTROL Seletor]**: `a[href]`. Esse evento será acionado sempre que uma tag de âncora for clicada na página com uma `href` propriedade.

      ![Imagem da interface do usuário que mostra a configuração do evento com as configurações descritas acima](assets/id-sharing-event-configuration.png)

* [!UICONTROL Configuração de condição]
   * **[!UICONTROL Tipo lógico]**: [!UICONTROL Regular]
   * **[!UICONTROL Extensão]**: [!UICONTROL Núcleo]
   * **[!UICONTROL Tipo de condição]**: [!UICONTROL Comparação de valores]
   * **[!UICONTROL Operando esquerdo]**: [!UICONTROL `%this.hostname%`]. Este é um elemento de dados especial que funciona com [!UICONTROL Principal - Clique] e resolve para o nome do host do link que foi clicado.
   * **[!UICONTROL Operador]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL Operando à direita]**: Digite uma expressão regular que corresponda aos domínios com os quais você deseja compartilhar identidades. Por exemplo, para corresponder links com nomes de host que terminam com `adobe.com` ou `behance.com`, use essa expressão regular: `behance.com$|adobe.com$`. A página vinculada precisa ter a variável [!DNL Web SDK] ou [!DNL Visitor ID] instalado para aceitar a identidade.

      ![Imagem da interface do usuário que mostra a configuração da condição com as configurações descritas acima](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Configuração de ação]
   * **[!UICONTROL Extensão]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo de ação]**: [!UICONTROL Redirecionar com identidade]
   * **[!UICONTROL Instância]**: Selecione a instância . Na maioria dos casos, você terá apenas uma instância configurada. Se você tiver várias instâncias, selecione aquela com a identidade que deseja compartilhar.

      ![Imagem da interface do usuário que mostra a configuração de ação com as configurações descritas acima](assets/id-sharing-action-configuration.png)

O **[!UICONTROL Redirecionar com identidade]** ação impedirá que o navegador navegue até o link. Em seguida, ele chamará a função `appendIdentityToUrl` no método [!DNL Web SDK] instância.

Por fim, ele redireciona o usuário para o [!DNL URL] com o `adobe_mc` parâmetro da string de consulta anexado.
