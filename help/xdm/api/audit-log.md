---
keywords: Experience Platform;página inicial;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;auditoria;log de auditoria;changelog;log de alterações;rpc;
solution: Experience Platform
title: Endpoint da API de Log de Auditoria
description: O ponto de extremidade /auditlog na API do registro de esquema permite recuperar uma lista cronológica de alterações feitas em um recurso XDM existente.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 5%

---

# Endpoint do log de auditoria

Para cada recurso do Experience Data Model (XDM), a variável [!DNL Schema Registry] O mantém um log de todas as alterações que ocorreram entre atualizações diferentes. A variável `/auditlog` endpoint na variável [!DNL Schema Registry] A API permite recuperar um log de auditoria para qualquer classe, grupo de campos de esquema, tipo de dados ou esquema especificado pela ID.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

A variável `/auditlog` O ponto de extremidade faz parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Ao contrário de outros endpoints no [!DNL Schema Registry] API, os pontos de extremidade RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type`, e não use um `CONTAINER_ID`. Em vez disso, eles devem usar o `/rpc` conforme demonstrado na chamada de API abaixo.

## Recuperar um log de auditoria para um recurso

Você pode recuperar um log de auditoria para qualquer classe, grupo de campos, tipo de dados ou esquema na Biblioteca de esquemas especificando a ID do recurso no caminho de uma solicitação GET para a `/auditlog` terminal.

**Formato da API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_ID}` | A variável `meta:altId` ou codificado em URL `$id` do recurso cujo log de auditoria você deseja recuperar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera o log de auditoria de um esquema.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista cronológica de alterações feitas no recurso, da mais recente para a menos recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Propriedade | Descrição |
| --- | --- |
| `updates` | Uma matriz de objetos, com cada objeto representando uma alteração feita no recurso especificado ou em um de seus recursos dependentes. |
| `id` | A variável `$id` do recurso que foi alterado. Normalmente, esse valor representa o recurso especificado no caminho da solicitação, mas pode representar um recurso dependente se essa for a origem da alteração. |
| `xdmType` | O tipo de recurso que foi alterado. |
| `action` | O tipo de alteração que foi feita. |
| `path` | A [Ponteiro JSON](../../landing/api-fundamentals.md#json-pointer) string que indica o caminho para o campo específico que foi alterado ou adicionado. |
| `value` | O valor atribuído ao campo novo ou atualizado. |

{style="table-layout:auto"}
