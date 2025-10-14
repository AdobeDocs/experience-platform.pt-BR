---
keywords: Experience Platform;página inicial;tópicos populares;IBM [!DNL IBM DB2];IBM;ibm [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: Criar uma Conexão Base do IBM [!DNL IBM DB2] Usando a API de Serviço de Fluxo
type: Tutorial
description: Saiba como conectar o IBM [!DNL IBM DB2] ao Adobe Experience Platform usando a API de Serviço de Fluxo.
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 5%

---

# Criar uma conexão de base [!DNL IBM DB2] do IBM usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL IBM DB2] do IBM está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL IBM DB2] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL IBM DB2] usando a API [!DNL Flow Service].

| Credencial | Descrição |
| ---------- | ----------- |
| `server` | O nome do servidor [!DNL IBM DB2]. Você pode especificar o número da porta após o nome do servidor delimitado por dois pontos. Por exemplo: servidor:porta. |
| `database` | O nome do banco de dados [!DNL IBM DB2]. |
| `username` | O nome de usuário usado para conectar ao banco de dados [!DNL IBM DB2]. |
| `password` | A senha da conta de usuário especificada para o nome de usuário. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID da especificação de conexão para [!DNL IBM DB2] é `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

Para obter mais informações sobre a introdução, consulte [este [!DNL IBM DB2] documento](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL IBM DB2] como parte dos parâmetros de solicitação.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Seguindo este tutorial, você criou uma conexão de base [!DNL IBM DB2] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)

