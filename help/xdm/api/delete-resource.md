---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Excluir um recurso
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0

---


# Excluir um recurso

Ocasionalmente, pode ser necessário remover (EXCLUIR) um recurso do Registro do Schema. Somente os recursos criados no container locatário podem ser excluídos. Isso é feito executando-se uma solicitação DELETE usando a parte `$id` do recurso que você deseja excluir.

**Formato da API**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser excluído da Biblioteca de Schemas. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | O `$id` URI codificado por URL ou `meta:altId` do recurso. |

**Solicitação**

As solicitações DELETE não exigem cabeçalhos Accept.

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

Você pode confirmar a exclusão tentando uma solicitação de pesquisa (GET) para o recurso. Você precisará incluir um cabeçalho Accept na solicitação, mas deverá receber um status HTTP 404 (Not Found), pois o recurso foi removido do Registro do Schema.