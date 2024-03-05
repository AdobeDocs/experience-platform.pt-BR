---
title: Preparo de dados para a coleção de dados
description: Saiba como mapear seus dados para um esquema de evento do Experience Data Model (XDM) ao configurar uma sequência de dados para os SDKs da web e móvel da Adobe Experience Platform.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 60%

---

# Preparo de dados para a coleção de dados

O Preparo de dados é um serviço da Adobe Experience Platform que permite mapear, transformar e validar dados de e para o [Experience Data Model (XDM)](../xdm/home.md). Ao configurar uma [sequência de dados](./overview.md) habilitada pela Platform, você pode usar os recursos do Preparo de dados para mapear os dados de origem no XDM durante o envio desses dados para a rede de borda da Platform.

Todos os dados enviados de uma página da Web devem chegar ao Experience Platform como XDM. Há três maneiras de traduzir dados de uma camada de dados na página para o XDM aceito pelo Experience Platform:

1. Reformate a camada de dados no XDM na própria página da Web.
2. Use a funcionalidade de elementos de dados nativos das tags para reformatar o formato de camada de dados existente de uma página da Web no XDM.
3. Reformate o formato da camada de dados existente de uma página da Web no XDM por meio da Rede de borda, usando o Preparo de dados para a coleção de dados.

Este guia foca na 3ª opção.

## Quando usar o Preparo de dados para a coleção de dados {#when-to-use-data-prep}

Há dois casos de uso em que o Preparo de dados para a coleção de dados é útil:

1. O site tem uma camada de dados bem formada, controlada e mantida, e há uma preferência por enviá-la diretamente para a Rede de borda em vez de usar a manipulação do JavaScript para convertê-la em XDM na página (por meio de elementos de dados de tags ou por manipulação manual do JavaScript).
2. Um sistema de marcação diferente de Tags é implantado no site.

## Enviar uma camada de dados existente para a Rede de borda via SDK da Web {#send-datalayer-via-websdk}

A camada de dados existente deve ser enviada usando o [`data`](/help/web-sdk/commands/sendevent/data.md) objeto dentro do `sendEvent` comando.

Se você estiver usando Tags, deverá usar o plug-in **[!UICONTROL Dados]** do campo **[!UICONTROL Enviar evento]** tipo de ação, conforme descrito na seção [Documentação da extensão de tag do SDK da Web](/help/tags/extensions/client/web-sdk/action-types.md).

O restante deste guia enfocará como mapear a camada de dados para padrões XDM após ter sido enviada pelo WebSDK.

>[!NOTE]
>
>Para obter uma orientação abrangente sobre todos os recursos do Preparo de dados, incluindo funções de transformação para campos calculados, consulte a seguinte documentação:
>
>* [Visão geral do Preparo de dados](../data-prep/home.md)
>* [Funções de mapeamento do Preparo de dados](../data-prep/functions.md)
>* [Manuseio de formatos de dados com o Preparo de dados](../data-prep/data-handling.md)

Este guia aborda como mapear seus dados na interface. Para acompanhar as etapas, inicie o processo de criação de uma sequência de dados até (e incluindo) a [etapa de configuração básica](./overview.md#create).

Para obter uma demonstração rápida do processo de preparo de dados para a coleção de dados, assista ao vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Selecionar dados] {#select-data}

Selecione **[!UICONTROL Salvar e adicionar mapeamento]** após concluir a configuração básica de uma sequência de dados e a etapa **[!UICONTROL Selecionar dados]** será exibida. Aqui, você deve fornecer um objeto JSON de amostra que represente a estrutura dos dados que planeja enviar para a Platform.

Para capturar propriedades diretamente da camada de dados, o objeto JSON deve ter uma única propriedade raiz `data`. As subpropriedades de `data` O objeto do deve ser construído de uma forma que mapeie para as propriedades da camada de dados que você deseja capturar. Selecione a seção abaixo para ver um exemplo de objeto JSON formatado corretamente com um objeto `data` raiz.

+++Arquivo JSON de amostra com objeto `data` raiz

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Para capturar propriedades de um elemento de dados de objeto XDM, as mesmas regras se aplicam ao objeto JSON, mas a propriedade raiz deve ser identificada como `xdm`. Selecione a seção abaixo para ver um exemplo de objeto JSON formatado corretamente com um objeto `xdm` raiz.

+++Arquivo JSON de amostra com objeto `xdm` raiz

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

Você pode selecionar a opção para fazer upload do objeto como um arquivo ou colar o objeto bruto na caixa de texto fornecida. Se o JSON for válido, um esquema de visualização será exibido no painel direito. Clique em **[!UICONTROL Avançar]** para continuar.

![Exemplo JSON de dados de entrada esperados.](assets/data-prep/select-data.png)

>[!NOTE]
>
> Use um objeto JSON de amostra que represente cada elemento de camada de dados que pode ser usado em qualquer página. Por exemplo, nem todas as páginas usam elementos de camada de dados do carrinho de compras. No entanto, os elementos da camada de dados do carrinho de compras devem ser incluídos nesta amostra de objeto JSON.

## [!UICONTROL Mapeamento]

A etapa **[!UICONTROL Mapeamento]** é exibida, permitindo mapear os campos nos dados de origem para o esquema de evento de público alvo na Platform. Aqui, é possível configurar o mapeamento de duas maneiras:

* [Criar regras de mapeamento](#create-mapping) para esse fluxo de dados por meio de um processo manual.
* [Importar regras de mapeamento](#import-mapping) de uma sequência de dados existente.

### Criar regras de mapeamento {#create-mapping}

Para criar uma regra de mapeamento, selecione **[!UICONTROL Adicionar novo mapeamento]**.

![Adicionar um novo mapeamento.](assets/data-prep/add-new-mapping.png)

Selecione o ícone de origem (![Ícone de origem](assets/data-prep/source-icon.png)) e, na caixa de diálogo exibida, selecione o campo de origem que deseja mapear na tela fornecida. Depois de escolher um campo, use o botão **[!UICONTROL Selecionar]** para continuar.

![Seleção do campo a ser mapeado no esquema de origem.](assets/data-prep/source-mapping.png)

Em seguida, selecione o ícone de esquema (![Ícone de esquema](assets/data-prep/schema-icon.png)) para abrir uma caixa de diálogo semelhante para o esquema de evento de destino. Escolha o campo para o qual deseja mapear os dados antes de confirmar com **[!UICONTROL Selecionar]**.

![Seleção do campo a ser mapeado no schema de destino.](assets/data-prep/target-mapping.png)

A página de mapeamento é exibida novamente com o mapeamento do campo concluído. A seção **[!UICONTROL Progresso do mapeamento]** é atualizada para refletir o número total de campos que foram mapeados com sucesso.

![Campo mapeado com êxito com o progresso refletido.](assets/data-prep/field-mapped.png)

>[!TIP]
>
>Se quiser mapear uma matriz de objetos (no campo de origem) para uma matriz de objetos diferentes (no campo de destino), adicione `[*]` após o nome da matriz nos caminhos dos campos de origem e destino, conforme mostrado abaixo.
>
>![Mapeamento de objeto de matriz.](assets/data-prep/array-object-mapping.png)

### Importar regras de mapeamento existentes {#import-mapping}

Se você tiver criado um fluxo de dados anteriormente, poderá reutilizar suas regras de mapeamento configuradas para um novo fluxo de dados.

>[!WARNING]
>
>A importação de regras de mapeamento de outro fluxo de dados substitui todos os mapeamentos de campo que você tenha adicionado antes da importação.

Para começar, selecione **[!UICONTROL Importar mapeamento]**.

![O botão Importar mapeamento está sendo selecionado.](assets/data-prep/import-mapping-button.png)

Na caixa de diálogo exibida, selecione a sequência de dados cujas regras de mapeamento você deseja importar. Depois que a sequência de dados for escolhida, selecione **[!UICONTROL Visualizar]**.

![Selecionar um fluxo de dados existente.](assets/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>As sequências de dados só podem ser importadas dentro da mesma [sandbox](../sandboxes/home.md). Em outras palavras, não é possível importar uma sequência de dados de uma sandbox para outra.

A próxima tela mostra uma visualização das regras de mapeamento salvas para a sequência de dados selecionada. Verifique se os mapeamentos exibidos são os esperados e selecione **[!UICONTROL Importar]** para confirmar e adicionar os mapeamentos à nova sequência de dados.

![Regras de mapeamento a serem importadas.](assets/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Se algum campo de origem das regras de mapeamento importadas não estiver incluído nos dados JSON de amostra que você [forneceu anteriormente](#select-data), esses mapeamentos de campo não serão incluídos na importação.

### Concluir o mapeamento

Para continuar, siga as etapas acima para mapear o restante dos campos para o esquema de destino. Embora não seja necessário mapear todos os campos de origem disponíveis, todos os campos no esquema de destino definidos como obrigatório devem ser mapeados para concluir esta etapa. O contador **[!UICONTROL Campos obrigatórios]** indica quantos campos obrigatórios ainda não estão mapeados na configuração atual.

Quando a contagem de campos obrigatória atingir zero e você estiver satisfeito com o mapeamento, selecione **[!UICONTROL Salvar]** para finalizar as alterações.

![Mapeamento concluído](assets/data-prep/mapping-complete.png)

## Próximas etapas

Este guia abordou como mapear seus dados para o XDM ao configurar uma sequência de dados na interface. Se você estava seguindo o tutorial geral para sequências de dados, agora pode retornar à etapa sobre [visualizar detalhes da sequência de dados](./overview.md).
