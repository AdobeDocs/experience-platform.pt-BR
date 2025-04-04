---
keywords: Experience Platform;home;tópicos populares;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Criar uma conexão de base de armazenamento de objetos do Oracle usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Armazenamento de objetos da Oracle usando a API do Serviço de fluxo.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 4%

---

# Criar uma conexão de base [!DNL Oracle Object Storage] usando a API [!DNL Flow Service]

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Oracle Object Storage] usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Oracle Object Storage] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Oracle Object Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUrl` | O ponto de extremidade [!DNL Oracle Object Storage] necessário para autenticação. O formato do ponto de extremidade é: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | A ID da chave de acesso [!DNL Oracle Object Storage] é necessária para autenticação. |
| `secretKey` | A senha [!DNL Oracle Object Storage] é necessária para autenticação. |
| `bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. O nome do bucket deve ter entre três e 63 caracteres, deve começar e terminar com uma letra ou um número e pode conter apenas letras minúsculas, números ou hifens (`-`). O nome do bucket não pode ser formatado como um endereço IP. |
| `folderPath` | O caminho de pasta permitido é necessário caso o usuário tenha acesso restrito. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Oracle Object Storage] é: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Para obter mais informações sobre como obter esses valores, consulte o [guia de autenticação do Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Oracle Object Storage] como parte dos parâmetros de solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.serviceUrl` | O ponto de extremidade [!DNL Oracle Object Storage] necessário para autenticação. |
| `auth.params.accessKey` | A ID da chave de acesso [!DNL Oracle Object Storage] é necessária para autenticação. |
| `auth.params.secretKey` | A senha [!DNL Oracle Object Storage] é necessária para autenticação. |
| `auth.params.bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. |
| `auth.params.folderPath` | O caminho de pasta permitido é necessário caso o usuário tenha acesso restrito. |
| `connectionSpec.id` | A ID de especificação de conexão [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão da conexão recém-criada. Essa ID é necessária para explorar os dados de armazenamento na nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão [!DNL Oracle Object Storage] usando a API [!DNL Flow Service] e obteve sua ID de conexão exclusiva. Você pode usar esta ID de conexão para [explorar armazenamentos em nuvem usando a API de Serviço de Fluxo](../../explore/cloud-storage.md).
