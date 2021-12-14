---
keywords: Experience Platform, home, tópicos populares, Kinesis, cinesis, Amazon Kinesis, amazon kinesis
solution: Experience Platform
title: Criar uma conexão de origem do Amazon Kinesis usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como conectar o Adobe Experience Platform a uma fonte Amazon Kinesis usando a API do Serviço de Fluxo.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Crie um [!DNL Amazon Kinesis] conexão de origem usando a API do Serviço de Fluxo

Este tutorial o orienta pelas etapas para se conectar [!DNL Amazon Kinesis] (a seguir designado por &quot;[!DNL Kinesis]&quot;) para Experience Platform, usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam um único [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL Kinesis] para a plataforma usando a [!DNL Flow Service] API.

### Obter credenciais necessárias

Para [!DNL Flow Service] para se conectar com seu [!DNL Amazon Kinesis] , você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | A ID da chave de acesso é metade do par de chaves de acesso usado para autenticar seu [!DNL Kinesis] para a Platform. |
| `secretKey` | A chave de acesso secreta é a outra metade do par de chaves de acesso usado para autenticar seu [!DNL Kinesis] para a Platform. |
| `region` | A região de seu [!DNL Kinesis] conta. Consulte o guia sobre [adicionar endereços IP à sua lista de permissões](../../../../ip-address-allow-list.md) para obter mais informações sobre regiões. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de origem, incluindo especificações de autenticação relacionadas à criação das conexões base e de origem. O [!DNL Kinesis] a ID de especificação de conexão é: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Para obter mais informações sobre [!DNL Kinesis] acessar chaves e como gerá-las, consulte esta seção [[!DNL AWS] guia sobre gerenciamento de chaves de acesso para usuários do IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../../../landing/api-guide.md).

## Criar uma conexão base

A primeira etapa na criação de uma conexão de origem é autenticar seu [!DNL Kinesis] e gerar uma ID de conexão básica. Uma ID de conexão básica permite explorar e navegar pelos arquivos da fonte e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos e formatos de dados.

Para criar uma ID de conexão base, faça uma solicitação de POST para a variável `/connections` endpoint enquanto fornece seu [!DNL Kinesis] credenciais de autenticação como parte dos parâmetros da solicitação.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `auth.params.accessKeyId` | A ID da chave de acesso para sua [!DNL Kinesis] conta. |
| `auth.params.secretKey` | A chave de acesso secreta para sua [!DNL Kinesis] conta. |
| `auth.params.region` | A região de seu [!DNL Kinesis] conta. |
| `connectionSpec.id` | O [!DNL Kinesis] ID de especificação de conexão: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Criar uma conexão de origem {#source}

Uma conexão de origem cria e gerencia a conexão com a fonte externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e ID de conexão de origem necessárias para criar um fluxo de dados. Uma instância de conexão de origem é específica de um locatário e da Organização IMS.

Para criar uma conexão de origem, faça uma solicitação de POST para a variável `/sourceConnections` endpoint da variável [!DNL Flow Service] API.

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser fornecido para incluir mais informações sobre a conexão de origem. |
| `baseConnectionId` | A ID de conexão básica da [!DNL Kinesis] fonte gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL Kinesis]. Essa ID é: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | O formato do [!DNL Kinesis] dados que você deseja assimilar. Atualmente, o único formato de dados compatível é `json`. |
| `params.stream` | O nome do fluxo de dados do qual extrair registros. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados compatíveis incluem: `raw` e `xdm`. |
| `params.reset` | Esse parâmetro define como os dados serão lidos. Use `latest` para começar a ler a partir dos dados mais recentes, e use `earliest` para começar a ler a partir dos primeiros dados disponíveis no fluxo. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária no próximo tutorial para criar um fluxo de dados.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou um [!DNL Kinesis] conexão de origem usando o [!DNL Flow Service] API. Você pode usar essa ID de conexão de origem no próximo tutorial para [crie um fluxo de dados de transmissão usando o [!DNL Flow Service] API](../../collect/streaming.md).
