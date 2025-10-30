---
description: Esta página exemplifica a chamada à API usada para criar um modelo de público-alvo por meio do Adobe Experience Platform Destination SDK.
title: Criar um modelo de público-alvo
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# Criar um modelo de público-alvo

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Para alguns destinos criados usando o Destination SDK, é necessário criar uma configuração de metadados de público-alvo para criar, atualizar ou excluir programaticamente metadados de público-alvo no destino. Esta página mostra como usar o endpoint da API `/authoring/audience-templates` para criar a configuração.

Para obter uma descrição detalhada dos recursos que você pode configurar por meio deste ponto de extremidade, consulte [gerenciamento de metadados de público-alvo](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações de API do modelo de público-alvo {#get-started}

Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Criar um modelo de público-alvo {#create}

Você pode criar um novo modelo de público fazendo uma solicitação `POST` para o ponto de extremidade `/authoring/audience-templates`.

**Formato da API**

```http
POST /authoring/audience-templates
```

+++Solicitação

A solicitação a seguir cria um novo modelo de público-alvo, configurado pelos parâmetros fornecidos na carga. A carga abaixo inclui todos os parâmetros aceitos pelo ponto de extremidade `/authoring/audience-templates`. Observe que não é necessário adicionar todos os parâmetros na chamada e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "metadataTemplate": {
    "name": "Test Webhook Audience Template",
    "create": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "update": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "PUT",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "delete": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "createDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/createDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "updateDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/updateDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "deleteDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/deleteDestination",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    }
  },
  "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Propriedade | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `name` | String | O nome do modelo de metadados de público-alvo para o seu destino. Esse nome aparecerá em qualquer mensagem de erro específica do parceiro na interface do usuário do Experience Platform. |
| `url` | String | O URL e o endpoint da API, usados para criar, atualizar, excluir ou validar públicos-alvo e/ou fluxos de dados na plataforma. Dois exemplos de setor são: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | String | O método usado no endpoint para criar, atualizar, excluir ou validar de forma programática o público-alvo no destino. Por exemplo: `POST`, `PUT`, `DELETE` |
| `headers.header` | String | Especifica os cabeçalhos HTTP que devem ser adicionados à chamada para a API. Por exemplo, `"Content-Type"` |
| `headers.value` | String | Especifica o valor de cabeçalhos HTTP que devem ser adicionados à chamada para a API. Por exemplo, `"application/x-www-form-urlencoded"` |
| `requestBody` | String | Especifica o conteúdo do corpo da mensagem que deve ser enviado para a API. Os parâmetros que devem ser adicionados ao objeto `requestBody` dependem dos campos aceitos pela API. Consulte a [documentação de macros com suporte](../functionality/audience-metadata-management.md#macros) para saber o que você pode incluir no corpo da mensagem. |
| `responseFields.name` | String | Especifique quaisquer campos de resposta que sua API retorne quando chamada. Para ver um exemplo, consulte os [exemplos de modelo](../functionality/audience-metadata-management.md#examples) no documento de funcionalidade de metadados de público-alvo. |
| `responseFields.value` | String | Especifique o valor de quaisquer campos de resposta que sua API retorna quando chamada. |
| `responseErrorFields.name` | String | Especifique quaisquer campos de resposta que sua API retorne quando chamada. Para ver um exemplo, consulte os [exemplos de modelo](../functionality/audience-metadata-management.md#examples) no documento de funcionalidade de metadados de público-alvo. |
| `responseErrorFields.value` | String | Analisa todas as mensagens de erro retornadas nas respostas de chamada da API do seu destino. Essas mensagens de erro serão exibidas para os usuários na interface do Experience Platform. |
| `validations.field` | String | Indica se as validações devem ser executadas para qualquer campo antes que as chamadas de API sejam feitas ao destino. Por exemplo, você pode usar `{{validations.accountId}}` para validar a ID da conta do usuário. |
| `validations.regex` | String | Indica como o campo deve ser estruturado para que a validação seja aprovada. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do modelo de público-alvo recém-criado.

+++

## Manipulação de erros de API

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe quando usar modelos de público-alvo e como configurar um modelo de público-alvo usando o ponto de extremidade da API `/authoring/audience-templates`. Leia [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
