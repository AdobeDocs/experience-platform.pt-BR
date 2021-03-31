---
keywords: Experience Platform, home, tópicos populares, sandboxes de lista
solution: Experience Platform
title: Listar sandboxes na API
topic: guia do desenvolvedor
description: Para listar todas as sandboxes pertencentes à sua Organização IMS (ativa ou não), faça uma solicitação do GET ao endpoint /sandboxes .
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 2%

---


# Listar sandboxes na API

Para listar todas as sandboxes pertencentes à sua Organização IMS (ativa ou não), faça uma solicitação GET ao endpoint `/sandboxes` .

**Formato da API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte a seção em [parâmetros de consulta](#query) para obter mais informações. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de sandboxes pertencentes à sua organização, incluindo detalhes como `name`, `title`, `state` e `type`.

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
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform-int.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sandbox. Usado para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da sandbox. |
| `state` | O estado de processamento atual da sandbox. O estado de uma sandbox pode ser qualquer um dos seguintes: <br/><ul><li>**criação**: A sandbox foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>**ativo**: A sandbox é criada e ativa.</li><li>**falhou**: Devido a um erro, a sandbox não pôde ser provisionada pelo sistema e está desativada.</li><li>**suprimido**: A sandbox foi desativada manualmente.</li></ul> |
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