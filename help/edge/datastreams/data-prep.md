---
title: Preparação de dados para coleção de dados
description: Saiba como mapear seus dados para um esquema de evento do Experience Data Model (XDM) ao configurar um conjunto de dados para a Web Adobe Experience Platform e SDKs móveis.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 5a30bd502cd3950f3c74d5c39d0c7e395fcbb839
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# Preparação de dados para coleção de dados

A Preparação de dados é um serviço da Adobe Experience Platform que permite mapear, transformar e validar dados de e para [Experience Data Model (XDM)](../../xdm/home.md). Ao configurar uma Plataforma ativada [datastream](./overview.md), você pode usar os recursos de Preparação de dados para mapear os dados de origem para XDM ao enviá-los para a Rede de borda da plataforma.

>[!NOTE]
>
>Para obter uma orientação abrangente sobre todos os recursos de Preparação de dados, incluindo funções de transformação para campos calculados, consulte a seguinte documentação:
>
>* [Visão geral da preparação de dados](../../data-prep/home.md)
>* [Funções de mapeamento da preparação de dados](../../data-prep/functions.md)
>* [Manuseio de formatos de dados com Preparação de dados](../../data-prep/data-handling.md)


Este guia aborda como mapear seus dados na interface do usuário da coleta de dados. Para seguir com as etapas, inicie o processo de criação de um conjunto de dados até (e incluindo) a variável [etapa de configuração básica](./overview.md#create).

Para obter uma demonstração rápida do processo de Preparação de dados para coleta de dados, consulte o seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Selecionar dados] {#select-data}

Selecionar **[!UICONTROL Salvar e adicionar mapeamento]** após concluir a configuração básica de um armazenamento de dados, e o **[!UICONTROL Selecionar dados]** será exibida. A partir daqui, você deve fornecer um objeto JSON de amostra que represente a estrutura dos dados que planeja enviar para a Plataforma.

Para capturar propriedades diretamente da camada de dados, o objeto JSON deve ter uma única propriedade raiz `data`. As subpropriedades da variável `data` O objeto deve ser construído de forma a mapear as propriedades da camada de dados que deseja capturar. Selecione a seção abaixo para exibir um exemplo de um objeto JSON corretamente formatado com um `data` raiz.

+++Exemplo de arquivo JSON com `data` root

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

Para capturar propriedades de um elemento de dados de objeto XDM, as mesmas regras se aplicam ao objeto JSON, mas a propriedade raiz deve ser chaveada como `xdm` em vez disso. Selecione a seção abaixo para exibir um exemplo de um objeto JSON corretamente formatado com um `xdm` raiz.

+++Exemplo de arquivo JSON com `xdm` root

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

Você pode selecionar a opção de carregar o objeto como um arquivo ou colar o objeto bruto na caixa de texto fornecida. Se o JSON for válido, um esquema de visualização será exibido no painel direito. Clique em **[!UICONTROL Avançar]** para continuar.

![Amostra JSON de dados de entrada esperados](../images/datastreams/data-prep/select-data.png)

## [!UICONTROL Mapeamento]

O **[!UICONTROL Mapeamento]** é exibida, permitindo mapear os campos nos dados de origem para o do esquema de evento de destino no Platform. Aqui, você pode configurar o mapeamento de duas maneiras:

* [Criar novas regras de mapeamento](#create-mapping) para esse armazenamento de dados por meio de um processo manual.
* [Importar regras de mapeamento](#import-mapping) de um armazenamento de dados existente.

### Criar um novo mapeamento {#create-mapping}

Para começar, selecione **[!UICONTROL Adicionar novo mapeamento]** para criar uma nova linha de mapeamento.

![Adição de um novo mapeamento](../images/datastreams/data-prep/add-new-mapping.png)

Selecione o ícone de origem (![Ícone de origem](../images/datastreams/data-prep/source-icon.png)) e, na caixa de diálogo exibida, selecione o campo de origem que deseja mapear na tela fornecida. Depois de escolher um campo, use a variável **[!UICONTROL Selecionar]** para continuar.

![Seleção do campo a ser mapeado no schema de origem](../images/datastreams/data-prep/source-mapping.png)

Em seguida, selecione o ícone de esquema (![Ícone Esquema](../images/datastreams/data-prep/schema-icon.png)) para abrir uma caixa de diálogo semelhante para o esquema de evento de destino. Escolha o campo para o qual deseja mapear os dados antes de confirmar com **[!UICONTROL Selecionar]**.

![Seleção do campo a ser mapeado no schema de target](../images/datastreams/data-prep/target-mapping.png)

A página de mapeamento é exibida novamente com o mapeamento de campo concluído mostrado. O **[!UICONTROL Andamento do mapeamento]** atualizações de seção para refletir o número total de campos que foram mapeados com êxito.

![Campo mapeado com êxito com progresso refletido](../images/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>Para mapear uma matriz de objetos (no campo de origem) para uma matriz de objetos diferentes (no campo de destino), adicione `[*]` após o nome da matriz nos caminhos de campo de origem e de destino, conforme mostrado abaixo.
>
>![Mapeamento de objetos de matriz](../images/datastreams/data-prep/array-object-mapping.png)

### Importar regras de mapeamento existentes {#import-mapping}

Se você criou um conjunto de dados anteriormente, é possível reutilizar as regras de mapeamento configuradas para um novo conjunto de dados.

>[!WARNING]
>
>A importação de regras de mapeamento de outro conjunto de dados substituirá qualquer mapeamento de campo que tenha sido adicionado antes da importação.

Para iniciar, selecione **[!UICONTROL Importar mapeamento]**.

![Imagem que mostra o [!UICONTROL Importar mapeamento] botão sendo selecionado](../images/datastreams/data-prep/import-mapping-button.png)

Na caixa de diálogo exibida, selecione o conjunto de dados cujas regras de mapeamento você deseja importar. Depois que o datastream for escolhido, selecione **[!UICONTROL Visualizar]**.

![Imagem que mostra um conjunto de dados existente sendo selecionado](../images/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Os datastreams só podem ser importados dentro do mesmo [sandbox](../../sandboxes/home.md). Em outras palavras, não é possível importar um armazenamento de dados de um sandbox para outro.

A próxima tela mostra uma pré-visualização das regras de mapeamento salvas para o armazenamento de dados selecionado. Certifique-se de que os mapeamentos exibidos sejam o que você espera e selecione **[!UICONTROL Importar]** para confirmar e adicionar os mapeamentos ao novo armazenamento de dados.

![Imagem que mostra as regras de mapeamento a serem importadas](../images/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Se algum campo de origem nas regras de mapeamento importadas não estiver incluído na amostra de dados JSON que você [fornecido anteriormente](#select-data), esses mapeamentos de campo não serão incluídos na importação.

### Concluir o mapeamento

Continue seguindo as etapas acima para mapear o restante dos campos para o schema de destino. Embora não seja necessário mapear todos os campos de origem disponíveis, todos os campos no schema de destino definidos conforme necessário devem ser mapeados para concluir esta etapa. O **[!UICONTROL Campos obrigatórios]** O contador indica quantos campos obrigatórios ainda não estão mapeados na configuração atual.

Quando a contagem dos campos necessários atingir zero e você estiver satisfeito com seu mapeamento, selecione **[!UICONTROL Salvar]** para finalizar as alterações.

![Mapeamento concluído](../images/datastreams/data-prep/mapping-complete.png)

## Próximas etapas

Este guia cobriu como mapear seus dados para XDM ao configurar um conjunto de dados na interface do usuário da coleta de dados. Caso esteja seguindo o tutorial de conjuntos de dados gerais, agora é possível retornar à etapa em [exibindo detalhes do datastream](./overview.md).
