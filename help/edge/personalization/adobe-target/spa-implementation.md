---
title: Implementação de aplicativos de página única para o Adobe Experience Platform Web SDK
description: Saiba como criar uma implementação de aplicativo de página única (SPA) do SDK da Web da Adobe Experience Platform usando o Adobe Target.
keywords: destino;adobe destino;exibições xdm; exibições;aplicativos de página única;SPA;ciclo de vida SPA;lado do cliente;teste AB;Direcionamento de experiência;XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 13%

---

# Implementação de aplicativos de página única

O SDK da Web da Adobe Experience Platform fornece recursos avançados que fazem com que sua empresa execute personalização em tecnologias de próxima geração no lado do cliente, como aplicativos de página única (SPA).

Os sites tradicionais funcionavam em modelos de navegação de &quot;página para página&quot;, conhecidos como Aplicativos de várias páginas, em que os designs de site eram totalmente combinados com URLs e as transições de uma página da Web para outra exigiam um carregamento de página.

Aplicativos da Web modernos, como aplicativos de página única, adotaram um modelo que impulsiona o uso rápido da renderização da interface do usuário do navegador, que geralmente é independente dos recarregamentos de página. Essas experiências podem ser acionadas por interações do cliente, como rolagens, cliques e movimentos de cursor. À medida que os paradigmas da Web moderna evoluíram, a relevância dos eventos genéricos tradicionais, como um carregamento de página, para implantar a personalização e a experimentação não funciona mais.

![](assets/spa-vs-traditional-lifecycle.png)

## Benefícios do SDK da Web da plataforma para SPA

Estes são alguns benefícios de usar o SDK da Web da Adobe Experience Platform para seus aplicativos de página única:

* Capacidade de armazenar em cache todas as ofertas no carregamento da página para reduzir várias chamadas do servidor a uma única chamada de servidor.
* Melhore bastante a experiência do usuário no site, pois as ofertas são exibidas imediatamente pelo cache, sem o tempo de atraso introduzido pelas chamadas do servidor tradicional.
* Uma única linha de código e uma configuração de desenvolvedor única permitem que os profissionais de marketing criem e executem atividades A/B e Direcionamento de experiência (XT) por meio do Visual Experience Composer (VEC) no seu SPA.

## Exibições XDM e aplicativos de página única

O VEC do Adobe Target para SPA aproveita um conceito chamado Exibições: um grupo lógico de elementos visuais que juntos constituem uma experiência com o SPA. Um aplicativo de página única pode, portanto, ser considerado como uma transição entre Exibições, em vez de URLs, com base nas interações do usuário. Uma Exibição geralmente pode representar um site inteiro ou elementos visuais agrupados dentro de um site.

Para explicar melhor o que são Exibições, o exemplo a seguir usa um site de comércio eletrônico online hipotético implementado no React para explorar Exibições de exemplo.

Depois de navegar para o site inicial, uma imagem principal promove uma venda de Páscoa e os produtos mais recentes disponíveis no site. Nesse caso, uma Exibição pode ser definida para toda a tela inicial. Essa Exibição pode simplesmente ser chamada de &quot;inicial&quot;.

![](assets/example-views.png)

À medida que o cliente se torna mais interessado nos produtos que a empresa está vendendo, ele decide clicar no botão **Produtos** link. Assim como o site inicial, a totalidade do site de produtos pode ser definida como uma Exibição. Essa Exibição pode se chamar &quot;products-all&quot;.

![](assets/example-products-all.png)

Como uma Exibição pode ser definida como um site inteiro ou um grupo de elementos visuais em um site, os quatro produtos mostrados no site de produtos podem ser agrupados e considerados como uma Exibição. Essa exibição pode se chamar &quot;produtos&quot;.

![](assets/example-products.png)

Quando o cliente decidir clicar no link **Carregar mais** botão para explorar mais produtos no site, o URL do site não muda nesse caso, mas uma Exibição pode ser criada aqui para representar apenas a segunda linha de produtos mostrados. O nome da exibição pode ser &quot;products-page-2&quot;.

![](assets/example-load-more.png)

O cliente decide comprar alguns produtos do site e prossegue para a tela de finalização. No site de finalização da compra, o cliente recebe as opções de escolher a entrega normal ou a expressa. Uma Exibição pode ser qualquer grupo de elementos visuais em um site, portanto, uma Exibição pode ser criada para preferências de entrega e ser chamada de &quot;Preferências de Entrega&quot;.

![](assets/example-check-out.png)

O conceito de Exibições pode ser estendido muito além disso. Estes são apenas alguns exemplos de Exibições que podem ser definidas em um site.

## Implementação de exibições XDM

As Exibições XDM podem ser aproveitadas no Adobe Target para capacitar os profissionais de marketing a executar testes A/B e XT no SPA por meio do Visual Experience Composer. Isso requer a execução das seguintes etapas para concluir uma configuração de desenvolvedor única:

1. Instalar [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. Determine todas as Exibições XDM no aplicativo de página única que deseja personalizar.
3. Após definir as Exibições XDM, para fornecer atividades AB ou XT do VEC, implemente a variável `sendEvent()` função com `renderDecisions` definir como `true` e a Exibição XDM correspondente no Aplicativo de página única. A Exibição do XDM deve ser passada `xdm.web.webPageDetails.viewName`. Essa etapa permite que os profissionais de marketing aproveitem o Visual Experience Composer para iniciar testes A/B e XT para esses XDMs.

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
>No primeiro `sendEvent()` chamada, todas as Exibições XDM que devem ser renderizadas para o usuário final serão buscadas e armazenadas em cache. Subsequente `sendEvent()` As chamadas com Exibições XDM transmitidas serão lidas do cache e renderizadas sem uma chamada de servidor.

## `sendEvent()` exemplos de função

Esta seção descreve três exemplos mostrando como chamar a variável `sendEvent()` função no React para um SPA hipotético de comércio eletrônico.

### Exemplo 1: página inicial de teste A/B

A equipe de marketing deseja executar testes A/B em toda a página inicial.

![](assets/use-case-1.png)

Para executar testes A/B em todo o site inicial, `sendEvent()` deve ser chamado com o XDM `viewName` definir como `home`:

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

### Exemplo 2: produtos personalizados

A equipe de marketing deseja personalizar a segunda linha de produtos alterando a cor do rótulo de preço para vermelho depois que um usuário clicar **Carregar mais**.

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

### Exemplo 3: preferências de delivery do teste A/B

A equipe de marketing deseja executar um teste A/B para ver se a cor do botão é alterada de azul para vermelho quando **Entrega expressa** for selecionado pode aumentar as conversões (em vez de manter a cor do botão azul para ambas as opções de delivery).

![](assets/use-case-3.png)

Para personalizar o conteúdo no site, dependendo da preferência de entrega selecionada, uma Exibição pode ser criada para cada preferência de entrega. Quando **Entrega normal** for selecionada, a Exibição poderá ser chamada de &quot;checkout-normal&quot;. Se **Entrega expressa** for selecionada, a Exibição poderá ser chamada de &quot;checkout-express&quot;.

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

## Uso do Visual Experience Composer para SPA

Quando terminar de definir suas Exibições XDM e implementar `sendEvent()` com essas Exibições XDM transmitidas, o VEC poderá detectar essas Exibições e permitir que os usuários criem ações e modificações para atividades A/B ou XT.

>[!NOTE]
>
>Para usar o VEC para SPA, você deve instalar e ativar o [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Cromo](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) Extensão do VEC Helper.

### Painel de modificações

O painel Modificações captura as ações criadas para uma Exibição específica. Todas as ações para uma Exibição são agrupadas nessa Exibição.

![](assets/modifications-panel.png)

### Ações

Clique em uma ação para destacar o elemento no site onde esta ação será aplicada. Cada ação do VEC criada em uma Exibição tem os seguintes ícones: **Informações**, **Editar**, **Clonar**, **Mover**, e **Excluir**. Esses ícones são explicados com mais detalhes na tabela a seguir.

![](assets/action-icons.png)

| Ícone | Descrição |
|---|---|
| Informações | Exibe os detalhes da ação. |
| Editar | Permite editar as propriedades da ação diretamente. |
| Clonar | Clona a ação a uma ou mais Exibições que existem no painel Modificações ou a uma ou mais Exibições que você buscou e nas quais navegou no VEC. A ação não precisa existir necessariamente no painel Modificações .<br/><br/>**Nota:** Após a realização de uma operação de clonagem, é necessário navegar para a Exibição no VEC via Procurar para ver se a ação clonada foi uma operação válida. Se a ação não puder ser aplicada à Exibição, você verá um erro. |
| Mover | Move a ação para um Evento de carregamento de página ou qualquer outra Exibição que já existe no painel de modificações.<br/><br/>**Evento de carregamento de página:** Qualquer ação correspondente ao evento de carregamento de página é aplicada no carregamento inicial da página no aplicativo da Web. <br/><br/>**Nota:** Depois que uma operação de movimentação é feita, você deve navegar para a Exibição no VEC via Procurar para ver se a movimentação foi uma operação válida. Se a ação não puder ser aplicada à Exibição, você verá um erro. |
| Excluir | Exclui a ação. |

## Uso do VEC para exemplos de SPA

Esta seção descreve três exemplos para usar o Visual Experience Composer para criar ações e modificações para atividades A/B ou XT.

### Exemplo 1: atualizar a visualização &quot;inicial&quot;

Anteriormente neste documento, uma Exibição chamada &quot;página inicial&quot; foi definida para todo o site inicial. Agora, a equipe de marketing quer atualizar a visualização &quot;inicial&quot; das seguintes maneiras:

* Altere o **Adicionar ao carrinho** e **Curtir** para uma parte mais clara de azul. Isso deve ocorrer durante o carregamento da página, pois envolve a alteração de componentes do cabeçalho.
* Altere o **Produtos mais recentes de 2019** rótulo para **Produtos mais quentes para 2019** e altere a cor do texto para roxo.

Para fazer essas atualizações no VEC, selecione **Compor** e aplique essas alterações à exibição &quot;inicial&quot;.

![](assets/vec-home.png)

### Exemplo 2: alterar rótulos de produto

Para a visualização &quot;products-page-2&quot;, a equipe de marketing gostaria de alterar a **Preço** rótulo para **Preço de venda** e altere a cor do rótulo para vermelho.

Para fazer essas atualizações no VEC, as seguintes etapas são necessárias:

1. Selecionar **Procurar** no VEC.
2. Selecionar **Produtos** na navegação superior do site.
3. Selecionar **Carregar mais** uma vez para exibir a segunda linha de produtos.
4. Selecionar **Compor** no VEC.
5. Aplicar ações para alterar o rótulo de texto para **Preço de venda** e a cor para vermelho.

![](assets/vec-products-page-2.png)

### Exemplo 3: personalizar o estilo de preferência do delivery

As exibições podem ser definidas em nível granular, como um estado ou uma opção por meio de um botão de opção. Anteriormente neste documento, as Exibições eram definidas para preferências de entrega, &quot;checkout-normal&quot; e &quot;checkout-express&quot;. A equipe de marketing deseja alterar a cor do botão para a exibição &quot;checkout-express&quot;.

Para fazer essas atualizações no VEC, as seguintes etapas são necessárias:

1. Selecionar **Procurar** no VEC.
2. Adicione produtos ao carrinho no site.
3. Selecione o ícone do carrinho no canto superior direito do site.
4. Selecionar **Confira o pedido**.
5. Selecione o **Entrega expressa** botão de opção em **Preferências de entrega**.
6. Selecionar **Compor** no VEC.
7. Altere o **Pagamento** cor do botão para vermelho.

>[!NOTE]
>
>A exibição &quot;checkout-express&quot; não aparece no painel Modificações até que a variável **Entrega expressa** botão de opção estiver selecionado. Isso ocorre porque a variável `sendEvent()` é executada quando a variável **Entrega expressa** O botão de opção está selecionado, portanto, o VEC não está ciente da Exibição &quot;checkout-express&quot; até que o botão de opção seja selecionado.

![](assets/vec-delivery-preference.png)
