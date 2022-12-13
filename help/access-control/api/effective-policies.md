---
keywords: Experience Platform, home, tópicos populares, políticas eficazes, api de controle de acesso
solution: Experience Platform
title: Endpoint da API de políticas efetivas
topic-legacy: developer guide
description: Saiba como visualizar políticas de acesso efetivas usando a API de controle de acesso do Adobe Experience Platform.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%

---

# Ponto final de políticas efetivas

Para exibir políticas eficazes de controle de acesso para o usuário atual, faça uma solicitação de POST para a `/acl/effective-policies` endpoint no [!DNL Access Control] API. As permissões e os tipos de recursos que você deseja recuperar devem ser fornecidos na carga da solicitação no formato de um storage. Isso é demonstrado na chamada de API de exemplo abaixo.

**Formato da API**

```http
POST /acl/effective-policies
```

**Solicitação**

As solicitações a seguir recuperam informações sobre o &quot;[!UICONTROL Gerenciar conjuntos de dados]&quot; e acesso ao &quot;[!UICONTROL esquemas]&quot; tipo de recurso para o usuário atual.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Para obter uma lista completa de permissões e tipos de recursos que podem ser fornecidos na matriz de carga, consulte a seção Apêndice em [permissões e tipos de recursos aceitos](#accepted-permissions-and-resource-types).

**Resposta**

Uma resposta bem-sucedida retorna informações sobre as permissões e os tipos de recursos fornecidos na solicitação. A resposta inclui as permissões ativas que o usuário atual tem para os tipos de recursos especificados na solicitação. Se qualquer permissão incluída no payload da solicitação estiver ativa para o usuário atual, a API retornará a permissão com um asterisco (`*`) para indicar que a permissão está ativa. Quaisquer permissões fornecidas na solicitação que não estejam ativas para o usuário são omitidas do payload da resposta.

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

Este documento cobriu como fazer chamadas para o [!DNL Access Control] API para retornar informações sobre permissões ativas e políticas de acesso relacionadas para tipos de recursos. Para obter mais informações sobre o controle de acesso para [!DNL Experience Platform], consulte o [visão geral do controle de acesso](../home.md).

## Apêndice

Esta seção fornece informações complementares para usar a variável [!DNL Access Control] API.

### Permissões aceitas e tipos de recursos

Esta é uma lista de permissões e tipos de recursos que você pode incluir na carga de uma solicitação do POST para o `/acl/active-permissions` endpoint .

**Permissões**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**Tipos de recursos**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
