---
keywords: Experience Platform, home, tópicos populares, Azure, Armazenamento de arquivos do Azure, Armazenamento de arquivos do Azure
solution: Experience Platform
title: Criar uma Conexão Base de Armazenamento de Arquivos do Azure usando a API do Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Armazenamento de Arquivos do Azure à Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Crie um [!DNL Azure File Storage] conexão básica usando o [!DNL Flow Service] API

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Azure File Storage] usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Azure File Storage] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para conectar-se com [!DNL Azure File Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O terminal da [!DNL Azure File Storag]Por exemplo, uma instância que você está acessando. |
| `userId` | O usuário com acesso suficiente ao [!DNL Azure File Storage] endpoint . |
| `password` | A senha de seu [!DNL Azure File Storage] instância |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL Azure File Storage] é: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Para obter mais informações sobre a introdução, consulte [este documento do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Azure File Storage] credenciais de autenticação como parte dos parâmetros da solicitação.

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
| `auth.params.host` | O terminal da [!DNL Azure File Storage] instância que você está acessando. |
| `auth.params.userId` | O usuário com acesso suficiente ao [!DNL Azure File Storage] endpoint . |
| `auth.params.password` | O [!DNL Azure File Storage] chave de acesso. |
| `connectionSpec.id` | O [!DNL Azure File Storage] ID de especificação de conexão: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Azure File Storage] conexão usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explorar um armazenamento em nuvem de terceiros usando a API do Serviço de Fluxo](../../explore/cloud-storage.md).
