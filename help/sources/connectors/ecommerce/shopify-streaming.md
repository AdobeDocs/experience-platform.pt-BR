---
title: Fonte de fluxo de compras
description: Saiba como criar uma conexão de origem e um fluxo de dados para assimilar dados de transmissão da sua instância do Shopify para o Adobe Experience Platform
badge: "Beta"
hidefromtoc: y
hide: y
source-git-commit: 97e6cda8fa7a40542de5a34a9f4dfcaeb715edbf
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>O [!DNL Shopify Streaming] A fonte está em beta. Leia o [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

A Adobe Experience Platform oferece suporte para assimilar dados de aplicativos de transmissão. O suporte para provedores de transmissão inclui [!DNL Shopify].

## Pré-requisitos {#prerequisites}

A seção a seguir descreve as etapas de pré-requisito a serem concluídas antes de usar o [!DNL Shopify Streaming] fonte.

Você deve ter um [!DNL Shopify] conta do parceiro para se conectar ao [!DNL Shopify] APIs. Se você ainda não tiver uma conta de parceiro, registre-se usando o [[!DNL Shopify] painel parceiros](https://www.shopify.com/partners).

### Crie seu aplicativo

Com um [!DNL Shopify] conta do parceiro, agora você pode continuar e criar seu aplicativo usando o painel de parceiros. Para obter etapas abrangentes sobre como criar seu aplicativo em [!DNL Shopify]leia a [[!DNL Shopify] guia de introdução](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Depois que o aplicativo for criado, recupere o **client ID** e **segredo do cliente** do **credenciais do cliente** da guia [!DNL Shopify] painel parceiros. A ID do cliente e o segredo do cliente serão usados nas próximas etapas para recuperar o código de autorização e o token de acesso.

### Recuperar o código de autorização

Em seguida, recupere seu código de autorização inserindo o do domínio `myshopify.com` URL no navegador, juntamente com cadeias de caracteres de consulta que definem a chave da API, os escopos e o URI de redirecionamento.

O formato desse URL é o seguinte:

**Formato da API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parâmetro | Descrição |
| --- | --- |
| `shop` | Seu subdomínio `myshopify.com` URL. |
| `api_key` | Seu [!DNL Shopify] ID do cliente. Você pode recuperar a ID do cliente do **credenciais do cliente** da guia [!DNL Shopify] painel parceiros. |
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

### Recuperar o token de acesso

Agora que você tem a ID do cliente, o segredo do cliente e o código de autorização, é possível recuperar o token de acesso. Para recuperar o token de acesso, faça uma solicitação POST ao `myshopify.com` URL ao anexar este URL com [!DNL Shopify's] Ponto de extremidade da API: `/admin/oauth/access_token`.

**Formato da API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Solicitação**

A solicitação a seguir gera um token de acesso para o seu [!DNL Shopify] instância.

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

## Criar um webhook para transmissão [!DNL Shopify] dados {#webhook}

Os Webhooks permitem que os aplicativos permaneçam sincronizados com seu [!DNL Shopify] ou executar uma ação depois que um evento específico ocorrer em uma loja. Para transmissão [!DNL Shopify] dados para o Experience Platform, os webhooks podem ser usados para definir o endpoint http e os tópicos da assinatura.

**Solicitação**

A solicitação a seguir cria um webhook para seu [!DNL Shopify Streaming] dados.

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
| `webhook.address` | O endpoint http onde as mensagens de transmissão são enviadas. |
| `webhook.topic` | O tópico da sua assinatura do webhook. Para obter mais informações, leia a [[!DNL Shopify] guia de tópicos do evento do webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | O formato dos dados. |

**Resposta**

Uma resposta bem-sucedida retorna informações sobre o webhook, incluindo seus `id`, endereço e outras informações de metadados.

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

Veja a seguir uma lista de limitações conhecidas que você pode encontrar ao usar webhooks com o [!DNL Shopify Streaming] fonte.

* Não há garantias de que você possa organizar a ordem de entrega de tópicos diferentes para o mesmo recurso. Por exemplo, é possível que uma `products/update` o webhook é entregue antes de um `products/create` webhook.
* Você pode definir seu webhook para enviar eventos do webhook para um terminal pelo menos uma vez. Isso significa que um terminal pode receber o mesmo evento mais de uma vez. Você pode verificar eventos duplicados do webhook comparando o `X-Shopify-Webhook-Id` para eventos anteriores.
* [!DNL Shopify] O trata as respostas do status HTTP 2xx como notificações bem-sucedidas. Quaisquer outras respostas do código de status são consideradas falhas. [!DNL Shopify] O fornece um mecanismo de repetição para notificações de webhook com falha. Se houver **sem resposta após aguardar cinco segundos**, [!DNL Shopify] tenta novamente a conexão **19 vezes** durante o próximo **48 horas**. Se ainda não houver respostas até o final do período de nova tentativa, então [!DNL Shopify] exclui o webhook.

## Próximas etapas

Os seguintes tutoriais fornecem etapas sobre como conectar seu [!DNL Shopify Streaming] fonte para o Experience Platform usando a API e a interface do usuário:

* [Criar uma conexão de fonte de transmissão e um fluxo de dados do Shopify usando a API do Serviço de Fluxo](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Criar uma conexão de origem e fluxo de dados do Shopify Streaming na interface do usuário](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
