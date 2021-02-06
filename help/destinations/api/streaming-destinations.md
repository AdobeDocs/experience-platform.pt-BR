---
keywords: Experience Platform;lar;tópicos populares; Tutoriais de API; API de destinos de transmissão contínua; Plataforma
solution: Experience Platform
title: Conecte-se a destinos de transmissão e ative dados usando chamadas de API
description: Este documento cobre a criação de destinos de streaming usando a API do Adobe Experience Platform
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '2021'
ht-degree: 1%

---


# Conecte-se a destinos de streaming e ative dados usando chamadas de API no Adobe Experience Platform

>[!NOTE]
>
>Os destinos [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs] na Plataforma estão atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

Este tutorial demonstra como usar chamadas de API para se conectar aos dados do Adobe Experience Platform, criar uma conexão com um destino de armazenamento de nuvem de fluxo ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) ou [Hubs de Evento do Azure](../catalog/cloud-storage/azure-event-hubs.md)), criar um fluxo de dados para o seu novo destino criado e ativar os dados para o seu novo destino criado.

Este tutorial usa o destino [!DNL Amazon Kinesis] em todos os exemplos, mas as etapas são idênticas para [!DNL Azure Event Hubs].

![Visão geral - as etapas para criar um destino de streaming e ativar segmentos](../assets/api/streaming-destination/overview.png)

Se você preferir usar a interface do usuário no Platform para se conectar a um destino e ativar dados, consulte os tutoriais [Conectar um destino](../ui/connect-destination.md) e [Ativar perfis e segmentos em um destino](../ui/activate-destinations.md).

## Comece já

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [[!DNL Catalog Service]](../../catalog/home.md):  [!DNL Catalog] é o sistema de registro para localização e linhagem de dados dentro do Experience Platform.
* [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para ativar os dados para os destinos de streaming na Plataforma.

### Reunir credenciais obrigatórias

Para concluir as etapas neste tutorial, você deve ter as seguintes credenciais prontas, dependendo do tipo de destinos aos quais você está conectando e ativando segmentos.

* Para conexões [!DNL Amazon Kinesis]: `accessKeyId`, `secretKey`, `region` ou `connectionUrl`
* Para conexões [!DNL Azure Event Hubs]: `sasKeyName`, `sasKey`, `namespace`

### Lendo chamadas de exemplo de API {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Colete valores para cabeçalhos obrigatórios e opcionais {#gather-values}

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Os recursos no Experience Platform podem ser isolados para caixas de proteção virtuais específicas. Em solicitações para APIs de plataforma, você pode especificar o nome e a ID da caixa de proteção em que a operação ocorrerá. Esses são parâmetros opcionais.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Experience Platform, consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

### Documentação do Swagger {#swagger-docs}

Você pode encontrar a documentação de referência para todas as chamadas de API neste tutorial no Swagger. Consulte a documentação da API do Serviço de Fluxo em Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). [ Recomendamos que você use este tutorial e a página de documentação do Swagger em paralelo.

## Obtenha a lista de destinos de streaming disponíveis {#get-the-list-of-available-streaming-destinations}

![Etapas de destino visão geral etapa 1](../assets/api/streaming-destination/step1.png)

Como primeira etapa, você deve decidir para qual destino de fluxo deve ativar os dados. Para começar, execute uma chamada para solicitar uma lista de destinos disponíveis aos quais você possa se conectar e ativar segmentos. Execute a seguinte solicitação de GET ao terminal `connectionSpecs` para retornar uma lista de destinos disponíveis:

**Formato da API**

```http
GET /connectionSpecs
```

**Solicitação**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Resposta**

Uma resposta bem-sucedida contém uma lista de destinos disponíveis e seus identificadores exclusivos (`id`). Armazene o valor do destino que você planeja usar, pois ele será necessário em outras etapas. Por exemplo, se você deseja conectar e fornecer segmentos a [!DNL Amazon Kinesis] ou [!DNL Azure Event Hubs], procure o seguinte trecho na resposta:

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Conecte-se aos seus dados de Experience Platform {#connect-to-your-experience-platform-data}

![Etapas de destino visão geral etapa 2](../assets/api/streaming-destination/step2.png)

Em seguida, você deve se conectar aos dados do Experience Platform para poder exportar os dados do perfil e ativá-los no destino preferencial. Este conjunto consiste em duas etapas descritas abaixo.

1. Primeiro, você deve executar uma chamada para autorizar o acesso aos seus dados no Experience Platform, configurando uma conexão básica.
2. Em seguida, usando a ID de conexão básica, você fará outra chamada na qual você cria uma conexão de origem, que estabelece a conexão com seus dados de Experience Platform.


### Autorizar acesso aos seus dados no Experience Platform

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: Use a ID de especificação de conexão para o serviço de Perfil unificado -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Resposta**

Uma resposta bem-sucedida contém o identificador exclusivo da conexão base (`id`). Armazene esse valor conforme necessário na próxima etapa para criar a conexão de origem.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Conecte-se aos seus dados de Experience Platform {#connect-to-platform-data}

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Use a ID obtida na etapa anterior.
* `{CONNECTION_SPEC_ID}`: Use a ID de especificação de conexão para o serviço de Perfil unificado -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) para a conexão de origem recém-criada ao Serviço de Perfil Unificado. Isso confirma que você se conectou com êxito aos dados de Experience Platform. Armazene esse valor conforme necessário em uma etapa posterior.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Conectar-se ao destino de streaming {#connect-to-streaming-destination}

![Etapas de destino visão geral etapa 3](../assets/api/streaming-destination/step3.png)

Nesta etapa, você está configurando uma conexão com o destino de streaming desejado. Este conjunto consiste em duas etapas descritas abaixo.

1. Primeiro, você deve executar uma chamada para autorizar o acesso ao destino de streaming, configurando uma conexão básica.
2. Em seguida, usando a ID de conexão básica, você fará outra chamada na qual criará uma conexão de público alvo, que especifica o local em sua conta de armazenamento onde os dados exportados serão entregues, bem como o formato dos dados que serão exportados.

### Autorizar acesso ao destino de streaming

**Formato da API**

```http
POST /connections
```

**Solicitação**

>[!IMPORTANT]
>
>O exemplo abaixo inclui comentários de código com prefixo `//`. Esses comentários destacam onde valores diferentes devem ser usados para destinos de streaming diferentes. Remova os comentários antes de usar o trecho.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Use a ID de especificação de conexão obtida na etapa  [Obtenha a lista dos destinos](#get-the-list-of-available-destinations) disponíveis.
* `{AUTHENTICATION_CREDENTIALS}`: preencha o nome do seu destino de streaming:  `Aws Kinesis authentication credentials` ou  `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`:  *Para  [!DNL Amazon Kinesis] conexões.* Sua ID de acesso para a localização do armazenamento Amazon Kinesis.
* `{SECRET_KEY}`:  *Para  [!DNL Amazon Kinesis] conexões.* Sua chave secreta para a localização do armazenamento Amazon Kinesis.
* `{REGION}`:  *Para  [!DNL Amazon Kinesis] conexões.* A região em sua  [!DNL Amazon Kinesis] conta na qual a Plataforma fará o stream de seus dados.
* `{SAS_KEY_NAME}`:  *Para  [!DNL Azure Event Hubs] conexões.* Preencha o nome da chave SAS. Saiba mais sobre como autenticar em [!DNL Azure Event Hubs] com chaves SAS na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`:  *Para  [!DNL Azure Event Hubs] conexões.* Preencha sua chave SAS. Saiba mais sobre como autenticar em [!DNL Azure Event Hubs] com chaves SAS na [documentação da Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`:  *Para  [!DNL Azure Event Hubs] conexões.* Preencha a  [!DNL Azure Event Hubs] namespace onde a Plataforma fará o stream dos seus dados. Para obter mais informações, consulte [Criar uma namespace de Hubs de Evento](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) na documentação [!DNL Microsoft].

**Resposta**

Uma resposta bem-sucedida contém o identificador exclusivo da conexão base (`id`). Armazene esse valor conforme necessário na próxima etapa para criar uma conexão de público alvo.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Especificar a localização do armazenamento e o formato dos dados

**Formato da API**

```http
POST /targetConnections
```

**Solicitação**

>[!IMPORTANT]
>
>O exemplo abaixo inclui comentários de código com prefixo `//`. Esses comentários destacam onde valores diferentes devem ser usados para destinos de streaming diferentes. Remova os comentários antes de usar o trecho.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Use a ID de conexão básica obtida na etapa acima.
* `{CONNECTION_SPEC_ID}`: Use as especificações de conexão obtidas na etapa  [Obtenha a lista dos destinos](#get-the-list-of-available-destinations) disponíveis.
* `{NAME_OF_DATA_STREAM}`:  *Para  [!DNL Amazon Kinesis] conexões.* Forneça o nome do seu fluxo de dados existente em sua  [!DNL Amazon Kinesis] conta. A plataforma exportará dados para esse fluxo.
* `{REGION}`:  *Para  [!DNL Amazon Kinesis] conexões.* A região na sua conta Amazon Kinesis onde a Plataforma fará o stream dos seus dados.
* `{EVENT_HUB_NAME}`:  *Para  [!DNL Azure Event Hubs] conexões.* Preencha o  [!DNL Azure Event Hub] nome onde a Plataforma fará o stream dos seus dados. Para obter mais informações, consulte [Criar um hub de eventos](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) na documentação [!DNL Microsoft].

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) para a conexão de público alvo recém-criada para seu destino de streaming. Armazene esse valor conforme necessário em etapas posteriores.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Criar um fluxo de dados

![Etapas de destino visão geral etapa 4](../assets/api/streaming-destination/step4.png)

Usando as IDs obtidas nas etapas anteriores, agora é possível criar um fluxo de dados entre seus dados de Experience Platform e o destino para o qual você ativará os dados. Pense nessa etapa como construindo o pipeline, através do qual os dados fluirão posteriormente, entre o Experience Platform e o destino desejado.

Para criar um fluxo de dados, execute uma solicitação de POST, como mostrado abaixo, enquanto fornece os valores mencionados abaixo dentro da carga.

Execute a seguinte solicitação de POST para criar um fluxo de dados.

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: A ID de especificação de fluxo para destinos baseados em perfis é  `71471eba-b620-49e4-90fd-23f1fa0174d8`. Use esse valor na chamada.
* `{SOURCE_CONNECTION_ID}`: Use a ID de conexão de origem obtida na etapa  [Conecte-se ao seu Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Use a ID de conexão do público alvo obtida na etapa  [Conectar ao destino](#connect-to-streaming-destination) de streaming.

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado e um `etag`. Anote os dois valores. como você os fará na próxima etapa, para ativar segmentos.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Ativar dados para o novo destino {#activate-data}

![Etapas de destino visão geral etapa 5](../assets/api/streaming-destination/step5.png)

Depois de criar todas as conexões e o fluxo de dados, agora você pode ativar os dados do perfil na plataforma de streaming. Nessa etapa, você seleciona quais segmentos e quais atributos de perfil está enviando para o destino e pode agendar e enviar dados para o destino.

Para ativar segmentos no seu novo destino, é necessário executar uma operação JSON PATCH, semelhante ao exemplo abaixo. Você pode ativar vários segmentos e atributos de perfil em uma chamada. Para saber mais sobre o JSON PATCH, consulte a especificação [RFC](https://tools.ietf.org/html/rfc6902).

**Formato da API**

```http
PATCH /flows
```

**Solicitação**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

* `{DATAFLOW_ID}`: Use o fluxo de dados obtido na etapa anterior.
* `{ETAG}`: Use a tag obtida na etapa anterior.
* `{SEGMENT_ID}`: Forneça a ID do segmento que deseja exportar para esse destino. Para recuperar as IDs de segmento dos segmentos que você deseja ativar, vá para **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, selecione **[!UICONTROL API do Serviço de Segmentação]** no menu de navegação esquerdo e procure a operação `GET /segment/definitions` em **[!UICONTROL Definições de Segmento]**.
* `{PROFILE_ATTRIBUTE}`: Por exemplo,  `personalEmail.address` ou  `person.lastName`

**Resposta**

Procure uma resposta 202 OK. Nenhum corpo de resposta é retornado. Para validar se a solicitação estava correta, consulte a próxima etapa, Validar o fluxo de dados.

## Validar o fluxo de dados

![Etapas de destino visão geral etapa 6](../assets/api/streaming-destination/step6.png)

Como etapa final do tutorial, você deve validar se os segmentos e os atributos do perfil foram corretamente mapeados para o fluxo de dados.

Para validar isso, execute a seguinte solicitação de GET:

**Formato da API**

```http
GET /flows
```

**Solicitação**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Use o fluxo de dados da etapa anterior.
* `{ETAG}`: Use a tag da etapa anterior.

**Resposta**

A resposta retornada deve incluir no parâmetro `transformations` os segmentos e atributos de perfil enviados na etapa anterior. Um exemplo de parâmetro `transformations` na resposta pode ser parecido com o seguinte:

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**Dados exportados**

>[!IMPORTANT]
>
> Além dos atributos do perfil e dos segmentos na etapa [Ativar dados para seu novo destino](#activate-data), os dados exportados em [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] também incluirão informações sobre o mapa de identidade. Isso representa as identidades dos perfis exportados (por exemplo, [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), ID móvel, ID do Google, endereço de email etc.). Veja um exemplo abaixo.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Uso de coleções do Postman para conectar-se a destinos de streaming {#collections}

Para conectar-se aos destinos de streaming descritos neste tutorial de uma forma mais simplificada, você pode usar [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] é uma ferramenta que você pode usar para fazer chamadas de API e gerenciar bibliotecas de chamadas e ambientes predefinidos.

Para este tutorial específico, as seguintes coleções [!DNL Postman] foram anexadas:

* [!DNL AWS Kinesis] [!DNL Postman] coleção
* [!DNL Azure Event Hubs] [!DNL Postman] coleção

Clique [aqui](../assets/api/streaming-destination/DestinationPostmanCollection.zip) para baixar o arquivo de coleções.

Cada coleção inclui as solicitações e variáveis de ambiente necessárias, para [!DNL AWS Kinesis] e [!DNL Azure Event Hub], respectivamente.

### Como usar as coleções do Postman

Para se conectar com êxito aos destinos usando as coleções [!DNL Postman] anexadas, siga estas etapas:

* Baixe e instale [!DNL Postman];
* [Descarregue e ](../assets/api/streaming-destination/DestinationPostmanCollection.zip) descompacte as coleções anexadas;
* Importe as coleções de suas pastas correspondentes para o Postman;
* Preencha as variáveis do ambiente de acordo com as instruções deste artigo;
* Execute as solicitações [!DNL API] do Postman, com base nas instruções neste artigo.

## Próximas etapas

Ao seguir este tutorial, você conectou a Plataforma a um dos destinos de streaming preferidos e configurou um fluxo de dados para o respectivo destino. Os dados de saída agora podem ser usados no destino para análises de clientes ou quaisquer outras operações de dados que você desejar executar. Consulte as seguintes páginas para obter mais detalhes:

* [Visão geral dos destinos](../home.md)
* [Visão geral do catálogo de destinos](../catalog/overview.md)
