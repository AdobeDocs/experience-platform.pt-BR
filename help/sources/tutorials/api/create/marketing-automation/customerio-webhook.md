---
title: Crie uma conexão de origem e um fluxo de dados para Customer.io usando a API do Serviço de fluxo
description: Saiba como conectar o Adobe Experience Platform ao Customer.io usando a API do Serviço de fluxo.
badge: Beta
exl-id: 1c84d818-428f-4097-9f6f-ef0cf1a04785
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 2%

---

# Crie uma conexão de origem e um fluxo de dados para [!DNL Customer.io] usando a API de Serviço de Fluxo

>[!NOTE]
>
>A origem [!DNL Customer.io] está na versão beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O tutorial a seguir guiará você pelas etapas para criar uma conexão de origem e um fluxo de dados do [!DNL Customer.io] para trazer dados do evento [[!DNL Customer.io]](https://customer.io/) para a Adobe Experience Platform usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Conectar o [!DNL Customer.io] ao Experience Platform usando a API [!DNL Flow Service] {#connect-platform-to-flow-api}

A seguir estão descritas as etapas que você precisa realizar para criar uma conexão de origem e um fluxo de dados para trazer seus dados de eventos do [!DNL Customer.io] para a Experience Platform.

### Criar uma conexão de origem {#source-connection}

Crie uma conexão de origem fazendo uma solicitação POST para a API [!DNL Flow Service], ao mesmo tempo em que fornece a ID de especificação da conexão da sua origem, detalhes como nome e descrição e o formato dos seus dados.

**Formato da API**

```https
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para [!DNL Customer.io]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Customer.io",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for customer.io",
      "connectionSpec": {
          "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sua conexão de origem. Certifique-se de que o nome da conexão de origem seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de origem. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de origem. |
| `connectionSpec.id` | A ID de especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato dos dados [!DNL Customer.io] que você deseja assimilar. Atualmente, o único formato de dados com suporte é `json`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
    "etag": "\"af00a717-0000-0200-0000-63ef2cbd0000\""
}
```

### Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados no Experience Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados do Experience Platform no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um esquema usando a API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=pt-BR#create).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), fornecendo a ID do esquema de destino na carga.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=pt-BR).

### Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino em que os dados assimilados devem ser armazenados. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa que corresponde ao data lake. Esta ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o data lake. Usando esses identificadores, você pode criar uma conexão de destino usando a API [!DNL Flow Service] para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de destino para [!DNL Customer.io]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Customer.io",
      "description": "Streaming Target Connection for Customer.io",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63ec807d3f5ce91bd2d06c65"
      }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da sua conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação da conexão que corresponde ao data lake. Esta ID fixa é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | O formato dos dados [!DNL Customer.io] que você deseja assimilar. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da nova conexão de destino. Essa ID é necessária nas etapas posteriores.

```json
{
    "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
    "etag": "\"70003dff-0000-0200-0000-63ef4a090000\""
}
```

### Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o esquema de destino ao qual o conjunto de dados de destino adere. Isso é feito executando uma solicitação POST para [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) com mapeamentos de dados definidos na carga da solicitação.

**Formato da API**

```http
POST /conversion/mappingSets
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.cio_id",
            "sourceAttribute": "data.identifiers.cio_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.email",
            "sourceAttribute": "data.identifiers.email",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.event_id0",
            "sourceAttribute": "event_id",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.metricx",
            "sourceAttribute": "metric",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.object_type1",
            "sourceAttribute": "object_type",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestampx",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `outputSchema.schemaRef.id` | A ID do [esquema XDM de destino](#target-schema) gerada em uma etapa anterior. |
| `mappings.sourceType` | O tipo de atributo de origem que está sendo mapeado. |
| `mappings.source` | O atributo de origem que precisa ser mapeado para um caminho XDM de destino. |
| `mappings.destination` | O caminho XDM de destino para o qual o atributo de origem está sendo mapeado. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
    "version": 0,
    "createdDate": 1676627988129,
    "modifiedDate": 1676627988129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Criar um fluxo {#flow}

A última etapa para trazer dados de [!DNL Customer.io] para a Experience Platform é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

* [ID de conexão do Source](#source-connection)
* [ID da conexão de destino](#target-connection)
* [ID de mapeamento](#mapping)

Um fluxo de dados é responsável por agendar e coletar dados de uma origem. Você pode criar um fluxo de dados executando uma solicitação POST enquanto fornece os valores mencionados anteriormente na carga.

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Customer.io",
      "description": "Streaming Dataflow for Customer.io",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "133bb51f-f310-4b4a-b8b2-731aef1e223c"
      ],
      "targetConnectionIds": [
          "da8b75ad-f6ee-4991-95df-291e62936e98"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome do fluxo de dados. Verifique se o nome do fluxo de dados é descritivo, pois você pode usá-lo para pesquisar informações sobre o fluxo de dados. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID de especificação de fluxo necessária para criar um fluxo de dados. Esta ID fixa é: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | A versão correspondente da ID de especificação de fluxo. O padrão deste valor é `1.0`. |
| `sourceConnectionIds` | A [ID da conexão de origem](#source-connection) gerada em uma etapa anterior. |
| `targetConnectionIds` | A [ID da conexão de destino](#target-connection) gerada em uma etapa anterior. |
| `transformations` | Essa propriedade contém as várias transformações necessárias para serem aplicadas aos seus dados. Essa propriedade é necessária ao trazer dados não compatíveis com XDM para a Experience Platform. |
| `transformations.name` | O nome atribuído à transformação. |
| `transformations.params.mappingId` | A [ID de mapeamento](#mapping) gerou em uma etapa anterior. |
| `transformations.params.mappingVersion` | A versão correspondente da ID de mapeamento. O padrão deste valor é `0`. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado. Você pode usar essa ID para monitorar, atualizar ou excluir seu fluxo de dados.

```json
{
    "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
    "etag": "\"4c012103-0000-0200-0000-63ef57db0000\""
}
```

### Obter o URL do ponto de extremidade de streaming {#get-streaming-endpoint-url}

Com o fluxo de dados criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Você usará essa URL de ponto de extremidade para inscrever sua origem em um webhook, permitindo que a origem se comunique com o Experience Platform.

Para recuperar a URL do ponto de extremidade de streaming, faça uma solicitação GET para o ponto de extremidade `/flows` e forneça a ID do fluxo de dados.

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna informações sobre seu fluxo de dados, incluindo a URL do ponto de extremidade, marcado como `inletUrl`. Consulte a página [Webhook de instalação](../../../ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint-url) para obter o valor necessário.

```json
{
    "items": [
        {
            "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "createdAt": 1676629979503,
            "updatedAt": 1676629985390,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Customer.io",
            "description": "Streaming Dataflow for Customer.io",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "etag": "\"4c01c003-0000-0200-0000-63ef57e10000\"",
            "sourceConnectionIds": [
                "133bb51f-f310-4b4a-b8b2-731aef1e223c"
            ],
            "targetConnectionIds": [
                "da8b75ad-f6ee-4991-95df-291e62936e98"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
                        "connectionSpec": {
                            "id": "96479064-7b8a-4d69-b9ed-21c5683837ea",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e75dcb5247eb65e7385df30270192e80b145566f52ed74d570505bd2e82463f3"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "59c0e53a2dc84f7791ecc1b3d6e51d5e",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4982698b-e6b3-48c2-8dcf-040e20121fd2",
            "providerRefId": "c4726e6f-64b4-4b3b-97e3-f128ace0cc74",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            }
        }
    ]
}
```

## Apêndice {#appendix}

A seção a seguir fornece informações sobre as etapas que podem ser seguidas para monitorar, atualizar e excluir o fluxo de dados.

### Monitorar seu fluxo de dados {#monitor-dataflow}

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos de API, leia o guia em [monitorando seus fluxos de dados de fontes usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html?lang=pt-BR).

### Atualizar seu fluxo de dados {#update-dataflow}

Atualize os detalhes do seu fluxo de dados, como seu nome e descrição, bem como seu agendamento de execução e conjuntos de mapeamento associados fazendo uma solicitação PATCH para o ponto de extremidade `/flows` da API [!DNL Flow Service], ao mesmo tempo em que fornece a ID do seu fluxo de dados. Ao fazer uma solicitação PATCH, você deve fornecer o `etag` exclusivo do fluxo de dados no cabeçalho `If-Match`. Para obter exemplos completos de API, leia o guia em [atualizando fluxos de dados de fontes usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html?lang=pt-BR)

### Atualizar sua conta {#update-account}

Atualize o nome, a descrição e as credenciais da conta de origem executando uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID da conexão base como um parâmetro de consulta. Ao fazer uma solicitação PATCH, você deve fornecer o `etag` exclusivo da sua conta de origem no cabeçalho `If-Match`. Para obter exemplos completos de API, leia o guia em [atualizando a conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html?lang=pt-BR).

### Excluir seu fluxo de dados {#delete-dataflow}

Exclua seu fluxo de dados executando uma solicitação DELETE para a API [!DNL Flow Service] enquanto fornece a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos de API, leia o guia em [excluindo seus fluxos de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html?lang=pt-BR).

### Excluir sua conta {#delete-account}

Exclua sua conta executando uma solicitação DELETE para a API [!DNL Flow Service] enquanto fornece a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos de API, leia o guia em [excluindo sua conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html?lang=pt-BR).
