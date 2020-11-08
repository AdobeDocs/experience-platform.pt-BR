---
keywords: Experience Platform;home;popular topics;list active sandboxes;list sandboxes
solution: Experience Platform
title: Lista de caixas de proteção ativas para o usuário atual
topic: developer guide
description: Você pode lista as caixas de proteção que estão ativas para o usuário atual, fazendo uma solicitação de GET para o terminal raiz.
translation-type: tm+mt
source-git-commit: 6326b3072737acf30ba2aee7081ce28dc9627a9a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---


# Lista de caixas de proteção ativas para o usuário atual

>[!NOTE]
>
>Diferentemente de outros pontos de extremidade fornecidos na API do Sandbox, esse ponto de extremidade está disponível para todos os usuários, incluindo aqueles sem permissões de acesso à Administração do Sandbox.

Você pode lista as caixas de proteção que estão ativas para o usuário atual, fazendo uma solicitação de GET para o ponto de extremidade raiz (`/`).

**Formato da API**

```http
GET /{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parâmetros de query opcionais para filtrar os resultados. Consulte a seção sobre parâmetros [de](#query) query para obter mais informações. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de caixas de proteção ativas para o usuário atual, incluindo detalhes como `name`, `title`, `state`e `type`.

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
| `name` | O nome da caixa de proteção. Usada para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da caixa de proteção. |
| `state` | O estado de processamento atual da caixa de proteção. O estado de uma caixa de proteção pode ser qualquer um dos seguintes: <ul><li>**criação**: A caixa de proteção foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>**ativo**: A caixa de proteção é criada e ativa.</li><li>**falha**: Devido a um erro, a caixa de proteção não pôde ser provisionada pelo sistema e está desativada.</li><li>**suprimido**: A caixa de proteção foi desativada manualmente.</li></ul> |
| `type` | O tipo de caixa de proteção, &quot;desenvolvimento&quot; ou &quot;produção&quot;. |
| `isDefault` | Uma propriedade booleana que indica se essa caixa de proteção é a caixa de proteção padrão da organização. Normalmente, essa é a caixa de proteção de produção. |
| `eTag` | Um identificador para uma versão específica da caixa de proteção. Usado para controle de versão e eficiência de cache, esse valor é atualizado sempre que uma alteração é feita na caixa de proteção. |

## Uso de parâmetros de query {#query}

A [[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) API suporta o uso de parâmetros de query para a página e filtrar resultados ao listar caixas de proteção.

>[!NOTE]
>
>Os parâmetros `limit` e `offset` query devem ser especificados juntos. Se você especificar apenas um, a API retornará um erro. Se você especificar nenhum, o limite padrão será 50 e o deslocamento será 0.

| Parâmetro | Descrição |
| --------- | ----------- |
| `limit` | O número máximo de registros a serem retornados na resposta. |
| `offset` | O número de entidades do primeiro registro para o start (deslocamento) da lista de resposta. |
