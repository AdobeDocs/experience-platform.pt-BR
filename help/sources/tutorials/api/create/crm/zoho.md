---
keywords: Experience Platform;página inicial;tópicos populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Criar uma conexão base do Zoho CRM usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Zoho CRM usando a API do Serviço de fluxo.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 3%

---

# Criar uma conexão de base [!DNL Zoho CRM] usando a API [!DNL Flow Service]

>[!IMPORTANT]
>
>A origem [!DNL Zoho CRM] será substituída no final de junho de 2025. Você pode usar o [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) no lugar da origem [!DNL Zoho CRM].

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Zoho CRM] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisa saber para se conectar com êxito ao [!DNL Zoho CRM] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Zoho CRM], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| `endpoint` | O ponto de extremidade do servidor [!DNL Zoho CRM] ao qual você está fazendo sua solicitação. |
| `accountsUrl` | O URL das contas é usado para gerar os tokens de acesso e atualização. O URL deve ser específico do domínio. |
| `clientId` | A ID do cliente que corresponde à sua conta de usuário do [!DNL Zoho CRM]. |
| `clientSecret` | O segredo do cliente que corresponde à conta de usuário [!DNL Zoho CRM]. |
| `accessToken` | O token de acesso autoriza seu acesso seguro e temporário à sua conta do [!DNL Zoho CRM]. |
| `refreshToken` | Um token de atualização é um token usado para gerar um novo token de acesso depois que ele expirar. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Zoho CRM] é: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Para obter mais informações sobre essas credenciais, consulte a documentação sobre [[!DNL Zoho CRM] autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual sobre [introdução às APIs da Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e sua ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` enquanto fornece suas credenciais de autenticação [!DNL Zoho CRM] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

>[!TIP]
>
>O domínio da URL das contas deve corresponder ao local de domínio apropriado. A seguir estão os vários domínios e suas URLs de contas correspondentes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Austrália: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Índia: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

A solicitação a seguir cria uma conexão base para [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | O nome da sua conexão base [!DNL Zoho CRM]. Você pode usar este nome para pesquisar sua conexão base [!DNL Zoho CRM]. |
| `description` | Uma descrição opcional para sua conexão de base [!DNL Zoho CRM]. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.endpoint` | O ponto de extremidade do servidor [!DNL Zoho CRM] ao qual você está fazendo sua solicitação. |
| `auth.params.accountsUrl` | O URL das contas é usado para gerar os tokens de acesso e atualização. O URL deve ser específico do domínio. |
| `auth.params.clientId` | A ID do cliente que corresponde à sua conta de usuário do [!DNL Zoho CRM]. |
| `auth.params.clientSecret` | O segredo do cliente que corresponde à conta de usuário [!DNL Zoho CRM]. |
| `auth.params.accessToken` | O token de acesso autoriza seu acesso seguro e temporário à sua conta do [!DNL Zoho CRM]. |
| `auth.params.refreshToken` | Um token de atualização é um token usado para gerar um novo token de acesso depois que ele expirar. |
| `connectionSpec.id` | A ID da especificação de conexão para [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Zoho] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] ](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do CRM para a Platform usando a API  [!DNL Flow Service] ](../../collect/crm.md)
