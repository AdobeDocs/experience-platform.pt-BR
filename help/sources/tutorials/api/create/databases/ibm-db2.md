---
keywords: Experience Platform, home, tópicos populares, IBM [!DNL IBM DB2];IBM;ibm [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: Criar uma conexão base IBM [!DNL IBM DB2] usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar a IBM [!DNL IBM DB2] à Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 2%

---

# Crie uma conexão base IBM [!DNL IBM DB2] usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector IBM [!DNL IBM DB2] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL IBM DB2] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md):  [!DNL Experience Platform] O permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito a [!DNL IBM DB2] usando a API [!DNL Flow Service].

| Credencial | Descrição |
| ---------- | ----------- |
| `server` | O nome do servidor [!DNL IBM DB2]. Você pode especificar o número da porta seguindo o nome do servidor delimitado por dois pontos. Por exemplo: server:port. |
| `database` | O nome do banco de dados [!DNL IBM DB2]. |
| `username` | O nome de usuário usado para se conectar ao banco de dados [!DNL IBM DB2]. |
| `password` | A senha da conta de usuário especificada para o nome de usuário. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL IBM DB2] é `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

Para obter mais informações sobre a introdução, consulte [this [!DNL IBM DB2] document](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia sobre como [começar a usar APIs da plataforma](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST ao endpoint `/connections`, fornecendo as credenciais de autenticação [!DNL IBM DB2] como parte dos parâmetros da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL IBM DB2]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua conta [!DNL IBM DB2]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL IBM DB2]: `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão IBM [!DNL IBM DB2] usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial à medida que aprende a [explorar bancos de dados usando a API do Serviço de Fluxo](../../explore/database-nosql.md).
