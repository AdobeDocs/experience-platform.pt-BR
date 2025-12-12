---
title: Visão geral da extensão do Adobe Target
description: Saiba mais sobre a extensão de tag para o Adobe Target na Adobe Experience Platform.
exl-id: b1c5e25b-42ea-4835-b2d4-913fa2536e77
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 93%

---

# Visão geral da extensão do Adobe Target

Use essa referência para obter informações sobre as opções disponíveis ao usar esta extensão para criar uma regra.

## Configurar a extensão do Adobe Target

>[!IMPORTANT]
>
> A extensão do Adobe Target requer at.js. Não é compatível com mbox.js.

Se a extensão do Adobe Target ainda não estiver instalada, abra a propriedade, selecione **[!UICONTROL Extensions > Catalog]**, passe o mouse sobre a extensão do Target e selecione **[!UICONTROL Install]**.

Para configurar a extensão, abra a guia [!UICONTROL Extensions], passe o mouse sobre a extensão e selecione **[!UICONTROL Configure]**.

![](../../../images/ext-target-config.png)

### Configurações do at.js

Todas as suas configurações do at.js, com exceção do Tempo-limite, são automaticamente recuperadas da configuração do at.js na interface do usuário do Target. A extensão recupera apenas as configurações da interface do usuário do Target quando adicionada pela primeira vez para que todas as configurações sejam gerenciadas na interface do usuário se forem necessárias atualizações adicionais.

As opções de configuração disponíveis são as seguintes:

#### Código do cliente

O código de cliente é o identificador de conta do Target. Isso deve ser quase sempre deixado como o valor padrão.

Pode ser alterado usando elementos de dados.

#### ID da organização

Essa ID vincula sua implementação à sua conta da Adobe Experience Cloud. Isso deve ser quase sempre deixado como o valor padrão.

Pode ser alterado usando elementos de dados.

#### Nome da mBox global

Mostra o nome da solicitação global do Target. Por padrão, esse nome é target-global-mbox, a menos que você tenha alterado o nome na interface do usuário do Target antes de adicionar a extensão.

Pode ser alterado usando elementos de dados.

#### Domínio do servidor

O domínio para onde as solicitações do Target são enviadas. Isso deve ser quase sempre deixado como o valor padrão.

#### Domínio cruzado

Determina onde o Target define cookies nos navegadores.

* **Desabilitado:** define os cookies somente no domínio próprio. Essa é a configuração usual.
* **Habilitado:** define cookies tanto no domínio primário como no domínio do Target de terceiros (o &quot;Domínio de servidor&quot;).

#### Tempo-limite (ms)

Se a resposta do Target não for recebida dentro do período definido, a solicitação expirará e o conteúdo padrão será exibido. Ainda há tentativas de solicitações adicionais durante a sessão do visitante. O padrão é 3000 ms, que pode ser diferente do tempo-limite configurado na interface do usuário do Target.

Para obter mais informações sobre como funciona a configuração de Tempo-limite, consulte a [ajuda do Adobe Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=pt_BR).

#### Outras configurações do at.js disponíveis na interface do usuário do Target

Várias configurações disponíveis na página [!UICONTROL Edit at.js settings] da interface do usuário do Target não fazem parte da extensão do Target. Aqui estão soluções alternativas:

* Criar mBox global automaticamente - Esta configuração é substituída pela ação Acionar mBox global na extensão do Target.
* Cabeçalho da biblioteca - Essa configuração não faz parte da extensão do Target. Coloque o código que precisa ser carregado antes do at.js em uma ação Extensão principal > Código personalizado antes de usar a ação Carregar Target.
* Rodapé da biblioteca - Essa configuração não faz parte da extensão do Target. Coloque o código que precisa ser carregado após o at.js em uma ação Extensão principal > Código personalizado após usar a ação Carregar Target.

## Tipos de ação da extensão do Target

Esta seção descreve os tipos de ação disponíveis na extensão do Target.

A extensão do Target fornece as seguintes ações no trecho Then de uma regra:

### Carregar Target

Adicione essa ação à sua regra de tag quando fizer sentido carregar o Target no contexto da regra. Isso carrega a biblioteca do at.js na página. Na maioria das implementações, o Target deve ser carregado em todas as páginas do site.

Nenhuma configuração é necessária.

### Adicionar parâmetros de mbox

Adicione parâmetros a todas as solicitações de mBox. A ação Carregar Target deve ser usada anteriormente.

1. Especifique o nome e o valor de qualquer parâmetro que desejar adicionar.
1. Selecione o ícone de **sinal de mais (+)** para adicionar parâmetros.

### Adicionar parâmetros globais de mbox

Adicione parâmetros somente às solicitações globais de mbox. A ação Carregar Target deve ser usada anteriormente.

1. Especifique o nome e o valor de qualquer parâmetro que desejar adicionar.
1. Selecione o ícone de **sinal de mais (+)** para adicionar parâmetros.

### Acionar mbox global

Acione o mbox global na sua página. A ação Carregar Target deve ser usada anteriormente.

Especifique se deseja habilitar a ocultação de corpo para evitar oscilação e o estilo usado ao ocultar seu elemento de corpo.

As opções disponíveis são as seguintes:

* **Ocultação de corpo:** você pode habilitar ou desabilitar essa configuração. O valor padrão é Habilitado, o que significa que o HTML BODY está oculto.
* **Estilo oculto de corpo:** o valor padrão é `body{opacity:0}`. Esse valor pode ser alterado para algo diferente, como `body{display:none}`.

Para obter mais informações, consulte a [documentação de ajuda online do Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html?lang=pt_BR).

## Implantação básica do Adobe Target

Depois que a extensão do Target estiver instalada, será necessária pelo menos uma regra para implantá-la corretamente. Primeiro, é preciso carregar a biblioteca do Target (at.js), especificar os parâmetros que você deseja usar com a mBox global e acionar a mBox global.

Uma regra do Target com esta implementação básica parece com o seguinte:

![](../../../images/basic_target_implementation.png)

Após salvar essa regra, será necessário adicioná-la a uma Biblioteca e criar/implantar para testar o comportamento.

## Extensão do Adobe Target com uma implantação assíncrona

As tags podem ser implantadas de forma assíncrona. Se você estiver carregando a biblioteca de tags de forma assíncrona com o Target inserido, o Target também será carregado de forma assíncrona. Esse cenário é totalmente suportado, mas há uma consideração adicional que deve ser tratada.

Nas implantações assíncronas, a página pode concluir a renderização do conteúdo padrão antes que a biblioteca do Target seja totalmente carregada e tenha realizado a troca de conteúdo. Isso pode levar ao que é conhecido como &quot;oscilação&quot;, em que o conteúdo padrão é exibido brevemente antes de ser substituído pelo conteúdo personalizado especificado pelo Target. Para evitar essa oscilação, sugerimos usar um trecho pré-ocultado e carregar o pacote de tag assíncrono para evitar oscilação de conteúdo.

Estas são algumas coisas que devem ser lembradas ao usar o trecho pré-ocultação:

* O trecho deve ser adicionado antes do carregamento do código incorporado do cabeçalho da tag.
* Esse código não pode ser gerenciado por tags. Portanto, deve ser adicionado diretamente à página.
* A página será exibida quando o primeiro dos seguintes eventos ocorrer:
   * Quando a resposta do mbox global for recebida
   * Quando a solicitação do mbox global expira
   * Quando o trecho atingir o tempo limite
* A ação &quot;Acionar mBox global&quot; deve ser usada em todas as páginas usando o trecho pré-ocultação para minimizar a duração da pré-ocultação.

O trecho de código de pré-ocultação é o seguinte e pode ser minimizado. As opções configuráveis estão no final:

```javascript
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Por padrão, o trecho oculta previamente todo o HTML BODY. Em alguns casos, você pode querer ocultar previamente apenas certos elementos de HTML e não a página inteira. Você pode conseguir isso personalizando o parâmetro de estilo. Substitua por algo que oculta apenas regiões específicas da página.

Por exemplo, você tem duas regiões identificadas por IDs, contêiner-1 e contêiner-2, o estilo poderá ser substituído pelo seguinte:

```css
#container-1, #container-2 {opacity: 0 !important}
```

Em vez do padrão:

```css
body {opacity: 0 !important}
```

Por padrão, o trecho expira em 3000 ms ou 3 segundos. Esse valor pode ser personalizado.
