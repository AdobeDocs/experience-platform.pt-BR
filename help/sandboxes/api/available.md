---
keywords: Experience Platform, home, tópicos populares, sandboxes disponíveis de lista, sandboxes de lista
solution: Experience Platform
title: Ponto de extremidade da API de sandboxes disponível
topic-legacy: developer guide
description: Você pode listar as sandboxes disponíveis para o usuário atual fazendo uma solicitação do GET para o endpoint de sandboxes disponível.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 3%

---

# Ponto de extremidade de sandboxes disponível

>[!NOTE]
>
>Ao contrário de outros endpoints fornecidos na API do Sandbox, esse endpoint está disponível para todos os usuários, incluindo aqueles sem permissões de acesso à Administração do Sandbox.

Você pode listar as sandboxes disponíveis para o usuário atual fazendo uma solicitação do GET para o endpoint de sandboxes disponível.

**Formato da API**

```http
GET /{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte a [documento de apêndice](./appendix.md#query) para obter uma lista de parâmetros disponíveis. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de sandboxes disponíveis para o usuário atual, incluindo detalhes como `name`, `title`, `state`e `type`.

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
| `state` | O estado de processamento atual da sandbox. O estado de uma sandbox pode ser qualquer um dos seguintes: <ul><li>`creating`: A sandbox foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>`active`: A sandbox é criada e ativa.</li><li>`failed`: Devido a um erro, a sandbox não pôde ser provisionada pelo sistema e está desativada.</li><li>`deleted`: A sandbox foi desativada manualmente.</li></ul> |
| `type` | O tipo de sandbox, seja &quot;desenvolvimento&quot; ou &quot;produção&quot;. |
| `isDefault` | Uma propriedade booleana que indica se essa sandbox é a sandbox de produção padrão da organização. |
| `eTag` | Um identificador para uma versão específica da sandbox. Usado para controle de versão e eficiência de armazenamento em cache, esse valor é atualizado sempre que uma alteração é feita na sandbox. |
