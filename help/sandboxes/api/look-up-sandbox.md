---
keywords: Experience Platform, home, tópicos populares, encontrar sandbox, procurar uma sandbox
solution: Experience Platform
title: Pesquisar uma sandbox na API
topic: guia do desenvolvedor
description: Você pode pesquisar uma sandbox individual fazendo uma solicitação do GET que inclui a propriedade name da sandbox no caminho da solicitação.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---


# Pesquisar uma sandbox na API

Você pode pesquisar uma sandbox individual fazendo uma solicitação do GET que inclui a propriedade `name` da sandbox no caminho da solicitação.

**Formato da API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja procurar. |

**Solicitação**

A solicitação a seguir recupera uma sandbox chamada &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox, incluindo `name`, `title`, `state` e `type`.

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
| `name` | O nome da sandbox. Usado para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da sandbox. |
| `state` | O estado de processamento atual da sandbox. O estado de uma sandbox pode ser qualquer um dos seguintes: <ul><li>**criação**: A sandbox foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>**ativo**: A sandbox é criada e ativa.</li><li>**falhou**: Devido a um erro, a sandbox não pôde ser provisionada pelo sistema e está desativada.</li><li>**suprimido**: A sandbox foi desativada manualmente.</li></ul> |
| `type` | O tipo de sandbox, seja &quot;desenvolvimento&quot; ou &quot;produção&quot;. |
| `isDefault` | Uma propriedade booleana que indica se essa sandbox é a sandbox padrão da organização. Normalmente, essa é a sandbox de produção. |
| `eTag` | Um identificador para uma versão específica da sandbox. Usado para controle de versão e eficiência de armazenamento em cache, esse valor é atualizado sempre que uma alteração é feita na sandbox. |