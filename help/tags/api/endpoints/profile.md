---
title: Ponto de extremidade de perfis
description: Saiba como fazer chamadas para o ponto de extremidade /profiles na API do reator.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 97%

---

# Ponto de extremidade do perfil

Na API do Reactor, um perfil representa um usuário da Adobe Experience Platform. A API do Reactor não mantém seu próprio banco de dados de usuários e permissões. Em vez disso, depende de Adobe IDs gerenciadas pelo [Sistema de gerenciamento de identidades (IMS) da Adobe](https://helpx.adobe.com/br/enterprise/using/identity.html).

Um perfil contém todas as informações sobre o usuário conectado, incluindo todas as Organizações IMS às quais ele pertence, os perfis de produto aos quais ele pertence em cada Organização e os direitos que eles têm de cada perfil de produto.

## Introdução

O endpoint usado neste manual faz parte da [API do Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte o [guia de introdução](../getting-started.md) para obter informações importantes sobre como realizar a autenticação na API.

## Recuperar o perfil atual {#lookup}

Você pode recuperar os detalhes do perfil conectado no momento fazendo uma solicitação GET para o ponto de extremidade `/profile`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
