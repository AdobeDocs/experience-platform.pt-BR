---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas eficazes de Visualização
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# Políticas eficazes de Visualização

Para visualização de políticas eficazes para o usuário atual, faça uma solicitação POST para o ponto de extremidade `/acl/effective-policies` na API do Controle de acesso. As permissões e os tipos de recursos que você deseja recuperar devem ser fornecidos na carga da solicitação na forma de um storage. Isso é demonstrado na chamada de API de exemplo abaixo.

**Formato da API**

```http
POST /acl/effective-policies
```

**Solicitação**

As solicitações a seguir recuperam informações sobre a permissão &quot;Gerenciar conjuntos de dados&quot; e o acesso ao tipo de recurso &quot;schemas&quot; para o usuário atual.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Para obter uma lista completa de permissões e tipos de recursos que podem ser fornecidos no storage de carga, consulte a seção do apêndice sobre permissões e tipos [de recursos](#accepted-permissions-and-resource-types)aceitos.

**Resposta**

Uma resposta bem-sucedida retorna informações sobre as permissões e os tipos de recursos fornecidos na solicitação. A resposta inclui as permissões ativas que o usuário atual tem para os tipos de recursos especificados na solicitação. Se qualquer permissão incluída na carga da solicitação estiver ativa para o usuário atual, a API retornará a permissão com um asterisco (`*`) para indicar que a permissão está ativa. Todas as permissões fornecidas na solicitação que não estão ativas para o usuário são omitidas da carga de resposta.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Próximas etapas

Este documento abordou como fazer chamadas para a API do Controle de acesso para retornar informações sobre permissões ativas e políticas relacionadas para tipos de recursos. Para obter mais informações sobre o controle de acesso, consulte a visão geral [do](../home.md)controle de acesso.

## Apêndice

Esta seção fornece informações adicionais para o uso da API do Controle de acesso.

### Permissões aceitas e tipos de recursos

A seguir está uma lista de permissões e tipos de recursos que podem ser incluídos na carga de uma solicitação POST para o `/acl/active-permissions` ponto de extremidade.

**Permissões**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**Tipos de recursos**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
