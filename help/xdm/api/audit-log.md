---
keywords: Experience Platform;home;popular topics;api;API;XDM;sistema XDM;modelo de dados da experiência;Modelo de dados da experiência;Modelo de dados da experiência;modelo de dados;modelo de dados;auditoria;registro de auditoria;changelog;change log;rpc;
solution: Experience Platform
title: Ponto Final da API de Log de Auditoria
description: O endpoint /auditlog na API do Registro de Schemas permite recuperar uma lista cronológica de alterações que foram feitas em um recurso XDM existente.
topic: developer guide
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---


# Ponto de extremidade do log de auditoria

Para cada recurso do Experience Data Model (XDM), o [!DNL Schema Registry] mantém um log de todas as alterações que ocorreram entre diferentes atualizações. O terminal `/auditlog` na API [!DNL Schema Registry] permite recuperar um log de auditoria para qualquer classe, combinação, tipo de dados ou schema especificado pela ID.

## Introdução

O endpoint usado neste guia faz parte da [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

O terminal `/auditlog` faz parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Ao contrário de outros pontos de extremidade na API [!DNL Schema Registry], os pontos de extremidade RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type` e não usam um `CONTAINER_ID`. Em vez disso, eles devem usar a namespace `/rpc`, como demonstrado na chamada de API abaixo.

## Recuperar um log de auditoria para um recurso

Você pode recuperar um log de auditoria para qualquer classe, combinação, tipo de dados ou schema na Biblioteca de Schemas especificando a ID do recurso no caminho de uma solicitação de GET para o terminal `/auditlog`.

**Formato da API**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_ID}` | O `meta:altId` ou o URL codificado `$id` do recurso cujo log de auditoria você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera o log de auditoria para uma combinação `Restaurant`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista cronológica das alterações feitas no recurso, da mais recente para a menos recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
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
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
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
| `id` | O `$id` do recurso que foi alterado. Normalmente, esse valor representará o recurso especificado no caminho da solicitação, mas poderá representar um recurso dependente se essa for a fonte da alteração. |
| `action` | O tipo de mudança que foi feita. |
| `path` | Uma string [Ponteiro JSON](../../landing/api-fundamentals.md#json-pointer) que indica o caminho para o campo específico que foi alterado ou adicionado. |
| `value` | O valor que foi atribuído ao campo novo ou atualizado. |