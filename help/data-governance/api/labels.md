---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ponto de extremidade de etiquetas
topic: developer guide
translation-type: tm+mt
source-git-commit: 80526bc0fea9e1854174a2edf9389ff0c4e98f71
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---


# Ponto de extremidade de etiquetas

Os rótulos de uso de dados permitem que você categorize dados de acordo com as políticas de uso que podem se aplicar a esses dados. O `/labels` endpoint no aplicativo [!DNL Policy Service API] permite gerenciar programaticamente as etiquetas de uso de dados no aplicativo de experiência.

>[!NOTE]
>
>O `/labels` ponto de extremidade é usado apenas para recuperar, criar e atualizar rótulos de uso de dados. Para obter etapas sobre como adicionar rótulos a conjuntos de dados e campos usando chamadas de API, consulte o guia sobre como [gerenciar rótulos](../labels/dataset-api.md)de conjuntos de dados.

## Introdução

O endpoint da API usado neste guia faz parte do [!DNL Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Antes de continuar, reveja o guia [de](getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Recuperar uma lista de etiquetas {#list}

É possível lista de todas as `core` ou `custom` etiquetas fazendo uma solicitação de GET para `/labels/core` ou `/labels/custom`, respectivamente.

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

Uma resposta bem-sucedida retorna uma lista de rótulos personalizados recuperados do sistema. Como a solicitação de exemplo acima foi feita para `/labels/custom`, a resposta abaixo mostra somente rótulos personalizados.

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

## Procurar uma etiqueta {#look-up}

Você pode procurar um rótulo específico incluindo a propriedade desse rótulo no caminho de uma solicitação de GET para a `name` [!DNL Policy Service] API.

**Formato da API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | A `name` propriedade do rótulo personalizado que você deseja pesquisar. |

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

Para criar ou atualizar um rótulo personalizado, é necessário fazer uma solicitação PUT para a [!DNL Policy Service] API.

**Formato da API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{LABEL_NAME}` | A `name` propriedade de um rótulo personalizado. Se um rótulo personalizado com esse nome não existir, um novo rótulo será criado. Se existir, esse rótulo será atualizado. |

**Solicitação**

A solicitação a seguir cria um novo rótulo, `L3`que tem como objetivo descrever os dados que contêm informações relacionadas aos planos de pagamento selecionados dos clientes.

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
| `name` | Um identificador de string exclusivo para o rótulo. Esse valor é usado para fins de pesquisa e aplicação do rótulo a conjuntos de dados e campos, portanto, recomenda-se que seja curto e conciso. |
| `category` | A categoria da etiqueta. Embora você possa criar suas próprias categorias para rótulos personalizados, é altamente recomendável usar `Custom` se quiser que o rótulo apareça na interface do usuário. |
| `friendlyName` | Um nome amigável para o rótulo, usado para fins de exibição. |
| `description` | (Opcional) Uma descrição do rótulo para fornecer mais contexto. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do rótulo personalizado, com o código HTTP 200 (OK) se um rótulo existente foi atualizado, ou 201 (Criado) se um novo rótulo foi criado.

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

Este guia cobriu o uso do ponto de extremidade `/labels` na API do Serviço de Política. Para obter etapas sobre como aplicar rótulos a conjuntos de dados e campos, consulte o guia [da API de etiquetas de](../labels/dataset-api.md)conjuntos de dados.