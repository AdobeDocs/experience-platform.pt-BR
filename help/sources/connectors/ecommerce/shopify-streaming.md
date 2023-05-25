---
title: Shopify Fonte de Transmissão
description: Saiba como criar uma conexão de origem e um fluxo de dados para assimilar dados de transmissão da sua instância do Shopify para o Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>A variável [!DNL Shopify Streaming] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

O Adobe Experience Platform oferece suporte para assimilação de dados de aplicativos de transmissão contínua. O suporte para provedores de transmissão inclui [!DNL Shopify].

## Pré-requisitos {#prerequisites}

A seção a seguir descreve as etapas de pré-requisito a serem concluídas antes de usar o [!DNL Shopify Streaming] origem.

Você deve ter um válido [!DNL Shopify] conta do parceiro para se conectar à [!DNL Shopify] APIs. Se você ainda não tiver uma conta de parceiro, registre-se usando o [[!DNL Shopify] painel de parceiros](https://www.shopify.com/partners).

### Criar seu aplicativo

Com um válido [!DNL Shopify] conta de parceiro, agora você pode continuar e criar seu aplicativo usando o painel de parceiros. Para obter etapas abrangentes sobre como criar seu aplicativo no [!DNL Shopify], leia o [[!DNL Shopify] guia de introdução](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Depois que o aplicativo for criado, recupere **ID do cliente** e **segredo do cliente** do **credenciais do cliente** guia do [!DNL Shopify] painel de parceiros. A ID do cliente e o segredo do cliente serão usados nas próximas etapas para recuperar o código de autorização e o token de acesso.

### Recupere seu código de autorização

Em seguida, recupere o código de autorização inserindo o nome do domínio `myshopify.com` O URL no navegador, juntamente com as sequências de consulta que definem a chave da API, os escopos e o URI de redirecionamento.

O formato desse URL é o seguinte:

**Formato da API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parâmetro | Descrição |
| --- | --- |
| `shop` | Seu subdomínio `myshopify.com` URL. |
| `api_key` | Seu [!DNL Shopify] ID do cliente. Você pode recuperar a ID do cliente do **credenciais do cliente** guia do [!DNL Shopify] painel de parceiros. |
| `scopes` | O tipo de acesso que você deseja definir. Por exemplo, é possível definir escopos como `scope=write_orders,read_customers` para permitir permissões para modificar pedidos e ler clientes. |
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

Agora que você tem a ID do cliente, o segredo do cliente e o código de autorização, é possível recuperar o token de acesso. Para recuperar o token de acesso, faça uma solicitação POST no `myshopify.com` URL ao anexar este URL com [!DNL Shopify's] Endpoint da API: `/admin/oauth/access_token`.

**Formato da API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Solicitação**

A solicitação a seguir gera um token de acesso para o [!DNL Shopify] instância.

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

Os webhooks permitem que os aplicativos permaneçam sincronizados com o [!DNL Shopify] dados ou executar uma ação depois que um evento específico ocorrer em uma loja. Para transmissão [!DNL Shopify] dados para Experience Platform, os webhooks podem ser usados para definir o endpoint http e os tópicos para assinatura.

**Solicitação**

A solicitação a seguir cria um webhook para o [!DNL Shopify Streaming] dados.

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
| `webhook.topic` | O tópico da sua assinatura de webhook. Para obter mais informações, leia a [[!DNL Shopify] guia de tópicos do evento do webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | O formato dos dados. |

**Resposta**

Uma resposta bem-sucedida retorna informações no webhook, incluindo as correspondentes `id`, endereço e outras informações de metadados.

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

Veja a seguir uma lista de limitações conhecidas que podem ser encontradas ao usar webhooks com o [!DNL Shopify Streaming] origem.

* Não há garantia de que você pode organizar a ordem de entrega de diferentes tópicos para o mesmo recurso. Por exemplo, é possível que uma variável `products/update` o webhook é entregue antes de um `products/create` webhook.
* Você pode definir seu webhook para entregar eventos de webhook a um endpoint pelo menos uma vez. Isso significa que um endpoint pode receber o mesmo evento mais de uma vez. Você pode procurar eventos de webhook duplicados comparando o `X-Shopify-Webhook-Id` cabeçalho para eventos anteriores.
* [!DNL Shopify] trata as respostas de status HTTP 2xx como notificações de sucesso. Quaisquer outras respostas de código de status são consideradas como falhas. [!DNL Shopify] fornece um mecanismo de repetição para notificações de webhook com falha. Se houver **nenhuma resposta após aguardar cinco segundos**, [!DNL Shopify] tenta novamente a conexão **19 vezes** durante o próximo **48 horas**. Se ainda não houver respostas no final do período de novas tentativas, [!DNL Shopify] exclui o webhook.

## Próximas etapas

Os seguintes tutoriais fornecem etapas sobre como conectar seus [!DNL Shopify Streaming] origem para Experience Platform usando a API e a interface do usuário:

* [Crie uma conexão de origem de transmissão do Shopify e um fluxo de dados usando a API do Serviço de Fluxo](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Criar uma conexão de origem e um fluxo de dados de transmissão do Shopify na interface](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
