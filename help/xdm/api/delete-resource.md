---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;delete
solution: Experience Platform
title: Excluir um recurso
describe: It may occasionally be necessary to remove resource from the Schema Registry. Only resources that you create in the tenant container may be deleted. This is done by performing a DELETE request using the $id of the resource you wish to delete.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# Excluir um recurso

Ocasionalmente, pode ser necessário remover (DELETE) um recurso do [!DNL Schema Registry]. Somente os recursos criados no container locatário podem ser excluídos. Isso é feito executando-se uma solicitação de DELETE usando o `$id` do recurso que você deseja excluir.

**Formato da API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser excluído do [!DNL Schema Library]. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | O `$id` URI codificado por URL ou `meta:altId` do recurso. |

**Solicitação**

As solicitações de DELETE não exigem cabeçalhos Aceitar.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o recurso. Você precisará incluir um cabeçalho Accept na solicitação, mas deverá receber um status HTTP 404 (Not Found), pois o recurso foi removido do [!DNL Schema Registry].