---
title: Criar uma conexão Amazon Kinesis Source usando a API do serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform a uma origem Amazon Kinesis usando a API do Serviço de fluxo.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 4%

---

# Criar uma conexão de origem [!DNL Amazon Kinesis] usando a API de Serviço de Fluxo

>[!IMPORTANT]
>
>A origem [!DNL Amazon Kinesis] está disponível no catálogo de origens para usuários que compraram o Real-Time Customer Data Platform Ultimate.

Este tutorial guiará você pelas etapas para conectar o [!DNL Amazon Kinesis] (a seguir denominado &quot;[!DNL Kinesis]&quot;) ao Experience Platform, usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Kinesis] ao Experience Platform usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte à sua conta [!DNL Amazon Kinesis], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | A ID da chave de acesso é metade do par de chaves de acesso usado para autenticar sua conta do [!DNL Kinesis] no Experience Platform. |
| `secretKey` | A chave de acesso secreta é a outra metade do par de chaves de acesso usado para autenticar sua conta do [!DNL Kinesis] no Experience Platform. |
| `region` | A região da sua conta [!DNL Kinesis]. Consulte o manual sobre [adição de endereços IP ao seu incluo na lista de permissões](../../../../ip-address-allow-list.md) para obter mais informações sobre regiões. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão [!DNL Kinesis] é: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Para obter mais informações sobre [!DNL Kinesis] chaves de acesso e como gerá-las, consulte este [[!DNL AWS] guia sobre como gerenciar chaves de acesso para usuários do IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

A primeira etapa na criação de uma conexão de origem é autenticar sua origem [!DNL Kinesis] e gerar uma ID de conexão base. Uma ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar itens específicos que você deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Kinesis] como parte dos parâmetros de solicitação.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.accessKeyId` | A ID da chave de acesso da sua conta [!DNL Kinesis]. |
| `auth.params.secretKey` | A chave de acesso secreta da sua conta [!DNL Kinesis]. |
| `auth.params.region` | A região da sua conta [!DNL Kinesis]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária na próxima etapa para criar uma conexão de origem.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Criar uma conexão de origem {#source}

Uma conexão de origem cria e gerencia a conexão com a origem externa de onde os dados são assimilados. Uma conexão de origem consiste em informações como fonte de dados, formato de dados e a ID da conexão de origem necessária para criar um fluxo de dados. Uma instância de conexão de origem é específica para um locatário e uma organização.

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` da API [!DNL Flow Service].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `baseConnectionId` | A ID da conexão base da sua origem [!DNL Kinesis] que foi gerada na etapa anterior. |
| `connectionSpec.id` | A ID de especificação de conexão fixa para [!DNL Kinesis]. Esta ID é: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | O formato dos dados [!DNL Kinesis] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |
| `params.stream` | O nome do fluxo de dados do qual extrair registros. |
| `params.dataType` | Esse parâmetro define o tipo de dados que está sendo assimilado. Os tipos de dados suportados incluem: `raw` e `xdm`. |
| `params.reset` | Esse parâmetro define como os dados serão lidos. Use `latest` para começar a ler os dados mais recentes e use `earliest` para começar a ler os primeiros dados disponíveis no fluxo. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária no próximo tutorial para criar um fluxo de dados.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Depois de criar ou atualizar um fluxo de dados de transmissão, é necessária uma breve pausa de 5 minutos na assimilação de dados para evitar possíveis instâncias de perda ou perda de dados.

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de origem [!DNL Kinesis] usando a API [!DNL Flow Service]. Você pode usar esta ID de conexão de origem no próximo tutorial para [criar um fluxo de dados de streaming usando a [!DNL Flow Service] API](../../collect/streaming.md).
