---
title: Criar uma conexão com a base de Marketing Cloud do Salesforce usando a API do serviço de fluxo
description: Saiba como autenticar sua conta de Marketing Cloud do Salesforce em relação ao Experience Platform usando a API de serviço de fluxo.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 4%

---

# Criar uma conexão de base [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>A origem [!DNL Salesforce Marketing Cloud] será substituída no final de maio de 2025. Você pode usar o [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) no lugar da origem [!DNL Salesforce Marketing Cloud].

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Salesforce Marketing Cloud] usando a [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../../../landing/api-guide.md).

A seção a seguir fornece informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Salesforce Marketing Cloud], você deve fornecer as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O servidor host do aplicativo. Esse geralmente é o seu subdomínio. **Observação:** ao inserir seu valor `host`, você precisa especificar o `{subdomain}.rest.marketingcloudapis.com`. Por exemplo, se a URL do host for `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, você deve inserir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` como valor do host. |
| `clientId` | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | O segredo do cliente associado ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Salesforce Marketing Cloud] é: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Salesforce Marketing Cloud] documento](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Criar uma conexão básica

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não tem suporte da integração de origem [!DNL Salesforce Marketing Cloud].

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece suas credenciais de autenticação [!DNL Salesforce Marketing Cloud] como parte do corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.clientId` | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | O segredo do cliente associado ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Resposta**

Uma resposta bem-sucedida retorna a conexão recém-criada, incluindo seu identificador de conexão exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Salesforce Marketing Cloud] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados de automação de marketing para a Platform usando a API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
