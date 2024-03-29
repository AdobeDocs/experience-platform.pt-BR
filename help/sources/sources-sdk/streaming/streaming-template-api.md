---
title: Modelo de autoatendimento de documentação para API do SDK de transmissão
description: Saiba como trazer dados de transmissão de uma origem para a Adobe Experience Platform usando a API do serviço de fluxo.
exl-id: a06384a2-cd99-456d-9f00-babcf3f7b7d9
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 2%

---

# Criar uma conexão de origem e um fluxo de dados para transmissão *SUA FONTE* dados usando o [!DNL Flow Service] API

*À medida que passa por esse modelo, substitua ou exclua todos os parágrafos em itálico (começando por este).*

*Comece atualizando os metadados (título e descrição) na parte superior da página. Ignore todas as instâncias do DNL nesta página. Essa é uma tag que ajuda nossos processos de tradução automática a traduzir corretamente a página para os vários idiomas compatíveis. Adicionaremos tags à sua documentação depois que você enviá-la.*

## Visão geral

*Forneça uma breve visão geral da sua empresa, incluindo o valor que ela oferece aos clientes. Inclua um link para a página inicial da documentação do produto para leitura adicional.*

>[!IMPORTANT]
>
>Esse conector de origem e a página de documentação são criados e mantidos pelo *SUA FONTE* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *Inserir link ou endereço de email no qual você pode ser contatado para obter atualizações*.

## Pré-requisitos

*Adicione informações nesta seção sobre qualquer coisa que os clientes precisem saber antes de começar a configurar o código-fonte na interface do usuário do Adobe Experience Platform. Isso pode se referir a:*

* *que precisam ser adicionados a uma lista de permissões*
* *requisitos para hash de email*
* *quaisquer detalhes específicos da conta da sua parte*
* *como obter uma chave de API para se conectar à sua plataforma*

### Coletar credenciais necessárias

Para se conectar *SUA FONTE* para Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| *credencial um* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione um exemplo da credencial de autenticação da sua origem aqui* |
| *credencial dois* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione um exemplo da credencial de autenticação da sua origem aqui* |
| *credencial três* | *Adicione uma breve descrição à credencial de autenticação da sua origem aqui* | *Adicione um exemplo da credencial de autenticação da sua origem aqui* |

Para obter mais informações sobre essas credenciais, consulte a *SUA FONTE* documentação de autenticação. *Adicione aqui o link para a documentação de autenticação da sua plataforma*.

### Integrar *SUA FONTE* com seu webhook

*O SDK de transmissão exige que a fonte seja compatível com webhooks para se comunicar com o Experience Platform. Nesta seção, você deve fornecer as etapas que os usuários terão que seguir para integrar YOURSOURCE a um webhook.*

## Conectar *SUA FONTE* para a Platform usando o [!DNL Flow Service] API

O tutorial a seguir guiará você pelas etapas para criar um *SUA FONTE* conexão de origem e criar um fluxo de dados para trazer *SUA FONTE* dados para a Platform usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Criar uma conexão de origem {#source-connection}

Crie uma conexão de origem fazendo uma solicitação POST para o [!DNL Flow Service] Ao fornecer a ID de especificação de conexão da origem, os detalhes como nome e descrição e o formato dos dados.

**Formato da API**

```https
POST /sourceConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de origem para *SUA FONTE*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
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
| `data.format` | O formato do *SUA FONTE* dados que você deseja assimilar. No momento, o único formato de dados compatível é `json`. |

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada. Essa ID é necessária em uma etapa posterior para criar um fluxo de dados.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Criar um esquema XDM de destino {#target-schema}

Para que os dados de origem sejam usados na Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. O esquema de destino é usado para criar um conjunto de dados da Platform no qual os dados de origem estão contidos.

Um schema XDM de destino pode ser criado executando uma solicitação POST para o [API do registro de esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um schema usando a API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados de destino pode ser criado executando uma solicitação POST para o [API do serviço de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fornecendo a ID do schema de destino na carga útil.

Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Criar uma conexão de destino {#target-connection}

Uma conexão de destino representa a conexão com o destino em que os dados assimilados devem ser armazenados. Para criar uma conexão de destino, você deve fornecer a ID de especificação de conexão fixa que corresponde ao data lake. Essa ID é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Agora você tem os identificadores exclusivos, um esquema de destino, um conjunto de dados de destino e a ID de especificação da conexão para o data lake. Usando esses identificadores, você pode criar uma conexão de destino usando o [!DNL Flow Service] API para especificar o conjunto de dados que conterá os dados de origem de entrada.

**Formato da API**

```https
POST /targetConnections
```

**Solicitação**

A solicitação a seguir cria uma conexão de destino para *SUA FONTE*:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| Propriedade | Descrição |
| -------- | ----------- |
| `name` | O nome da sua conexão de destino. Certifique-se de que o nome da conexão de destino seja descritivo, pois você pode usá-lo para pesquisar informações sobre a conexão de destino. |
| `description` | Um valor opcional que pode ser incluído para fornecer mais informações sobre a conexão de destino. |
| `connectionSpec.id` | A ID da especificação da conexão que corresponde ao data lake. Essa ID fixa é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | O formato do *SUA FONTE* que você deseja trazer para a Platform. |
| `params.dataSetId` | A ID do conjunto de dados de destino recuperada em uma etapa anterior. |


**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo da nova conexão de destino (`id`). Essa ID é necessária nas etapas posteriores.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
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
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `xdmSchema` | A ID do [esquema XDM do público-alvo](#target-schema) gerada em uma etapa anterior. |
| `mappings.destinationXdmPath` | O caminho XDM de destino para o qual o atributo de origem está sendo mapeado. |
| `mappings.sourceAttribute` | O atributo de origem que precisa ser mapeado para um caminho XDM de destino. |
| `mappings.identity` | Um valor booleano que designa se o conjunto de mapeamento será marcado para [!DNL Identity Service]. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes do mapeamento recém-criado, incluindo seu identificador exclusivo (`id`). Esse valor é necessário em uma etapa posterior para criar um fluxo de dados.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Criar um fluxo {#flow}

O último passo para trazer dados de *SUA FONTE* para a Platform é criar um fluxo de dados. Até agora, você tem os seguintes valores necessários preparados:

* [ID da conexão de origem](#source-connection)
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
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
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
| `flowSpec.id` | A ID de especificação de fluxo necessária para criar um fluxo de dados. Essa ID fixa é: `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | A versão correspondente da ID de especificação de fluxo. Esse valor é padronizado como `1.0`. |
| `sourceConnectionIds` | A variável [ID da conexão de origem](#source-connection) gerada em uma etapa anterior. |
| `targetConnectionIds` | A variável [ID da conexão de destino](#target-connection) gerada em uma etapa anterior. |
| `transformations` | Essa propriedade contém as várias transformações necessárias para serem aplicadas aos seus dados. Essa propriedade é necessária ao trazer dados não compatíveis com XDM para a Platform. |
| `transformations.name` | O nome atribuído à transformação. |
| `transformations.params.mappingId` | A variável [ID do mapeamento](#mapping) gerada em uma etapa anterior. |
| `transformations.params.mappingVersion` | A versão correspondente da ID de mapeamento. Esse valor é padronizado como `0`. |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado. Você pode usar essa ID para monitorar, atualizar ou excluir seu fluxo de dados.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Obter o URL do ponto de extremidade de streaming

Com o fluxo de dados criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Você usará esse URL de ponto de extremidade para inscrever sua origem em um webhook, permitindo que a origem se comunique com o Experience Platform.

Para recuperar o URL do ponto de extremidade de streaming, faça uma solicitação GET ao `/flows` e forneça a ID do seu fluxo de dados.

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna informações sobre o fluxo de dados, incluindo a URL do ponto de extremidade, marcado como `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## Apêndice

A seção a seguir fornece informações sobre as etapas que podem ser seguidas para monitorar, atualizar e excluir o fluxo de dados.

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre execuções de fluxo, status de conclusão e erros. Para obter exemplos completos de API, leia o guia em [monitoramento de fluxos de dados de origens usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Atualizar seu fluxo de dados

Atualize os detalhes do seu fluxo de dados, como nome e descrição, bem como o agendamento de execução e os conjuntos de mapeamento associados fazendo uma solicitação PATCH para o `/flows` endpoint de [!DNL Flow Service] ao fornecer a ID do fluxo de dados. Ao fazer uma solicitação PATCH, você deve fornecer os atributos exclusivos de seu fluxo de dados `etag` no `If-Match` cabeçalho. Para obter exemplos completos de API, leia o guia em [atualização de fluxos de dados de origens usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Atualizar sua conta

Atualize o nome, a descrição e as credenciais da sua conta de origem executando uma solicitação PATCH para a [!DNL Flow Service] ao fornecer a ID de conexão básica como um parâmetro de consulta. Ao fazer uma solicitação PATCH, você deve fornecer as informações exclusivas de sua conta de origem `etag` no `If-Match` cabeçalho. Para obter exemplos completos de API, leia o guia em [atualização da conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Excluir seu fluxo de dados

Exclua seu fluxo de dados executando uma solicitação DELETE para o [!DNL Flow Service] ao fornecer a ID do fluxo de dados que você deseja excluir como parte do parâmetro de consulta. Para obter exemplos completos de API, leia o guia em [exclusão de fluxos de dados usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Excluir sua conta

Exclua sua conta executando uma solicitação DELETE para o [!DNL Flow Service] ao fornecer a ID de conexão básica da conta que você deseja excluir. Para obter exemplos completos de API, leia o guia em [exclusão da conta de origem usando a API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
