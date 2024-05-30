---
solution: Experience Platform
title: Editar conexões de destino usando a API do Serviço de fluxo
type: Tutorial
description: Saiba como editar vários componentes de uma conexão de destino usando a API de serviço de fluxo.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 5%

---

# Editar conexões de destino usando a API do Serviço de fluxo

Este tutorial aborda as etapas para editar vários componentes de uma conexão de destino. Saiba como atualizar credenciais de autenticação, exportar local e muito mais usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> No momento, as operações de edição descritas neste tutorial só são permitidas por meio da API de serviço de fluxo.

## Introdução {#get-started}

Este tutorial requer que você tenha uma ID de fluxo de dados válida. Se você não tiver uma ID de fluxo de dados válida, selecione o destino escolhido na [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas em [conectar ao destino](../ui/connect-destination.md) e [ativar dados](../ui/activation-overview.md) antes de tentar este tutorial.

>[!NOTE]
>
> Os termos *fluxo* e *fluxo de dados* são usados alternadamente neste tutorial. No contexto deste tutorial, eles têm o mesmo significado.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem as informações adicionais que você precisará saber para atualizar seu fluxo de dados com êxito usando o [!DNL Flow Service] API.

### Leitura de chamadas de API de amostra {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

### Coletar valores para cabeçalhos necessários {#gather-values-for-required-headers}

Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos no Experience Platform, incluindo os que pertencem a [!DNL Flow Service], são isolados em sandboxes virtuais específicas. Todas as solicitações para APIs da Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se a variável `x-sandbox-name` cabeçalho não for especificado, as solicitações serão resolvidas no `prod` sandbox.

Todas as solicitações que contêm uma carga (`POST`, `PUT`, `PATCH`) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Pesquisar detalhes do fluxo de dados {#look-up-dataflow-details}

A primeira etapa na edição da conexão de destino é recuperar os detalhes do fluxo de dados usando a ID do fluxo. Você pode exibir os detalhes atuais de um fluxo de dados existente fazendo uma solicitação GET ao `/flows` terminal.

>[!TIP]
>
>Você pode usar a interface do usuário do Experience Platform para obter a ID de fluxo de dados desejada de um destino. Ir para **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]**, selecione o fluxo de dados de destino desejado e localize a ID de destino no painel direito. A ID de destino é o valor que você usará como ID de fluxo na próxima etapa.
>
> ![Obter ID de destino usando a interface do Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O único `id` para o fluxo de dados de destino que deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera informações relacionadas à ID do fluxo.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes atuais do fluxo de dados, incluindo a versão, o identificador exclusivo (`id`e outras informações relevantes. Os mais relevantes para este tutorial são a conexão de destino e as IDs de conexão de base destacadas na resposta abaixo. Você usará essas IDs nas próximas seções para atualizar vários componentes da conexão de destino.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Editar componentes de conexão de destino (local de armazenamento e outros componentes) {#patch-target-connection}

Os componentes de uma conexão de destino diferem de acordo com o destino. Por exemplo, para [!DNL Amazon S3] destinos, é possível atualizar o compartimento e o caminho para onde os arquivos são exportados. Para [!DNL Pinterest] destinos, você poderá atualizar seus [!DNL Pinterest Advertiser ID] e para [!DNL Google Customer Match] você pode atualizar seu [!DNL Pinterest Account ID].

Para atualizar componentes de uma conexão de destino, execute uma `PATCH` solicitação à `/targetConnections/{TARGET_CONNECTION_ID}` ao fornecer a ID da conexão de destino, a versão e os novos valores que deseja usar. Lembre-se de que você obteve a ID de conexão de destino na etapa anterior, ao inspecionar um fluxo de dados existente para o destino desejado.

>[!IMPORTANT]
>
>A variável `If-Match` o cabeçalho é necessário ao criar um `PATCH` solicitação. O valor desse cabeçalho é a versão exclusiva da conexão de destino que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão de destino e outras.
>
> Para obter a versão mais recente do valor da tag, execute uma solicitação GET para o `/targetConnections/{TARGET_CONNECTION_ID}` endpoint, onde `{TARGET_CONNECTION_ID}` é a ID de conexão de destino que você deseja atualizar.
>
> Certifique-se de vincular o valor do `If-Match` cabeçalho entre aspas duplas, como nos exemplos abaixo, ao criar `PATCH` solicitações.

Abaixo estão alguns exemplos de atualização de parâmetros na especificação de conexão de destino para diferentes tipos de destinos. Mas a regra geral para atualizar parâmetros para qualquer destino é a seguinte:

Obter a ID do fluxo de dados da conexão > obter a ID da conexão de destino > `PATCH` a conexão de destino com valores atualizados para os parâmetros desejados.

>[!BEGINSHADEBOX]

**Formato da API**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitação**

A solicitação a seguir atualiza o `bucketName` e `path` parâmetros de um [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) conexão de destino.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`, e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de destino e uma Etag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para o [!DNL Flow Service] ao fornecer a ID de conexão de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager e Google Ad Manager 360]

**Solicitação**

A solicitação a seguir atualiza os parâmetros de um [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) ou [[!DNL Google Ad Manager 360] destino](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) conexão para adicionar o novo [**[!UICONTROL Anexar ID de público-alvo ao nome do público-alvo]**](/help/release-notes/2023/april-2023.md#destinations) campo.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`, e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de destino e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para o [!DNL Flow Service] ao fornecer a ID de conexão de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Solicitação**

A solicitação a seguir atualiza o `advertiserId` parâmetro de a [[!DNL Pinterest] conexão de destino](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`, e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão de destino e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para o [!DNL Flow Service] ao fornecer a ID de conexão de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Editar componentes de conexão base (parâmetros de autenticação e outros componentes) {#patch-base-connection}

Edite a conexão básica quando quiser atualizar as credenciais de um destino. Os componentes de uma conexão base diferem por destino. Por exemplo, para [!DNL Amazon S3] destinos, você poderá atualizar a chave de acesso e a chave secreta para o [!DNL Amazon S3] localização.

Para atualizar componentes de uma conexão básica, execute uma `PATCH` solicitação à `/connections` ao fornecer a ID de conexão básica, a versão e os novos valores que deseja usar.

Lembre-se de que você recebeu a ID de conexão básica em um [etapa anterior](#look-up-dataflow-details), quando você inspecionou um fluxo de dados existente para o destino desejado referente ao parâmetro `baseConnection`.

>[!IMPORTANT]
>
>A variável `If-Match` o cabeçalho é necessário ao criar um `PATCH` solicitação. O valor desse cabeçalho é a versão exclusiva da conexão base que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão de base e outras.
>
> Para obter a versão mais recente do valor Etag, execute uma solicitação GET para o `/connections/{BASE_CONNECTION_ID}` endpoint, onde `{BASE_CONNECTION_ID}` é a ID de conexão básica que você deseja atualizar.
>
> Certifique-se de vincular o valor do `If-Match` cabeçalho entre aspas duplas, como nos exemplos abaixo, ao criar `PATCH` solicitações.

Abaixo estão alguns exemplos de atualização de parâmetros na especificação de conexão de base para diferentes tipos de destinos. Mas a regra geral para atualizar parâmetros para qualquer destino é a seguinte:

Obter a ID do fluxo de dados da conexão > obter a ID da conexão base > `PATCH` a conexão básica com os valores atualizados para os parâmetros desejados.

>[!BEGINSHADEBOX]

**Formato da API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitação**

A solicitação a seguir atualiza o `accessId` e `secretKey` parâmetros de um [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) conexão de destino.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`, e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão básica e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para o [!DNL Flow Service] ao fornecer a ID de conexão básica.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Solicitação**

A solicitação a seguir atualiza os parâmetros de um [[!DNL Azure Blob] destino](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) conexão para atualizar a cadeia de conexão necessária para se conectar a uma instância do Blob do Azure.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`, e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão básica e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para o [!DNL Flow Service] ao fornecer a ID de conexão básica.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Manipulação de erros de API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform para obter mais informações sobre como interpretar respostas de erro.

## Próximas etapas {#next-steps}

Seguindo este tutorial, você aprendeu a atualizar vários componentes de uma conexão de destino usando o [!DNL Flow Service] API. Para obter mais informações sobre destinos, consulte a [visão geral dos destinos](../home.md).
