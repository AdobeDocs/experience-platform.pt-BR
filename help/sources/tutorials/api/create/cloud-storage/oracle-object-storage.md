---
keywords: Experience Platform, home, tópicos populares, Armazenamento de objetos do Oracle, Armazenamento de objetos do oracle
solution: Experience Platform
title: Criar uma conexão básica de armazenamento de objetos do Oracle usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform ao Oracle Object Storage usando a API do Serviço de Fluxo.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Crie um [!DNL Oracle Object Storage] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Oracle Object Storage] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Oracle Object Storage] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar a [!DNL Oracle Object Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUrl` | O [!DNL Oracle Object Storage] endpoint necessário para autenticação. O formato do ponto de extremidade é: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | O [!DNL Oracle Object Storage] a ID da chave de acesso é necessária para autenticação. |
| `secretKey` | O [!DNL Oracle Object Storage] senha necessária para autenticação. |
| `bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. O nome do bucket deve ter entre três e 63 caracteres, deve começar e terminar com uma letra ou um número e pode conter somente letras minúsculas, números ou hífens (`-`). O nome do bucket não pode ser formatado como um endereço IP. |
| `folderPath` | O caminho de pasta permitido é necessário se o usuário tiver acesso restrito. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Oracle Object Storage] é: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Para obter mais informações sobre como obter esses valores, consulte [Guia de autenticação do Armazenamento de objetos do Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Oracle Object Storage] credenciais de autenticação como parte dos parâmetros da solicitação.

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
| `auth.params.serviceUrl` | O [!DNL Oracle Object Storage] endpoint necessário para autenticação. |
| `auth.params.accessKey` | O [!DNL Oracle Object Storage] a ID da chave de acesso é necessária para autenticação. |
| `auth.params.secretKey` | O [!DNL Oracle Object Storage] senha necessária para autenticação. |
| `auth.params.bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. |
| `auth.params.folderPath` | O caminho de pasta permitido é necessário se o usuário tiver acesso restrito. |
| `connectionSpec.id` | O [!DNL Oracle Object Storage] ID de especificação de conexão: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão da conexão recém-criada. Essa ID é necessária para explorar seus dados de armazenamento em nuvem no próximo tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Oracle Object Storage] conexão usando o [!DNL Flow Service] e obtiveram sua ID de conexão exclusiva. Você pode usar essa ID de conexão para [explorar armazenamentos em nuvem usando a API do Serviço de fluxo](../../explore/cloud-storage.md).
