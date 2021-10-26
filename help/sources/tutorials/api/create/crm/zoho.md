---
keywords: Experience Platform, home, tópicos populares, Zoho CRM, zoho crm, Zoho, zoho
solution: Experience Platform
title: Criar uma conexão básica do Zoho CRM usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Zoho CRM usando a API do Serviço de Fluxo.
source-git-commit: 7a15090d8ed2c1016d7dc4d7d3d0656640c4785c
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 1%

---

# (Beta) Criar um [!DNL Zoho CRM] conexão básica usando o [!DNL Flow Service] API

>[!NOTE]
>
>O [!DNL Zoho CRM] A fonte está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Zoho CRM] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Zoho CRM] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Zoho CRM], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `endpoint` | O terminal da [!DNL Zoho CRM] servidor para o qual você está fazendo sua solicitação. |
| `accountsUrl` | O URL da conta é usado para gerar seu acesso e atualizar tokens. O URL deve ser específico de domínio. |
| `clientId` | A ID do cliente que corresponde ao seu [!DNL Zoho CRM] conta do usuário. |
| `clientSecret` | O segredo do cliente que corresponde ao seu [!DNL Zoho CRM] conta do usuário. |
| `accessToken` | O token de acesso autoriza o acesso seguro e temporário ao seu [!DNL Zoho CRM] conta. |
| `refreshToken` | Um token de atualização é um token usado para gerar um novo token de acesso depois que o token de acesso expirar. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Zoho CRM] é: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Para obter mais informações sobre essas credenciais, consulte a documentação em [[!DNL Zoho CRM] autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Zoho CRM] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

>[!TIP]
>
>O domínio do URL da conta deve corresponder ao local de domínio apropriado. A seguir estão os vários domínios e os URLs de contas correspondentes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Austrália: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Índia: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

A solicitação a seguir cria uma conexão base para [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --- | --- |
| `name` | O nome da sua [!DNL Zoho CRM] conexão básica. Você pode usar esse nome para pesquisar seu [!DNL Zoho CRM] conexão básica. |
| `description` | Uma descrição opcional para seu [!DNL Zoho CRM] conexão básica. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.endpoint` | O terminal da [!DNL Zoho CRM] servidor para o qual você está fazendo sua solicitação. |
| `auth.params.accountsUrl` | O URL da conta é usado para gerar seu acesso e atualizar tokens. O URL deve ser específico de domínio. |
| `auth.params.clientId` | A ID do cliente que corresponde ao seu [!DNL Zoho CRM] conta do usuário. |
| `auth.params.clientSecret` | O segredo do cliente que corresponde ao seu [!DNL Zoho CRM] conta do usuário. |
| `auth.params.accessToken` | O token de acesso autoriza o acesso seguro e temporário ao seu [!DNL Zoho CRM] conta. |
| `auth.params.refreshToken` | Um token de atualização é um token usado para gerar um novo token de acesso depois que o token de acesso expirar. |
| `connectionSpec.id` | A ID de especificação de conexão para [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Zoho CRM] conexão básica usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explorar sistemas CRM usando a API do Serviço de Fluxo](../../explore/crm.md).
