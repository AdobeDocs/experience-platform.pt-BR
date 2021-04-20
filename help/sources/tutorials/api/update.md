---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, atualizar contas
solution: Experience Platform
title: Atualizar contas usando a API do Serviço de fluxo
topic: overview
type: Tutorial
description: Este tutorial aborda as etapas para atualizar os detalhes e as credenciais de uma conta usando a API do Serviço de Fluxo.
translation-type: tm+mt
source-git-commit: 37be5f5ffa4640d7d4442a24cc257069237f15cb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Atualizar contas usando a API de Serviço de Fluxo

Em algumas circunstâncias, pode ser necessário atualizar os detalhes de uma conexão de origem existente. [!DNL Flow Service] O fornece a capacidade de adicionar, editar e excluir detalhes de um lote ou conexão de transmissão existente, incluindo o nome, descrição e credenciais.

Este tutorial aborda as etapas para atualizar os detalhes e as credenciais de uma conexão usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este tutorial requer uma conexão existente e uma ID de conexão válida. Se você não tiver uma conexão existente, selecione sua fonte de escolha na [visão geral das fontes](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para atualizar com êxito uma conexão usando a API [!DNL Flow Service].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da plataforma, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos no Experience Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Procurar detalhes da ligação

A primeira etapa da atualização da conexão é recuperar os detalhes usando a ID da conexão. Para recuperar os detalhes atuais da conexão, faça uma solicitação GET para a API [!DNL Flow Service] enquanto fornece a ID da conexão, da conexão que deseja atualizar.

**Formato da API**

```http
GET /connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor exclusivo `id` para a conexão que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera informações relacionadas à conexão.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes atuais da conexão, incluindo suas credenciais, o identificador exclusivo (`id`) e a versão. O valor da versão é necessário para atualizar a conexão.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Atualizar conexão

Para atualizar o nome, a descrição e as credenciais da conexão, execute uma solicitação de PATCH para a API [!DNL Flow Service], fornecendo a ID da conexão, a versão e as novas informações que deseja usar.

>[!IMPORTANT]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação de PATCH. O valor desse cabeçalho é a versão exclusiva da conexão que você deseja atualizar.

**Formato da API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor exclusivo `id` para a conexão que você deseja atualizar. |

**Solicitação**

A solicitação a seguir fornece um novo nome e descrição, bem como um novo conjunto de credenciais, para atualizar sua conexão.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar a conexão. As operações incluem: `add`, `replace` e `remove`. |
| `path` | O caminho do parâmetro a ser atualizado. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID da conexão e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service], fornecendo a ID da conexão.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você atualizou as credenciais e as informações associadas à conexão usando a API [!DNL Flow Service]. Para obter mais informações sobre como usar conectores de origem, consulte a [visão geral das fontes](../../home.md).
