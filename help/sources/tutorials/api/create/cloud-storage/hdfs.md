---
keywords: Experience Platform, home, tópicos populares, Sistema de Arquivos Distribuído do Apache Hadoop, hadoop Apache, hdfs, HDFS
solution: Experience Platform
title: Criar uma conexão base do Apache HDFS usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar um sistema de arquivos distribuído do Apache Hadoop ao Adobe Experience Platform usando a API do Serviço de fluxo.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Crie um [!DNL Apache] Conexão base HDFS usando o [!DNL Flow Service] API

>[!NOTE]
>
>O conector HDFS do Apache está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Uma conexão base representa a conexão autenticada entre uma fonte e o Adobe Experience Platform.

Este tutorial o orienta pelas etapas para criar uma conexão básica para [!DNL Apache Hadoop Distributed File System] (a seguir designado por &quot;[!DNL HDFS]&quot;) usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL HDFS] usando o [!DNL Flow Service] API.

### Obter credenciais necessárias

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL define os parâmetros de autenticação necessários para a conexão com o [!DNL HDFS] anonimamente. Para obter mais informações sobre como obter esse valor, consulte [this [!DNL HDFS] documento](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. A ID de especificação de conexão para [!DNL AdWords] é: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

Uma conexão base retém informações entre a fonte e a Plataforma, incluindo as credenciais de autenticação da fonte, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL HDFS] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL HDFS]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `auth.params.url` | O URL que define os parâmetros de autenticação necessários para conexão com o [!DNL HDFS] anonimamente |
| `connectionSpec.id` | O [!DNL HDFS] ID de especificação de conexão: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL HDFS] conexão usando o [!DNL Flow Service] API e obtiveram o valor de ID exclusivo da conexão. Você pode usar essa ID no próximo tutorial enquanto aprende a usar [explorar um armazenamento em nuvem de terceiros usando a API do Serviço de Fluxo](../../explore/cloud-storage.md).
