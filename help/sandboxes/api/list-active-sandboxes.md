---
keywords: Experience Platform, home, tópicos populares, sandboxes ativas de lista, sandboxes de lista
solution: Experience Platform
title: Listar sandboxes ativas para o usuário atual na API
topic: guia do desenvolvedor
description: Você pode listar as sandboxes que estão ativas para o usuário atual fazendo uma solicitação do GET para o endpoint da raiz.
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---


# Listar sandboxes ativas para o usuário atual na API

>[!NOTE]
>
>Ao contrário de outros endpoints fornecidos na API do Sandbox, esse endpoint está disponível para todos os usuários, incluindo aqueles sem permissões de acesso à Administração do Sandbox.

Você pode listar as sandboxes que estão ativas para o usuário atual fazendo uma solicitação GET para o endpoint raiz (`/`).

**Formato da API**

```http
GET /{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte a seção em [parâmetros de consulta](#query) para obter mais informações. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de sandboxes ativas para o usuário atual, incluindo detalhes como `name`, `title`, `state` e `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sandbox. Usado para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da sandbox. |
| `state` | O estado de processamento atual da sandbox. O estado de uma sandbox pode ser qualquer um dos seguintes: <ul><li>**criação**: A sandbox foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>**ativo**: A sandbox é criada e ativa.</li><li>**falhou**: Devido a um erro, a sandbox não pôde ser provisionada pelo sistema e está desativada.</li><li>**suprimido**: A sandbox foi desativada manualmente.</li></ul> |
| `type` | O tipo de sandbox, seja &quot;desenvolvimento&quot; ou &quot;produção&quot;. |
| `isDefault` | Uma propriedade booleana que indica se essa sandbox é a sandbox padrão da organização. Normalmente, essa é a sandbox de produção. |
| `eTag` | Um identificador para uma versão específica da sandbox. Usado para controle de versão e eficiência de armazenamento em cache, esse valor é atualizado sempre que uma alteração é feita na sandbox. |

## Uso de parâmetros de consulta {#query}

A API [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) oferece suporte ao uso de parâmetros de consulta para página e filtrar resultados ao listar sandboxes.

>[!NOTE]
>
>Os parâmetros de consulta `limit` e `offset` devem ser especificados juntos. Se você especificar apenas um, a API retornará um erro. Se você especificar nenhum, o limite padrão é 50 e o deslocamento é 0.

| Parâmetro | Descrição |
| --------- | ----------- |
| `limit` | O número máximo de registros a serem retornados na resposta. |
| `offset` | O número de entidades do primeiro registro para iniciar (deslocar) a lista de resposta. |
