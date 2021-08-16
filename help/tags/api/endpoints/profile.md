---
title: Ponto de extremidade de perfis
description: Saiba como fazer chamadas para o endpoint /profiles na API do Reator.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 5%

---

# Ponto de extremidade do perfil

Na API do reator, um perfil representa um usuário do Adobe Experience Platform. A API do reator não mantém seu próprio banco de dados de usuários e permissões e, em vez disso, depende de IDs de Adobe gerenciadas pelo [Adobe&#39;s identity management system (IMS)](https://helpx.adobe.com/br/enterprise/using/identity.html).

Um perfil contém todas as informações sobre o usuário conectado, incluindo todas as Organizações IMS às quais ele pertence, os perfis de produto aos quais ele pertence em cada Organização e os direitos que eles têm de cada perfil de produto.

## Introdução

O endpoint usado neste guia faz parte da [API do reator](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes sobre como autenticar para a API.

## Recuperar o perfil atual {#lookup}

Você pode recuperar os detalhes do perfil conectado no momento fazendo uma solicitação de GET para o endpoint `/profile`.

**Formato da API**

```http
GET /profile
```

**Solicitação**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do perfil.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```

