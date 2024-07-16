---
title: Shopify Streaming Source
description: Saiba como criar uma conexão de origem e um fluxo de dados para assimilar dados de transmissão da sua instância do Shopify para o Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>A origem [!DNL Shopify Streaming] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform oferece suporte para assimilação de dados de aplicativos de transmissão contínua. O suporte para provedores de streaming inclui [!DNL Shopify].

## Pré-requisitos {#prerequisites}

A seção a seguir descreve as etapas de pré-requisito a serem concluídas antes de usar a origem [!DNL Shopify Streaming].

Você deve ter uma conta de parceiro [!DNL Shopify] válida para se conectar às APIs [!DNL Shopify]. Se você ainda não tiver uma conta de parceiro, registre-se usando o [[!DNL Shopify] painel de parceiros](https://www.shopify.com/partners).

### Criar seu aplicativo

Com uma conta de parceiro [!DNL Shopify] válida, agora você pode continuar e criar seu aplicativo usando o painel de parceiros. Para obter etapas abrangentes sobre como criar seu aplicativo no [!DNL Shopify], leia o [[!DNL Shopify] guia de introdução](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Depois que o aplicativo for criado, recupere a **ID do cliente** e o **segredo do cliente** da guia **credenciais do cliente** do painel de parceiros [!DNL Shopify]. A ID do cliente e o segredo do cliente serão usados nas próximas etapas para recuperar o código de autorização e o token de acesso.

### Recupere seu código de autorização

Em seguida, recupere o código de autorização inserindo a URL `myshopify.com` do domínio no navegador, juntamente com as cadeias de caracteres de consulta que definem a chave de API, os escopos e o URI de redirecionamento.

O formato desse URL é o seguinte:

**Formato da API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parâmetro | Descrição |
| --- | --- |
| `shop` | A URL do subdomínio `myshopify.com`. |
| `api_key` | Sua ID de cliente do [!DNL Shopify]. Você pode recuperar sua ID de cliente da guia **credenciais do cliente** do painel de parceiros [!DNL Shopify]. |
| `scopes` | O tipo de acesso que você deseja definir. Por exemplo, você pode definir escopos como `scope=write_orders,read_customers` para permitir permissões para modificar pedidos e ler clientes. |
| `redirect_uri` | O URL do script que gerará o token de acesso. |

**Solicitação**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Resposta**

Uma resposta bem-sucedida retorna o URL de redirecionamento, incluindo o código de autorização necessário para gerar o token de acesso.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Recupere o token de acesso

Agora que você tem a ID do cliente, o segredo do cliente e o código de autorização, é possível recuperar o token de acesso. Para recuperar o token de acesso, faça uma solicitação POST à URL `myshopify.com` do domínio ao anexar essa URL ao ponto de extremidade de API [!DNL Shopify's]: `/admin/oauth/access_token`.

**Formato da API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Solicitação**

A solicitação a seguir gera um token de acesso para a instância [!DNL Shopify].

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o token de acesso e os escopos de permissão.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Criar um webhook para transmissão de dados [!DNL Shopify] {#webhook}

Os webhooks permitem que os aplicativos permaneçam sincronizados com os dados do [!DNL Shopify] ou executem uma ação depois que um evento específico ocorrer em uma loja. Para transmitir dados do [!DNL Shopify] para o Experience Platform, é possível usar webhooks para definir o ponto de extremidade http e os tópicos para assinatura.

**Solicitação**

A solicitação a seguir cria um webhook para seus dados do [!DNL Shopify Streaming].

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Parâmetro | Descrição |
| --- | --- | 
| `webhook.address` | O endpoint http para onde as mensagens de transmissão são enviadas. |
| `webhook.topic` | O tópico da sua assinatura de webhook. Para obter mais informações, leia o [[!DNL Shopify] guia de tópicos do evento do webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | O formato dos dados. |

**Resposta**

Uma resposta bem-sucedida retorna informações no webhook, incluindo `id`, endereço e outras informações de metadados correspondentes.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Limitações {#limitations}

Esta é uma lista de limitações conhecidas que você pode encontrar ao usar webhooks com a origem [!DNL Shopify Streaming].

* Não há garantia de que você pode organizar a ordem de entrega de diferentes tópicos para o mesmo recurso. Por exemplo, é possível que um webhook `products/update` seja entregue antes de um webhook `products/create`.
* Você pode definir seu webhook para entregar eventos de webhook a um endpoint pelo menos uma vez. Isso significa que um endpoint pode receber o mesmo evento mais de uma vez. Você pode procurar eventos de webhook duplicados comparando o cabeçalho `X-Shopify-Webhook-Id` com os eventos anteriores.
* [!DNL Shopify] trata as respostas de status HTTP 2xx como notificações bem-sucedidas. Quaisquer outras respostas de código de status são consideradas como falhas. [!DNL Shopify] fornece um mecanismo de repetição para notificações de webhook com falha. Se não houver **nenhuma resposta após aguardar cinco segundos**, o [!DNL Shopify] tentará novamente a conexão **19 vezes** durante as próximas **48 horas**. Se ainda não houver respostas no final do período de novas tentativas, [!DNL Shopify] excluirá o webhook.

## Próximas etapas

Os tutoriais a seguir fornecem etapas sobre como conectar a origem do [!DNL Shopify Streaming] ao Experience Platform usando a API e a interface do usuário:

* [Crie uma conexão de origem de transmissão do Shopify e um fluxo de dados usando a API do Serviço de Fluxo](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Criar uma conexão de origem e um fluxo de dados de transmissão do Shopify na interface](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
