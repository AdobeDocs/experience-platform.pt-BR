---
title: Crie uma conexão de origem e um fluxo de dados para Customer.io usando a API do Serviço de Fluxo
description: Saiba como conectar o Adobe Experience Platform ao Customer.io usando a API do Serviço de fluxo.
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 2%

---

# Criar uma conexão de origem e um fluxo de dados para [!DNL Customer.io] usando a API do Serviço de Fluxo

>[!NOTE]
>
>O [!DNL Customer.io] A fonte está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O tutorial a seguir o orienta pelas etapas para criar um [!DNL Customer.io] conexão de origem e fluxo de dados para trazer [[!DNL Customer.io]](https://customer.io/) dados de evento para a Adobe Experience Platform usando a variável [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Connect [!DNL Customer.io] para a plataforma usando a [!DNL Flow Service] API {#connect-platform-to-flow-api}

O seguinte descreve as etapas necessárias para criar uma conexão de origem e um fluxo de dados para trazer seus [!DNL Customer.io] dados de eventos para o Experience Platform.

### Criar uma conexão de origem {#source-connection}

Crie uma conexão de origem fazendo uma solicitação de POST para a [!DNL Flow Service] API, enquanto fornece a ID de especificação de conexão de sua fonte, detalhes como nome e descrição e o formato de seus dados.

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
| `connectionSpec.id` | A ID da especificação de conexão que corresponde à sua origem. |
| `data.format` | O formato do [!DNL Customer.io] dados que você deseja assimilar. Atualmente, o único formato de dados compatível é `json`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "133bb51f-f310-4b4a-b8b2-731aef1e223c",
    "etag": "\"af00a717-0000-0200-0000-63ef2cbd0000\""
}
```

### Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um schema de target deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O schema de destino é usado para criar um conjunto de dados da plataforma no qual os dados de origem estão contidos.

Um esquema XDM de destino pode ser criado executando-se uma solicitação de POST para a [API do Registro de Schema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial em [criação de um schema usando a API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação de POST para a [API do Serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do schema do target no payload.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial em [criação de um conjunto de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino onde os dados assimilados devem ser armazenados. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa que corresponde ao lago de dados. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos em um esquema de destino em um conjunto de dados de destino e a ID de especificação de conexão no lago de dados. Usando esses identificadores, você pode criar uma conexão de target usando o [!DNL Flow Service] API para especificar o conjunto de dados que conterá os dados de origem de entrada.

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
| `name` | O nome da conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação de conexão que corresponde ao lago de dados. Essa ID fixa é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | O formato do [!DNL Customer.io] dados que você deseja assimilar. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Essa ID é necessária em etapas posteriores.

```json
{
    "id": "da8b75ad-f6ee-4991-95df-291e62936e98",
    "etag": "\"70003dff-0000-0200-0000-63ef4a090000\""
}
```

### Criar um mapeamento {#mapping}

Para que os dados de origem sejam assimilados em um conjunto de dados de destino, eles devem primeiro ser mapeados para o schema de destino ao qual o conjunto de dados de destino adere. Isso é feito executando uma solicitação POST para [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) com mapeamentos de dados definidos na carga da solicitação.

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
| `outputSchema.schemaRef.id` | A ID do [esquema XDM de destino](#target-schema) gerado em uma etapa anterior. |
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

O último passo para trazer dados do [!DNL Customer.io] para Platform é criar um fluxo de dados. Por enquanto, você terá os seguintes valores obrigatórios preparados:

* [ID de conexão de origem](#source-connection)
* [ID de conexão do Target](#target-connection)
* [ID de mapeamento](#mapping)

Um fluxo de dados é responsável por agendar e coletar dados de uma fonte. Você pode criar um fluxo de dados executando uma solicitação de POST e, ao mesmo tempo, fornecendo os valores mencionados anteriormente dentro da carga útil.

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
| `name` | O nome do seu fluxo de dados. Certifique-se de que o nome do seu fluxo de dados seja descritivo, pois você pode usá-lo para pesquisar informações no seu fluxo de dados. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre o fluxo de dados. |
| `flowSpec.id` | A ID de especificação de fluxo necessária para criar um fluxo de dados. Essa ID fixa é: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | A versão correspondente da ID de especificação de fluxo. Esse valor assume como padrão `1.0`. |
| `sourceConnectionIds` | O [ID de conexão de origem](#source-connection) gerado em uma etapa anterior. |
| `targetConnectionIds` | O [target connection ID](#target-connection) gerado em uma etapa anterior. |
| `transformations` | Essa propriedade contém as várias transformações necessárias para serem aplicadas aos seus dados. Essa propriedade é necessária ao trazer dados não compatíveis com XDM para a plataforma. |
| `transformations.name` | O nome atribuído à transformação. |
| `transformations.params.mappingId` | O [ID de mapeamento](#mapping) gerado em uma etapa anterior. |
| `transformations.params.mappingVersion` | A versão correspondente da ID de mapeamento. Esse valor assume como padrão `0`. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado. Você pode usar essa ID para monitorar, atualizar ou excluir seu fluxo de dados.

```json
{
    "id": "4982698b-e6b3-48c2-8dcf-040e20121fd2",
    "etag": "\"4c012103-0000-0200-0000-63ef57db0000\""
}
```

### Obter o URL do terminal de transmissão {#get-streaming-endpoint-url}

Com o fluxo de dados criado, agora é possível recuperar o URL do terminal de transmissão. Você usará esse URL de ponto de extremidade para assinar sua fonte para um webhook, permitindo que sua fonte se comunique com o Experience Platform.

Para recuperar o URL do endpoint de transmissão, faça uma solicitação do GET para a variável `/flows` e forneça a ID do seu fluxo de dados.

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

Uma resposta bem-sucedida retorna informações sobre o fluxo de dados, incluindo o URL do terminal, marcado como `inletUrl`. Consulte a [Configurar Webhook](../../../ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint-url) para obter o valor necessário.

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

A seção a seguir fornece informações sobre as etapas possíveis para monitorar, atualizar e excluir seu fluxo de dados.

### Monitorar o fluxo de dados {#monitor-dataflow}

Depois que o fluxo de dados tiver sido criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos da API, leia o guia em [monitorar os fluxos de dados de fontes usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Atualizar o fluxo de dados {#update-dataflow}

Atualize os detalhes do seu fluxo de dados, como o nome e a descrição, bem como o cronograma de execução e os conjuntos de mapeamento associados, fazendo uma solicitação de PATCH para a `/flows` ponto final de [!DNL Flow Service] API, enquanto fornece a ID do fluxo de dados. Ao fazer uma solicitação do PATCH, você deve fornecer dados exclusivos de seu fluxo de dados `etag` no `If-Match` cabeçalho. Para obter exemplos completos da API, leia o guia em [atualização de fluxos de dados de fontes usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Atualize sua conta {#update-account}

Atualize o nome, a descrição e as credenciais da conta de origem executando uma solicitação de PATCH para a [!DNL Flow Service] API ao fornecer a ID de conexão básica como parâmetro de consulta. Ao fazer uma solicitação de PATCH, você deve fornecer a conta de origem exclusiva `etag` no `If-Match` cabeçalho. Para obter exemplos completos da API, leia o guia em [atualização da conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Excluir seu fluxo de dados {#delete-dataflow}

Exclua seu fluxo de dados executando uma solicitação de DELETE para [!DNL Flow Service] Ao fornecer a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos da API, leia o guia em [excluir seus fluxos de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Excluir sua conta {#delete-account}

Exclua sua conta executando uma solicitação de DELETE para [!DNL Flow Service] API ao fornecer a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos da API, leia o guia em [excluir sua conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).