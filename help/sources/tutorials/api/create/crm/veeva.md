---
keywords: Experience Platform; home; tópicos populares; veeva crm; Veeva CRM; Veeva;
solution: Experience Platform
title: Criar uma conexão básica do CRM Veeva usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a Veeva CRM usando a API do Serviço de Fluxo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 9bd241d5f986759268edd072cee72d02f40f858f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# (Beta) Crie uma conexão base [!DNL Veeva CRM] usando a API [!DNL Flow Service]

>[!NOTE]
>
>A origem [!DNL Veeva CRM] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Veeva CRM] usando a [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisa saber para se conectar com êxito a [!DNL Veeva CRM] usando a API [!DNL Flow Service].

### Obter credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Veeva CRM], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL da sua instância [!DNL Veeva CRM]. |
| `username` | O valor do nome de usuário da sua conta [!DNL Veeva CRM]. |
| `password` | O valor da senha da sua conta [!DNL Veeva CRM]. |
| `securityToken` | O token de segurança da sua instância [!DNL Veeva CRM]. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Veeva CRM] é: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Para obter mais informações sobre esses valores, consulte este [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/api/#order-management-rest-api).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL Veeva CRM] como parte dos parâmetros da solicitação.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | O nome da sua conexão base [!DNL Veeva CRM]. Você pode usar esse nome para pesquisar sua conexão base [!DNL Veeva CRM]. |
| `description` | Uma descrição opcional para sua conexão base [!DNL Veeva CRM]. |
| `auth.specName` | O tipo de autenticação usado para a conexão. |
| `auth.params.environmentUrl` | O URL da sua instância [!DNL Veeva CRM]. |
| `auth.params.username` | O valor do nome de usuário da sua conta [!DNL Veeva CRM]. |
| `auth.params.password` | O valor da senha da sua conta [!DNL Veeva CRM]. |
| `auth.params.securityToken` | O token de segurança da sua instância [!DNL Veeva CRM]. |
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

Ao seguir este tutorial, você criou uma conexão base [!DNL Veeva CRM] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar sistemas CRM usando a API do Serviço de Fluxo](../../explore/crm.md).
