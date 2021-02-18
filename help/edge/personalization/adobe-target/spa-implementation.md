---
title: Implementação de aplicativo de página única para o Adobe Experience Platform Web SDK
description: Saiba como criar uma implementação de aplicativo de página única (SPA) do Adobe Experience Platform Web SDK usando o Adobe Target.
keywords: público alvo;adobe público alvo;xdm visualização; visualização;aplicativos de página única;SPA;SPA ciclo de vida;lado do cliente;teste AB;AB;direcionamento de experiência;XT;VEC
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---


# Implementação de aplicativo de página única

O Adobe Experience Platform Web SDK fornece recursos avançados que equipam sua empresa para executar personalização em tecnologias de cliente da próxima geração, como aplicativos de página única (SPA).

Os sites tradicionais funcionavam em modelos de navegação de &quot;página para página&quot;, conhecidos como Aplicativos de várias páginas, em que os designs de site eram totalmente combinados com URLs e as transições de uma página da Web para outra exigiam um carregamento de página.

Aplicativos da Web modernos, como aplicativos de página única, adotaram um modelo que impulsiona o uso rápido da renderização da interface do navegador, que geralmente é independente dos recarregamentos de página. Essas experiências podem ser acionadas por interações do cliente, como rolagens, cliques e movimentos do cursor. À medida que os paradigmas da Web moderna evoluíram, a relevância dos eventos genéricos tradicionais, como uma carga de página, para implantar personalização e experimentação não funciona mais.

![](assets/spa-vs-traditional-lifecycle.png)

## Benefícios do SDK da Web da plataforma para SPA

Estes são alguns benefícios de usar o Adobe Experience Platform Web SDK para seus aplicativos de página única:

* Capacidade de armazenar em cache todas as ofertas no carregamento da página para reduzir várias chamadas do servidor a uma única chamada de servidor.
* Melhore tremendamente a experiência do usuário em seu site, pois as ofertas são mostradas imediatamente pelo cache, sem o atraso de tempo introduzido pelas chamadas tradicionais do servidor.
* Uma única linha de código e configuração única do desenvolvedor permitem que os profissionais de marketing criem e executem atividades A/B e Experience Targeting (XT) por meio do Visual Experience Composer (VEC) no seu SPA.

## Visualizações XDM e aplicativos de página única

O Adobe Target VEC para SPA aproveita um conceito chamado Visualização: um grupo lógico de elementos visuais que, juntos, formam uma experiência SPA. Um aplicativo de página única pode, portanto, ser considerado como fazendo a transição por Visualizações, em vez de URLs, com base nas interações do usuário. Uma Exibição geralmente pode representar um site inteiro ou elementos visuais agrupados dentro de um site.

Para explicar melhor o que são as Visualizações, o exemplo a seguir usa um site hipotético de comércio eletrônico implementado no React para explorar Visualizações de exemplo.

Depois de navegar até o site inicial, uma imagem principal promove uma venda de Páscoa, bem como os produtos mais recentes disponíveis no site. Nesse caso, uma Visualização poderia ser definida para a tela inicial inteira. Esta Visualização poderia simplesmente ser chamada de &quot;lar&quot;.

![](assets/example-views.png)

À medida que o cliente se interessa mais pelos produtos que a empresa está vendendo, ele decide clicar no link **Produtos**. Assim como o site inicial, a totalidade do site de produtos pode ser definida como uma Exibição. Esta Visualização poderia ser chamada de &quot;products-all&quot;.

![](assets/example-products-all.png)

Como uma Visualização pode ser definida como um site inteiro ou um grupo de elementos visuais em um site, os quatro produtos mostrados no site de produtos podem ser agrupados e considerados uma Visualização. Esta visualização poderia ser chamada de &quot;produtos&quot;.

![](assets/example-products.png)

Quando o cliente decide clicar no botão **Carregar mais** para explorar mais produtos no site, o URL do site não é alterado nesse caso, mas uma Visualização pode ser criada aqui para representar apenas a segunda linha de produtos mostrados. O nome da Visualização pode ser &quot;products-page-2&quot;.

![](assets/example-load-more.png)

O cliente decide comprar alguns produtos do site e vai para a tela de finalização. No site de checkout, o cliente recebe opções para escolher o delivery normal ou o delivery expresso. Uma Visualização pode ser qualquer grupo de elementos visuais em um site, de modo que uma Visualização pode ser criada para preferências de delivery e ser chamada de &quot;Preferências de Delivery&quot;.

![](assets/example-check-out.png)

O conceito de Visualizações pode ser muito mais alargado do que isso. Estes são apenas alguns exemplos de Visualizações que podem ser definidas em um site.

## Implementando Visualizações XDM

As Visualizações XDM podem ser aproveitadas no Adobe Target para permitir que os profissionais de marketing executem testes A/B e XT no SPA por meio do Visual Experience Composer. Isso requer a execução das seguintes etapas para concluir uma configuração única do desenvolvedor:

1. Instalar [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Determine todas as Visualizações XDM em seu aplicativo de página única que você deseja personalizar.
3. Depois de definir as Visualizações XDM, para fornecer atividades AB ou XT VEC, implemente a função `sendEvent()` com `renderDecisions` definida como `true` e a Visualização XDM correspondente em seu Aplicativo de Página Única. A Visualização XDM deve ser transmitida em `xdm.web.webPageDetails.viewName`. Essa etapa permite que os profissionais de marketing aproveitem o Visual Experience Composer para iniciar testes A/B e XT para esses XDM.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>Na primeira chamada `sendEvent()`, todas as Visualizações XDM que devem ser renderizadas para o usuário final serão buscadas e armazenadas em cache. As chamadas `sendEvent()` subsequentes com Visualizações XDM enviadas serão lidas do cache e renderizadas sem uma chamada de servidor.

## `sendEvent()` exemplos de função

Esta seção descreve três exemplos que mostram como chamar a função `sendEvent()` em Reagir para uma SPA hipotética de comércio eletrônico.

### Exemplo 1: Home page de teste A/B

A equipe de marketing deseja executar testes A/B em todo o home page.

![](assets/use-case-1.png)

Para executar testes A/B em todo o site inicial, `sendEvent()` deve ser chamado com o XDM `viewName` definido como `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Exemplo 2: Produtos personalizados

A equipe de marketing deseja personalizar a segunda linha de produtos alterando a cor do rótulo de preço para vermelho depois que o usuário clicar em **Carregar mais**.

![](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Exemplo 3: Preferências do delivery de teste A/B

A equipe de marketing deseja executar um teste A/B para verificar se a alteração da cor do botão de azul para vermelho quando **Delivery Express** estiver selecionado pode aumentar as conversões (em vez de manter a cor do botão azul para ambas as opções de delivery).

![](assets/use-case-3.png)

Para personalizar o conteúdo do site, dependendo da preferência do delivery selecionada, é possível criar uma Visualização para cada preferência de delivery. Quando **Delivery normal** é selecionado, a Visualização pode ser chamada de &quot;checkout-normal&quot;. Se **Delivery expresso** estiver selecionado, a Visualização poderá ser chamada de &quot;checkout-express&quot;.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Uso do Visual Experience Composer para um SPA

Quando você terminar de definir suas Visualizações XDM e implementar `sendEvent()` com essas Visualizações XDM passadas, o VEC poderá detectar essas Visualizações e permitir que os usuários criem ações e modificações para atividades A/B ou XT.

>[!NOTE]
>
>Para usar o VEC para o seu SPA, você deve instalar e ativar a [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Extensão Auxiliar VEC.

### Painel de modificações

O painel Modificações captura as ações criadas para uma Visualização específica. Todas as ações de uma Visualização são agrupadas sob essa Visualização.

![](assets/modifications-panel.png)

### Ações

Clique em uma ação para destacar o elemento no site onde esta ação será aplicada. Cada ação VEC criada em uma Visualização tem os seguintes ícones: **Informações**, **Editar**, **Clonar**, **Mover** e **Eliminar**. Esses ícones são explicados com mais detalhes na tabela a seguir.

![](assets/action-icons.png)

| Ícone | Descrição |
|---|---|
| Informações | Exibe os detalhes da ação. |
| Editar | Permite editar as propriedades da ação diretamente. |
| Clonar | Clona a ação a uma ou mais Exibições que existem no painel Modificações ou a uma ou mais Exibições que você buscou e nas quais navegou no VEC. A ação não precisa existir necessariamente no painel Modificações .<br/><br/>**Observação:** depois que uma operação de clone é realizada, você deve navegar até a Visualização no VEC via Navegação para ver se a ação clonada era uma operação válida. Se a ação não puder ser aplicada à Exibição, você verá um erro. |
| Mover | Move a ação para um Evento de carregamento de página ou qualquer outra Exibição que já existe no painel de modificações.<br/><br/>**Evento de carregamento de página:** quaisquer ações correspondentes ao evento de carregamento de página são aplicadas ao carregamento de página inicial do aplicativo da Web. <br/><br/>**Observação:** depois que uma operação de movimentação é realizada, você deve navegar até a Visualização no VEC via Navegação para ver se a movimentação era uma operação válida. Se a ação não puder ser aplicada à Exibição, você verá um erro. |
| Excluir | Exclui a ação. |

## Uso do VEC para SPA exemplos

Esta seção descreve três exemplos de uso do Visual Experience Composer para criar ações e modificações para atividades A/B ou XT.

### Exemplo 1: Atualizar Visualização &quot;inicial&quot;

No início deste documento, uma Visualização chamada &quot;home&quot; foi definida para todo o site doméstico. Agora a equipe de marketing quer atualizar a visualização &quot;inicial&quot; das seguintes maneiras:

* Altere os botões **Adicionar ao carrinho** e **Curtir** para um compartilhamento mais claro de azul. Isso deve ocorrer durante o carregamento da página, pois envolve a alteração de componentes do cabeçalho.
* Altere a etiqueta **Produtos mais recentes para 2019** para **Produtos mais avançados para 2019** e altere a cor do texto para roxo.

Para fazer essas atualizações no VEC, selecione **Compor** e aplique essas alterações à visualização &quot;inicial&quot;.

![](assets/vec-home.png)

### Exemplo 2: Alterar etiquetas de produto

Para a Visualização &quot;products-page-2&quot;, a equipe de marketing gostaria de alterar o rótulo **Price** para **Preço de venda** e alterar a cor do rótulo para vermelho.

Para fazer essas atualizações no VEC, são necessárias as seguintes etapas:

1. Selecione **Procurar** no VEC.
2. Selecione **Produtos** na navegação superior do site.
3. Selecione **Carregar mais** uma vez para visualização na segunda linha de produtos.
4. Selecione **Compor** no VEC.
5. Aplique ações para alterar o rótulo do texto para **Preço de venda** e a cor para vermelho.

![](assets/vec-products-page-2.png)

### Exemplo 3: Personalizar estilo de preferência de delivery

Visualizações podem ser definidas em um nível granular, como um estado ou uma opção de um botão de opção. Anteriormente, neste documento, as Visualizações eram definidas para preferências de delivery, &quot;normal de finalização&quot; e &quot;expresso de finalização&quot;. A equipe de marketing deseja alterar a cor do botão para vermelho para a Visualização &quot;checkout-express&quot;.

Para fazer essas atualizações no VEC, são necessárias as seguintes etapas:

1. Selecione **Procurar** no VEC.
2. Adicione produtos ao carrinho do site.
3. Selecione o ícone do carrinho no canto superior direito do site.
4. Selecione **Finalizar seu pedido**.
5. Selecione o botão de opção **Delivery Express** em **Preferências de Delivery**.
6. Selecione **Compor** no VEC.
7. Altere a cor do botão **Pagar** para vermelha.

>[!NOTE]
>
>A Visualização &quot;checkout-express&quot; não aparece no painel Modificações até que o botão de opção **Delivery Express** seja selecionado. Isso ocorre porque a função `sendEvent()` é executada quando o botão de opção **Delivery Express** é selecionado, portanto, o VEC não está ciente da Visualização &quot;checkout-express&quot; até que o botão de opção seja selecionado.

![](assets/vec-delivery-preference.png)
