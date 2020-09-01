---
keywords: Experience Platform;home;popular topics;list active sandboxes;list sandboxes
solution: Experience Platform
title: Lista de caixas de proteção ativas para o usuário atual
topic: developer guide
description: Você pode lista as caixas de proteção que estão ativas para o usuário atual, fazendo uma solicitação de GET para o terminal raiz.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---


# Lista de caixas de proteção ativas para o usuário atual

>[!NOTE]
>
>Diferentemente de outros pontos de extremidade fornecidos na API do Sandbox, esse ponto de extremidade está disponível para todos os usuários, incluindo aqueles sem permissões de acesso à Administração do Sandbox.

Você pode lista as caixas de proteção que estão ativas para o usuário atual, fazendo uma solicitação de GET para o ponto de extremidade raiz (`/`).

**Formato da API**

```http
GET /
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/ \
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
    ]
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
