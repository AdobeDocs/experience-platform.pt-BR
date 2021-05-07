---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, auditoria, log de auditoria, log de alterações, log de alterações, rpc;
solution: Experience Platform
title: Ponto de extremidade da API de log de auditoria
description: O endpoint /auditlog na API do Registro de Schema permite recuperar uma lista cronológica de alterações feitas em um recurso XDM existente.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---

# Ponto de extremidade de log de auditoria

Para cada recurso do Experience Data Model (XDM), o [!DNL Schema Registry] mantém um log de todas as alterações que ocorreram entre diferentes atualizações. O endpoint `/auditlog` na API [!DNL Schema Registry] permite recuperar um log de auditoria para qualquer classe, grupo de campos de esquema, tipo de dados ou schema especificado pela ID.

## Introdução

O endpoint usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

O ponto de extremidade `/auditlog` faz parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Ao contrário de outros endpoints na API [!DNL Schema Registry], os endpoints RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type` e não usam um `CONTAINER_ID`. Em vez disso, eles devem usar o namespace `/rpc`, conforme demonstrado na chamada de API abaixo.

## Recuperar um log de auditoria de um recurso

Você pode recuperar um log de auditoria para qualquer classe, grupo de campos, tipo de dados ou esquema na Biblioteca de Esquemas especificando a ID do recurso no caminho de uma solicitação de GET para o endpoint `/auditlog`.

**Formato da API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_ID}` | O `meta:altId` ou `$id` codificado por URL do recurso cujo log de auditoria você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera o log de auditoria de um grupo de campos `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.fieldgroups.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista cronológica de alterações feitas no recurso, da mais recente para a menos recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "fieldgroups",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "fieldgroups",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Propriedade | Descrição |
| --- | --- |
| `auditTrails` | Uma matriz de objetos, com cada objeto representando uma alteração feita no recurso especificado ou um de seus recursos dependentes. |
| `id` | O `$id` do recurso que foi alterado. Normalmente, esse valor representa o recurso especificado no caminho da solicitação, mas pode representar um recurso dependente se essa for a fonte da alteração. |
| `action` | O tipo de mudança que foi feita. |
| `path` | Uma string [JSON Pointer](../../landing/api-fundamentals.md#json-pointer) indicando o caminho para o campo específico que foi alterado ou adicionado. |
| `value` | O valor atribuído ao campo novo ou atualizado. |
