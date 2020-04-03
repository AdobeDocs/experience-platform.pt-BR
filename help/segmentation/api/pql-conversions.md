---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conversões de PQL
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# Conversões de PQL

introdução

- Converter formatação de pql/text e pql/json

## Introdução

Os pontos finais da API usados neste guia fazem parte da API de segmentação. Antes de continuar, consulte o guia [do desenvolvedor de](./getting-started.md)Segmentação.

Em particular, a seção [de](./getting-started.md#getting-started) introdução do guia do desenvolvedor de Segmentação inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra no documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API da plataforma de experiência.

## Converter formatação de pql/text e pql/json

**Formato da API**

```http
POST /segment/conversion
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome exclusivo para a definição do segmento. |
| `expression.type` | O tipo de expressão. Pode ser `PQL` ou `ARL`. |
| `expression.format` | O formato de expressão. Pode ser `pql/text` ou `pql/json`. |
| `expression.value` | A string de query da expressão que você deseja converter. |
| `schema.name` | A ID de classe do schema que você está referenciando. |
| `ttlInDays` | Um número inteiro que representa o tempo de vida (TTL). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do segmento convertido.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Próximas etapas
