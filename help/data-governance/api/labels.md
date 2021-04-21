---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Rótulos do ponto de extremidade da API
topic-legacy: developer guide
description: Saiba como gerenciar rótulos de uso de dados no Experience Platform usando a API do serviço de política.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Ponto de extremidade de rótulos

Os rótulos de uso de dados permitem categorizar os dados de acordo com as políticas de uso que podem se aplicar a esses dados. O endpoint `/labels` no [!DNL Policy Service API] permite gerenciar programaticamente os rótulos de uso de dados no aplicativo de experiência.

>[!NOTE]
>
>O endpoint `/labels` é usado apenas para recuperar, criar e atualizar rótulos de uso de dados. Para obter etapas sobre como adicionar rótulos a conjuntos de dados e campos usando chamadas de API, consulte o guia em [gerenciar rótulos de conjunto de dados](../labels/dataset-api.md).

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API [!DNL Experience Platform].

## Recuperar uma lista de rótulos {#list}

Você pode listar todos os rótulos `core` ou `custom` fazendo uma solicitação GET para `/labels/core` ou `/labels/custom`, respectivamente.

**Formato da API**

```http
GET /labels/core
GET /labels/custom
```

**Solicitação**

A solicitação a seguir lista todos os rótulos personalizados criados em sua organização.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de rótulos personalizados recuperados do sistema. Como a solicitação de exemplo acima foi feita para `/labels/custom`, a resposta abaixo mostra apenas rótulos personalizados.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Procure um rótulo {#look-up}

Você pode pesquisar um rótulo específico incluindo a propriedade `name` desse rótulo no caminho de uma solicitação GET para a API [!DNL Policy Service].

**Formato da API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | A propriedade `name` do rótulo personalizado que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera o rótulo personalizado `L2`, conforme indicado no caminho.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do rótulo personalizado.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Criar ou atualizar um rótulo personalizado {#create-update}

Para criar ou atualizar um rótulo personalizado, você deve fazer uma solicitação PUT para a API [!DNL Policy Service].

**Formato da API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | A propriedade `name` de um rótulo personalizado. Se um rótulo personalizado com esse nome não existir, um novo rótulo será criado. Se existir, esse rótulo será atualizado. |

**Solicitação**

A solicitação a seguir cria um novo rótulo, `L3`, que visa descrever dados que contêm informações relacionadas aos planos de pagamento selecionados dos clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | Um identificador de string exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e aplicação do rótulo a conjuntos de dados e campos, portanto, é recomendável que seja curto e conciso. |
| `category` | A categoria do rótulo. Embora você possa criar suas próprias categorias para rótulos personalizados, é altamente recomendável usar `Custom` se desejar que o rótulo apareça na interface do usuário. |
| `friendlyName` | Um nome amigável para o rótulo, usado para fins de exibição. |
| `description` | (Opcional) Uma descrição do rótulo para fornecer contexto adicional. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do rótulo personalizado, com código HTTP 200 (OK) se um rótulo existente foi atualizado, ou 201 (Criado) se um novo rótulo foi criado.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Próximas etapas

Este guia cobriu o uso do ponto de extremidade `/labels` na API do Serviço de política . Para obter etapas sobre como aplicar rótulos a conjuntos de dados e campos, consulte o [guia da API de rótulos de conjunto de dados](../labels/dataset-api.md).
