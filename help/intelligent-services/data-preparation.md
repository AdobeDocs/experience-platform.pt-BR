---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Preparar dados para uso no Intelligent Services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1b367eb65d1e592412d601d089725671e42b7bbd

---


# Preparar dados para uso no Intelligent Services

Para que os Serviços inteligentes detectem insights de seus dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. Os Serviços inteligentes aproveitam os schemas do Experience Data Model (XDM) para conseguir isso. Especificamente, todos os conjuntos de dados usados no Intelligent Services devem estar em conformidade com o schema XDM **Consumer ExperienceEvent (CEE)** .

Este documento fornece orientação geral sobre como mapear os dados de seus eventos de marketing de vários canais para esse schema, descrevendo informações sobre campos importantes dentro do schema para ajudá-lo a determinar como mapear efetivamente seus dados para sua estrutura.

## Como entender o schema CEE

O schema ExperienceEvent do consumidor descreve o comportamento de um indivíduo, pois ele se relaciona aos eventos de marketing digital (Web ou móveis), bem como à atividade de comércio online ou offline. O uso desse schema é necessário para os Serviços inteligentes devido aos campos semânticos bem definidos (colunas), evitando nomes desconhecidos que deixariam os dados menos claros.

Os Serviços inteligentes utilizam vários campos chave dentro desse schema para gerar insights dos dados de seus eventos de marketing, que podem ser encontrados no nível raiz e expandidos para mostrar os subcampos necessários.

![](./images/data-preparation/schema-expansion.gif)

Como todos os schemas XDM, a mistura CEE é extensível. Em outras palavras, campos adicionais podem ser adicionados à mistura CEE e variações diferentes podem ser incluídas em vários schemas, se necessário.

Um exemplo completo da mistura pode ser encontrado no repositório [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)público e deve ser usado como referência para os campos principais descritos na seção abaixo.

## Campos principais

As seções abaixo destacam os principais campos da mistura CEE que devem ser utilizados para que os Serviços inteligentes gerem insights úteis, incluindo descrições e links para documentação de referência para mais exemplos.

### xdm:canal

Este campo representa o canal de marketing relacionado ao ExperienceEvent. O campo inclui informações sobre o tipo de canal, o tipo de mídia e o tipo de local. **Este campo _deve_ser fornecido para que a Atribuição AI funcione com seus dados**.

![](./images/data-preparation/channel.png)

**Exemplo de schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Para obter informações completas sobre cada um dos subcampos obrigatórios para `xdm:channel`, consulte as especificações da [experiência do schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) do canal. Para obter alguns exemplos de mapeamentos, consulte a [tabela abaixo](#example-channels).

#### Exemplos de mapeamentos de canal {#example-channels}

A tabela a seguir fornece alguns exemplos de canais de marketing mapeados para o `xdm:channel` schema:

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Pesquisa paga | https:/<span>/ns.adobe.com/xdm/canal-types/search | pago | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/canais-types/social | won | clicks |
| Exibir | https:/<span>/ns.adobe.com/xdm/canal-types/display | pago | clicks |
| Email | https:/<span>/ns.adobe.com/xdm/canal-types/email | pago | clicks |
| Quem indicou interna | https:/<span>/ns.adobe.com/xdm/canal-types/direct | proprietário | clicks |
| Exibir ViewThrough | https:/<span>/ns.adobe.com/xdm/canal-types/display | pago | impressões |
| Redirecionamento de código QR | https:/<span>/ns.adobe.com/xdm/canal-types/direct | proprietário | clicks |
| Dispositivo móvel | https:/<span>/ns.adobe.com/xdm/canal-types/mobile | proprietário | clicks |

### xdm:productListItems

Este campo é uma matriz de itens que representam os produtos selecionados por um cliente, incluindo o SKU do produto, o nome, o preço e a quantidade.

![](./images/data-preparation/productListItems.png)

**Exemplo de schema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Para obter informações completas sobre cada um dos subcampos obrigatórios para `xdm:productListItems`, consulte as especificações do schema [de detalhes do](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) comércio.

### xdm:comércio

Este campo contém informações específicas de comércio sobre o ExperienceEvent, incluindo o número do pedido de compra e as informações de pagamento.

![](./images/data-preparation/commerce.png)

**Exemplo de schema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Para obter informações completas sobre cada um dos subcampos obrigatórios para `xdm:commerce`, consulte as especificações do schema [de detalhes do](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) comércio.

### xdm:web

Este campo representa detalhes da Web relacionados ao ExperienceEvent, como interação, detalhes da página e quem indicou.

![](./images/data-preparation/web.png)

**Exemplo de schema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Para obter informações completas sobre cada um dos subcampos obrigatórios para `xdm:productListItems`, consulte as especificações do schema [de detalhes da Web](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) ExperienceEvent.

### xdm:marketing

Este campo contém informações relacionadas a atividades de marketing que estão ativas com o ponto de contato.

![](./images/data-preparation/marketing.png)

**Exemplo de schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Para obter informações completas sobre cada um dos subcampos obrigatórios para `xdm:productListItems`, consulte as especificações do setor de [marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) .

## Dados de mapeamento e assimilação

Depois de determinar se os dados de seus eventos de marketing podem ser mapeados para o schema CEE, você pode start o processo de inserir seus dados nos Serviços inteligentes. Entre em contato com os Serviços de consultoria da Adobe para ajudar a mapear seus dados para o schema e assimilá-los ao serviço.

Se você tiver uma subscrição da plataforma Adobe Experience e quiser mapear e assimilar os dados, siga as etapas descritas na seção abaixo.

### Uso da plataforma Adobe Experience

>[!NOTE] As etapas abaixo exigem uma subscrição para a plataforma Experience. Se você não tiver acesso à Plataforma, pule para a seção de [próximas etapas](#next-steps) .

Esta seção descreve o fluxo de trabalho para mapear e assimilar dados na Experience Platform para uso em Serviços inteligentes, incluindo links para tutoriais para etapas detalhadas.

#### Criar um schema CEE e um conjunto de dados

Quando estiver pronto para o start preparando seus dados para ingestão, a primeira etapa é criar um novo schema XDM que emprega a combinação CEE. Os seguintes tutoriais acompanham o processo de criação de um novo schema na interface do usuário ou na API:

* [Criar um schema na interface do usuário](../xdm/tutorials/create-schema-ui.md)
* [Criar um schema na API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Os tutoriais acima seguem um fluxo de trabalho genérico para criar um schema. Ao escolher uma classe para o schema, você deve usar a classe **** XDM ExperienceEvent. Depois que essa classe for escolhida, você poderá adicionar a mistura CEE ao schema.

Depois de adicionar o mixin CEE ao schema, você pode adicionar outras combinações, conforme necessário, para campos adicionais em seus dados.

Depois de criar e salvar o schema, você pode criar um novo conjunto de dados com base nesse schema. Os seguintes tutoriais acompanham o processo de criação de um novo conjunto de dados na interface do usuário ou na API:

* [Criar um conjunto de dados na interface do usuário](../catalog/datasets/user-guide.md#create) (Siga o fluxo de trabalho para usar um schema existente)
* [Criar um conjunto de dados na API](../catalog/datasets/create.md)

#### Mapear e assimilar dados

Depois de criar um schema CEE e um conjunto de dados, você pode fazer um start mapeando suas tabelas de dados para o schema e ingerir esses dados na Plataforma. Consulte o tutorial sobre como [mapear um arquivo CSV para um schema](../ingestion/tutorials/map-a-csv-file.md) XDM para obter etapas sobre como executar isso na interface do usuário. Depois que um conjunto de dados é preenchido, o mesmo conjunto de dados pode ser usado para assimilar arquivos de dados adicionais.

## Próximas etapas {#next-steps}

Este documento fornece orientação geral sobre como preparar seus dados para uso nos Serviços inteligentes. Se precisar de consultoria adicional com base no caso de uso, entre em contato com o Suporte de consultoria da Adobe.

Depois de preencher com êxito um conjunto de dados com os dados de experiência do cliente, você pode usar os Serviços inteligentes para gerar insights. Consulte os seguintes documentos para começar:

* [Visão geral do AI de atribuição](./attribution-ai/overview.md)
* [Visão geral da IA do cliente](./customer-ai/overview.md)
