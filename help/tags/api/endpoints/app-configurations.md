---
title: Ponto de extremidade de configurações do aplicativo
description: Saiba como fazer chamadas para o endpoint /app_settings na API do Reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 7%

---

# Ponto de extremidade de configurações do aplicativo

>[!WARNING]
>
>A implementação do endpoint `/app_configurations` está em fluxo à medida que os recursos são adicionados, removidos e retrabalhados.

As configurações do aplicativo permitem que as credenciais sejam armazenadas e recuperadas para uso posterior. O endpoint `/app_configurations` na API do Reator permite gerenciar programaticamente as configurações do aplicativo no aplicativo de experiência.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Recuperar uma lista de configurações do aplicativo {#list}

**Formato da API**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parâmetro | Descrição |
| --- | --- |
| `COMPANY_ID` | O `id` da [empresa](./companies.md) proprietária das configurações do aplicativo. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Usando parâmetros de consulta, as configurações de aplicativo listadas podem ser filtradas com base nos seguintes atributos:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Consulte o guia sobre [respostas de filtragem](../guides/filtering.md) para obter mais informações.

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de configurações do aplicativo.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Pesquisar uma configuração de aplicativo {#lookup}

Você pode pesquisar uma configuração de aplicativo fornecendo a ID no caminho de uma solicitação do GET.

**Formato da API**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `APP_CONFIGURATION_ID` | O `id` da configuração do aplicativo que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da configuração do aplicativo.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Criar uma configuração de aplicativo {#create}

Você pode criar uma nova configuração de aplicativo fazendo uma solicitação de POST.

**Formato da API**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parâmetro | Descrição |
| --- | --- |
| `COMPANY_ID` | O `id` da [empresa](./companies.md) em que você está definindo a configuração do aplicativo. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `platform` | A plataforma em que o aplicativo é executado (Web ou móvel). Isso determina quais serviços de mensagens estão disponíveis. |
| `messaging_service` | O serviço de mensagens associado ao aplicativo, como [Apple Push Notification service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) e [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Isso determina quais tipos de chave podem ser usados. |
| `key_type` | Representa o protocolo que um fornecedor de serviços de push suporta e determina o formato do objeto `push_credential`. À medida que os protocolos evoluem para serviços de mensagens, novos valores `key_type` são criados para suportar os protocolos atualizados. |
| `push_credential` | O valor real da credencial, que é criptografado em repouso. Normalmente, esse campo não é descriptografado ou incluído nas respostas da API. Somente determinados serviços do Adobe podem obter uma resposta contendo uma credencial de push descriptografada. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da configuração do aplicativo recém-criado.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Atualizar uma configuração de aplicativo

Você pode atualizar uma configuração de aplicativo incluindo sua ID no caminho de uma solicitação de PUT.

**Formato da API**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `APP_CONFIGURATION_ID` | O `id` da configuração do aplicativo que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir atualiza o `app_id` de uma configuração de aplicativo existente.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `attributes` | Um objeto cujas propriedades representam os atributos a serem atualizados para a configuração do aplicativo. Cada chave representa o atributo de configuração do aplicativo específico a ser atualizado, juntamente com o valor correspondente ao qual deve ser atualizado.<br><br>Os seguintes atributos podem ser atualizados para configurações do aplicativo:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | O `id` da configuração do aplicativo que você deseja atualizar. Isso deve corresponder ao valor `{APP_CONFIGURATION_ID}` fornecido no caminho da solicitação. |
| `type` | O tipo de recurso que está sendo atualizado. Para esse ponto de extremidade, o valor deve ser `app_configurations`. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da configuração atualizada do aplicativo.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Excluir uma configuração de aplicativo

Você pode excluir uma configuração de aplicativo ao incluir sua ID no caminho de uma solicitação de DELETE.

**Formato da API**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `APP_CONFIGURATION_ID` | O `id` da configuração do aplicativo que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) sem corpo de resposta, indicando que a configuração do aplicativo foi excluída.
