---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Procurar uma caixa de areia
topic: developer guide
translation-type: tm+mt
source-git-commit: ef423a8c1b412315d03cddf7d8c351a232eb509b
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---


# Procurar uma caixa de areia

Você pode procurar uma caixa de proteção individual fazendo uma solicitação de GET que inclua a propriedade da caixa de proteção `name` no caminho da solicitação.

**Formato da API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A `name` propriedade da caixa de proteção que você deseja procurar. |

**Solicitação**

A solicitação a seguir recupera uma caixa de proteção chamada &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da caixa de proteção, incluindo suas `name`informações, `title`, `state`e `type`.

```json
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
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da caixa de proteção. Usada para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da caixa de proteção. |
| `state` | O estado de processamento atual da caixa de proteção. O estado de uma caixa de proteção pode ser qualquer um dos seguintes: <ul><li>**criação**: A caixa de proteção foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>**ativo**: A caixa de proteção é criada e ativa.</li><li>**falha**: Devido a um erro, a caixa de proteção não pôde ser provisionada pelo sistema e está desativada.</li><li>**suprimido**: A caixa de proteção foi desativada manualmente.</li></ul> |
| `type` | O tipo de caixa de proteção, &quot;desenvolvimento&quot; ou &quot;produção&quot;. |
| `isDefault` | Uma propriedade booleana que indica se essa caixa de proteção é a caixa de proteção padrão da organização. Normalmente, essa é a caixa de proteção de produção. |
| `eTag` | Um identificador para uma versão específica da caixa de proteção. Usado para controle de versão e eficiência de cache, esse valor é atualizado sempre que uma alteração é feita na caixa de proteção. |