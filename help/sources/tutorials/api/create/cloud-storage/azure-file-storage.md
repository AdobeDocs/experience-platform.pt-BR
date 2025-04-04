---
keywords: Experience Platform;página inicial;tópicos populares;Azure;Armazenamento de arquivos do Azure;Armazenamento de arquivos do Azure
solution: Experience Platform
title: Criar uma conexão da base de armazenamento de arquivos do Azure usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Armazenamento de arquivos do Azure ao Adobe Experience Platform usando a API do Serviço de fluxo.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 5%

---

# Criar uma conexão de base [!DNL Azure File Storage] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Azure File Storage] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Azure File Storage] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Azure File Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O ponto de extremidade da instância [!DNL Azure File Storag]e que você está acessando. |
| `userId` | O usuário com acesso suficiente ao ponto de extremidade [!DNL Azure File Storage]. |
| `password` | A senha da sua instância [!DNL Azure File Storage] |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Azure File Storage] é: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Para obter mais informações sobre a introdução, consulte [este documento do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Azure File Storage] como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.host` | O ponto de extremidade da instância [!DNL Azure File Storage] que você está acessando. |
| `auth.params.userId` | O usuário com acesso suficiente ao ponto de extremidade [!DNL Azure File Storage]. |
| `auth.params.password` | A chave de acesso [!DNL Azure File Storage]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Azure File Storage]: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão [!DNL Azure File Storage] usando a API [!DNL Flow Service] e obteve o valor de identificador exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a [explorar um armazenamento na nuvem de terceiros usando a API do Serviço de Fluxo](../../explore/cloud-storage.md).
