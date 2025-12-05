---
title: Visão geral da extensão de tags do Algolia
description: Saiba mais sobre a extensão Tags do Algolia no Adobe Experience Platform.
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 6eee26df3841a7829625361fc726bf59a278f867
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 1%

---

# Visão geral da extensão de marcas [!DNL Algolia]

A extensão de Tags do [!DNL Algolia] permite que os profissionais de marketing configurem facilmente regras que enviam dados de interação do usuário para o [!DNL Algolia], ajudando você a fornecer experiências de Pesquisa e Descoberta de IA mais personalizadas.

Essa extensão é alimentada por um recurso principal:

* **[!DNL Algolia]Insights**: captura e envia automaticamente eventos de interação do usuário para [!DNL Algolia], o que permite análises poderosas, experiências personalizadas e relevância de pesquisa aprimorada.

## Pré-requisitos {#prerequisites}

Você deve ter uma conta [!DNL Algolia] válida para usar esta extensão. Vá para a [[!DNL Algolia] página de inscrição](https://dashboard.algolia.com/users/sign_up) para criar uma conta caso ainda não tenha uma.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar [!DNL Algolia] ao Adobe Experience Platform, você precisará das seguintes informações:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID do aplicativo | A ID do Aplicativo pode ser encontrada na seção [Chaves de API](https://www.algolia.com/account/api-keys/all) do Painel [!DNL Algolia]. | 0ABCDEFG12 |
| Chave da API de pesquisa | Sua Chave de API de Pesquisa pode ser encontrada na seção [Chaves de API](https://www.algolia.com/account/api-keys/all) do seu Painel [!DNL Algolia]. | 1234a12345678901b1234567890c1ab1 |

## Instalar e configurar a extensão do Insights do [!DNL Algolia] {#install-configure}

Para instalar a extensão do Insights do [!DNL Algolia], navegue até [!UICONTROL Data Collection UI] e selecione **[!UICONTROL Tags]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensions]** na navegação à esquerda e, em seguida, selecione a guia **[!UICONTROL Catalog]**. Procure o cartão de [!DNL Algolia] Insights e selecione **[!UICONTROL Install]**.

![](../../../images/extensions/client/algolia/install.png)

Na visualização de configuração exibida, você deve fornecer os seguintes detalhes:

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Application ID] | Insira o [!UICONTROL Application Id] que você reuniu anteriormente na seção [detalhes de configuração](#configuration-details). |
| [!UICONTROL Search API Key] | Insira o [!UICONTROL Search API Key] que você reuniu anteriormente na seção [detalhes de configuração](#configuration-details). |
| [!UICONTROL Index Name] | O [!UICONTROL Index Name] contém os Produtos ou Conteúdo.  Este índice será usado como padrão. |
| [!UICONTROL User Token Data Element] | O elemento de dados que retornará o token do usuário. |
| [!UICONTROL Authenticated User Token Data Element] | Definir o elemento de dados que retornará o token do usuário autenticado. |
| [!UICONTROL Currency Code] | Insira o código de moeda no formato ISO-4217, como USD ou EUR. Esse campo suporta elementos de dados. |

![](../../../images/extensions/client/algolia/configure.png)

## [!DNL Algolia] tipos de ação de extensão do Insights {#action-types}

O [!DNL Algolia] oferece suporte a um conjunto de eventos padrão predefinidos, cada um com contextos e propriedades específicas. As ações disponíveis na extensão [!DNL Algolia] estão alinhadas a esses tipos de evento, facilitando a categorização e configuração dos eventos que você envia para o [!DNL Algolia] com base em seus tipos.

### Carregar Insights {#load-insights}

>[!NOTE]
>
>Na maioria dos casos, é recomendável carregar o [!DNL Algolia] Insights em cada página do site.

Adicione a ação **[!UICONTROL Load Insights]** à sua regra de tag sempre que fizer mais sentido para carregar [!DNL Algolia] Insights com base no contexto da sua regra. Esta ação carrega a biblioteca `search-insights.js` na página.

Crie uma nova regra de tag ou abra uma existente. Defina as condições de acordo com suas necessidades, selecione **[!UICONTROL Algolia]** como [!UICONTROL Extension] e selecione **[!UICONTROL Load Insights]** como [!UICONTROL Action Type].

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Insight Library Version] | A versão do Insights do [!DNL Algolia]. O padrão é `2.17.3`. |
| [!UICONTROL User Opt Out Data Element] | O Elemento de dados que captura a preferência de rastreamento do usuário. |
| [!UICONTROL Use User Token Cookie] | Marque esta caixa para permitir que [!DNL Algolia] gere um cookie de Token de Usuário. Por padrão, esta opção está definida como `true`. |

![](../../../images/extensions/client/algolia/load-insights.png)

### Clicado {#clicked}

Adicione a ação **[!UICONTROL Click]** à sua regra de marca para enviar eventos clicados para [!DNL Algolia]. Crie uma nova regra de tag ou abra uma existente. Defina as condições de acordo com suas necessidades, selecione **[!UICONTROL Algolia]** como [!UICONTROL Extension] e selecione **[!UICONTROL Clicked]** como [!UICONTROL Action Type].

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Event Name] | O Nome do evento que pode ser usado para refinar ainda mais este evento de clique. |
| [!UICONTROL Event Details Data Element] | O elemento de dados retorna detalhes do evento no formato JSON, incluindo: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (opcional)</li><li>`positions` (opcional)</li><li>`price` (opcional)</li><li>`quantity` (opcional)</li><li>`discount` (opcional)</li><li>`objectData` (opcional)</li><li>`currency` (opcional)</li></ul> |


>[!NOTE]
>
>Se `queryID` e `positions` forem incluídos, o evento será classificado como **IDs de objeto clicado após a Pesquisa**. Caso contrário, ele será classificado como um evento de **IDs de objeto clicado**.
><br>
>Se o Elemento de Dados não fornecer um `indexName`, o **Nome de Índice Padrão** será usado quando o evento for enviado.

![](../../../images/extensions/client/algolia/clicked.png)

Para obter mais informações sobre categorias de evento, consulte as [IDs de objeto clicadas após a pesquisa](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)
e guias de [IDs de objeto clicado](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/).

### Convertido {#converted}

Adicione a ação **[!UICONTROL Converted]** à sua regra de marcas para enviar eventos convertidos para [!DNL Algolia]. Crie uma nova regra de tag ou abra uma existente. Defina as condições de acordo com suas necessidades, selecione **[!UICONTROL Algolia]** como [!UICONTROL Extension] e selecione **[!UICONTROL Converted]** como [!UICONTROL Action Type].

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Event Name] | O Nome do Evento que será usado para refinar ainda mais este evento **convert**. |
| [!UICONTROL Event Details Data Element] | O elemento de dados retorna detalhes do evento, incluindo: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (opcional)</li><li>`recordID` (opcional)</li></ul> |

>[!NOTE]
>
>Se o Elemento de Dados contiver `queryId`, o evento será classificado como **Convertido após a Pesquisa**. Caso contrário, será classificado como um evento **Converted**.
><br>
>Se o Elemento de Dados não fornecer um `indexName`, o **Nome de Índice Padrão** será usado quando o evento for enviado.

![](../../../images/extensions/client/algolia/converted.png)

Para obter mais informações sobre as categorias de evento, consulte os guias [IDs de objeto convertido após a pesquisa](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/) e [IDs de objeto convertido](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/).

### Adicionado ao carrinho {#added-to-cart}

Adicione a ação **[!UICONTROL Added to Cart]** à sua regra de tag para enviar eventos de carrinho adicionados a [!DNL Algolia]. Crie uma nova regra de tag ou abra uma existente. Defina as condições de acordo com suas necessidades, selecione **[!UICONTROL Algolia]** como [!UICONTROL Extension] e selecione **[!UICONTROL Added to cart]** como [!UICONTROL Action Type].

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Event Name] | O Nome do Evento que será usado para refinar ainda mais este evento **adicionar ao carrinho**. |
| [!UICONTROL Event Details Data Element] | O elemento de dados retorna detalhes do evento no formato JSON, incluindo: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` (opcional)</li><li>`queryID` (opcional)</li><li>`currency` (opcional)</li></ul>. |

>[!NOTE]
>
>Se o Elemento de Dados contiver `queryId`, o evento será classificado como **Adicionado às IDs de objeto do carrinho após a Pesquisa**. Caso contrário, será classificado como um evento **Adicionado às IDs de objeto do carrinho**.
><br>
>Se o Elemento de Dados não fornecer um `indexName`, o **Nome de Índice Padrão** será usado quando o evento for enviado.
><br>
>Se os Elementos de dados padrão não atenderem aos seus requisitos, um Elemento de dados personalizado poderá ser criado para retornar os detalhes do evento desejado.

![](../../../images/extensions/client/algolia/added-to-cart.png)

Para obter mais informações sobre as categorias de eventos, consulte os guias [Adicionado às IDs de objeto do carrinho após a pesquisa](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/) e [Adicionado às IDs de objeto do carrinho](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/).

### Comprado {#purchased}

Adicione a ação **[!UICONTROL Purchased]** à sua regra de marca para enviar eventos comprados para [!DNL Algolia]. Crie uma nova regra de tag ou abra uma existente. Defina as condições de acordo com suas necessidades, selecione **[!UICONTROL Algolia]** como [!UICONTROL Extension] e selecione **[!UICONTROL Purchased]** como [!UICONTROL Action Type].

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Event Name] | O Nome do Evento que será usado para refinar ainda mais este evento **compra**. |
| [!UICONTROL Event Details Data Element] | O elemento de dados retorna detalhes do evento no formato JSON, incluindo: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` (opcional)</li><li>`queryID` (opcional)</li><li>`currency` (opcional)</li></ul>. |

>[!NOTE]
>
>A ação Comprado recupera dados do evento do armazenamento do navegador com base nas IDs do item comprado. Se qualquer um dos itens comprados contiver um `queryID` em seus dados armazenados, o evento será classificado como **IDs de objeto comprado após a Pesquisa**. Caso contrário, será classificado como um evento **IDs de objeto compradas**.
><br>
>Essa abordagem permite que o evento de compra inclua automaticamente todo o contexto relevante (ID de consulta, nome do índice, preço, quantidade, desconto) das interações anteriores do usuário com os itens.

![](../../../images/extensions/client/algolia/purchased.png)

Para obter mais informações sobre categorias de evento, consulte as [IDs de objeto compradas após a pesquisa](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)
e guias de [IDs de objeto comprado](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/).

### Exibido {#viewed}

Adicione a ação **[!UICONTROL Viewed]** à sua regra de marca para enviar eventos comprados para [!DNL Algolia]. Crie uma nova regra de tag ou abra uma existente. Defina as condições de acordo com suas necessidades, selecione **[!UICONTROL Algolia]** como [!UICONTROL Extension] e selecione **[!UICONTROL Viewed]** como [!UICONTROL Action Type].

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Event Name] | O Nome do Evento que será usado para refinar este evento **exibir**. |
| [!UICONTROL Event Details Data Element] | O elemento de dados retorna detalhes do evento no formato JSON, incluindo: <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>Se o Elemento de Dados não fornecer um `indexName`, o **Nome de Índice Padrão** será usado ao enviar o evento.

![](../../../images/extensions/client/algolia/viewed.png)

Para obter mais informações sobre o evento de exibição, consulte o guia [IDs de objeto visualizadas](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/).

## Elementos de dados da extensão do Insights do [!DNL Algolia] {#data-elements}

O [!DNL Algolia] oferece suporte a um conjunto de elementos de dados predefinidos, cada um com contextos e propriedades específicas. As seções a seguir descrevem os elementos de dados disponíveis na extensão do Insights do [!DNL Algolia].

### DataSet {#dataset}

O Elemento de Dados DataSet recupera dados associados a elementos HTML, que são usados em [!DNL Algolia] ações. Esse elemento de dados armazena automaticamente os dados do evento recuperados no armazenamento do navegador para uso posterior (como em eventos de conversão ou compra).

**Configuração Geral:**

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Hit Element Div/Class Name] | O Nome do Elemento HTML e/ou Nome da Classe CSS contendo os atributos do conjunto de dados incluindo `data-insights-object-id` e, opcionalmente, `data-insights-query-id` e `data-insights-position` no Elemento HTML. |
| [!UICONTROL Index Name Element Div/Class Name] | O Nome do Elemento HTML e/ou o Nome da Classe CSS que tem os atributos do conjunto de dados (`data-indexname`) no Elemento HTML. |

**Configuração do Commerce (Opcional):**

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Price Data Element] | Elemento de dados que retorna o preço do item. Se fornecido, ele será incluído nos dados armazenados do evento para eventos de comércio. |
| [!UICONTROL Quantity Data Element] | Elemento de dados que retorna a quantidade do item. O padrão é 1 se não for fornecido. |
| [!UICONTROL Discount Data Element] | Elemento de dados que retorna o valor decimal de desconto do item. |
| [!UICONTROL Currency Code] | O código de moeda no formato ISO-4217. Se nenhum código de moeda for especificado, a moeda padrão da configuração da extensão será usada. |

**Substituições (Opcional):**

Esses campos permitem que você substitua o comportamento padrão de recuperação de dados dos atributos do conjunto de dados do HTML.

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Record ID Data Element] | Substitua a abordagem padrão para usar o URL da página como a ID do registro. A ID do registro é usada para armazenar e pesquisar dados para enviar a [!DNL Algolia] para este produto/página. |
| [!UICONTROL Query ID Data Element] | A ID da consulta é recuperada do conjunto de dados no elemento HTML. Para substituir esse comportamento, use essa propriedade para fornecer um elemento de dados que retorne a ID da consulta como uma string. |
| [!UICONTROL Object IDs Data Element] | As IDs de objeto são recuperadas do conjunto de dados no elemento do HTML. Para substituir esse comportamento, use essa propriedade para fornecer um elemento de dados que retorne as IDs de objeto como uma matriz. |
| [!UICONTROL Positions Data Element] | As Posições são recuperadas do conjunto de dados no elemento HTML. Para substituir esse comportamento, use essa propriedade para fornecer um elemento de dados que retornará as Posições como uma matriz. |
| [!UICONTROL Index Name Data Element] | O Nome do índice é recuperado do conjunto de dados no elemento HTML. Para substituir esse comportamento, use essa propriedade para fornecer um elemento de dados que retornará o Nome do índice como uma string. |

![](../../../images/extensions/client/algolia/dataset.png)

Esse elemento de dados retorna:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,
  objectData,  // Optional: commerce data if price is provided
  currency,    // Optional: if provided
  recordID
}
```

Um exemplo de HTML que contém um conjunto de dados:

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### Sequência de consulta {#query-string}

O Elemento de Dados da Cadeia de Caracteres de Consulta extrai dados da cadeia de caracteres de consulta da URL a serem usados em [!DNL Algolia] ações.

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Object ID Param Name] | O nome do parâmetro de consulta que contém a ID do Objeto. |
| [!UICONTROL Index Name Param Name] | O nome do parâmetro de consulta que contém o Nome do Índice. |
| [!UICONTROL Query ID Param Name] | O nome do parâmetro de consulta que contém a ID da consulta. |
| [!UICONTROL Position Param Name] | O nome do parâmetro de consulta que contém a Posição. |

![](../../../images/extensions/client/algolia/query-string.png)

Esse elemento de dados retorna:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions
}
```

Um exemplo de HTML que contém parâmetros de consulta:

```html
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### Armazenamento {#storage}

O Elemento de Dados de Armazenamento recupera dados do armazenamento da sessão do navegador para uso em [!DNL Algolia] ações. Esse elemento de dados também pode ser usado para aumentar os dados armazenados com informações comerciais adicionais.

Esse elemento de dados recupera detalhes do evento que foram armazenados anteriormente no armazenamento de sessão (normalmente pelo elemento de dados do conjunto de dados durante eventos de clique). Os dados são removidos automaticamente durante os eventos de conversão, a menos que a remoção seja explicitamente desativada.

**Substituições (Opcional):**

| Propriedade | Descrição |
| --- | --- |
| [!UICONTROL Record ID Data Element] | A ID do registro é usada como uma chave para pesquisar os dados do evento armazenados no armazenamento do navegador. O URL da página é a ID de registro padrão. Para substituir esse comportamento, use essa propriedade para fornecer um elemento de dados que retorne a ID de registro como uma string. |
| [!UICONTROL Price Data Element] | Elemento de dados que retorna o preço do item. Se fornecido, atualizará os dados do evento armazenados com as informações de preço. |
| [!UICONTROL Quantity Data Element] | Elemento de dados que retorna a quantidade do item. Se fornecido, atualizará os dados do evento armazenados com as informações de quantidade. |
| [!UICONTROL Discount Data Element] | Elemento de dados que retorna o valor decimal de desconto do item. Se fornecido, atualizará os dados do evento armazenados com informações de desconto. |
| [!UICONTROL Currency Code] | Insira o código de moeda no formato ISO-4217. Se fornecido, atualizará os dados do evento armazenados com as informações de moeda. |

![](../../../images/extensions/client/algolia/storage.png)

Esse elemento de dados retorna o que é armazenado no Armazenamento de sessão, incluindo quaisquer dados de comércio aumentados:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,      // If available from original event
  objectData,     // Optional: commerce data if price is provided
  currency,       // Optional: if provided
  recordID
}
```

## Clicado ou convertido após a pesquisa {#clicked-converted-after-search}

Os eventos *Clicados após a Pesquisa* ou *Convertidos após a Pesquisa* exigem um `queryID`, e `positions` também é necessário para *Clicados após a Pesquisa*. Estas propriedades estão disponíveis quando o sinalizador `insights` está habilitado nos parâmetros de consulta de Pesquisa Instantânea e/ou Preenchimento Automático. Consulte os seguintes recursos para saber como configurar o Insights para o seu site:

* [Configurando Insights no Preenchimento Automático](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [Configurando Insights no InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [Introdução aos eventos de clique e conversão](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [Envio [!DNL Algolia] Eventos de Insights](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Iniciar Repositório GitHub de Extensão](https://github.com/algolia/algolia-launch-extension)
* [Documentação do InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] Documentação da API do Insights](https://www.algolia.com/doc/rest-api/insights/)
* [Repositório de Código da Extensão do Algolia Launch](https://github.com/algolia/algolia-launch-extension)

## Próximas etapas {#next-steps}

Este guia abordou como enviar dados para [!DNL Algolia] usando a extensão de tag [!DNL Algolia Insights]. Se você pretende enviar eventos do lado do servidor para o [!DNL Algolia], agora é possível prosseguir para instalar e configurar a [[!DNL Conversions API] extensão de encaminhamento de eventos](../../server/algolia/overview.md).

Para obter mais informações sobre tags na Experience Platform, consulte a [visão geral das tags](../../../home.md).
