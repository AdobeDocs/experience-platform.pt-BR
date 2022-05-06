---
keywords: Experience Platform; home; tópicos populares; veeva crm; Veeva CRM; Veeva;
solution: Experience Platform
title: Criar uma conexão básica do CRM Veeva usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a Veeva CRM usando a API do Serviço de Fluxo.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# Crie um [!DNL Veeva CRM] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Veeva CRM] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Veeva CRM] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Veeva CRM], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL do [!DNL Veeva CRM] instância. |
| `username` | O valor do nome de usuário de seu [!DNL Veeva CRM] conta. |
| `password` | O valor da senha de seu [!DNL Veeva CRM] conta. |
| `securityToken` | O token de segurança para seu [!DNL Veeva CRM] instância. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Veeva CRM] é: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Para obter mais informações sobre esses valores, consulte esta seção [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/api/#order-management-rest-api).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Veeva CRM] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --- | --- |
| `name` | O nome da sua [!DNL Veeva CRM] conexão básica. Você pode usar esse nome para pesquisar seu [!DNL Veeva CRM] conexão básica. |
| `description` | Uma descrição opcional para seu [!DNL Veeva CRM] conexão básica. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.environmentUrl` | O URL do [!DNL Veeva CRM] instância. |
| `auth.params.username` | O valor do nome de usuário de seu [!DNL Veeva CRM] conta. |
| `auth.params.password` | O valor da senha de seu [!DNL Veeva CRM] conta. |
| `auth.params.securityToken` | O token de segurança para seu [!DNL Veeva CRM] instância. |
| `connectionSpec.id` | A ID de especificação de conexão para [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Veeva CRM] conexão básica usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando o [!DNL Flow Service] API](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para a plataforma usando o [!DNL Flow Service] API](../../collect/crm.md)
