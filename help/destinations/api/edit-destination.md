---
solution: Experience Platform
title: Editar conexões de destino usando a API de Serviço de Fluxo
type: Tutorial
description: Saiba como editar vários componentes de uma conexão de destino usando a API de Serviço de Fluxo.
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---

# Editar conexões de destino usando a API de Serviço de Fluxo

Este tutorial aborda as etapas para editar vários componentes de uma conexão de destino. Saiba como atualizar credenciais de autenticação, exportar local e muito mais usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Atualmente, as operações de edição descritas neste tutorial são compatíveis apenas por meio da API do Serviço de fluxo.

## Introdução {#get-started}

Este tutorial requer uma ID de fluxo de dados válida. Se você não tiver uma ID de fluxo de dados válida, selecione o destino escolhido na [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas em [conectar-se ao destino](../ui/connect-destination.md) e [ativar dados](../ui/activation-overview.md) antes de tentar este tutorial.

>[!NOTE]
>
> Os termos *fluxo* e *fluxo de dados* são usados alternadamente neste tutorial. No contexto deste tutorial, eles têm o mesmo significado.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para atualizar com sucesso o fluxo de dados usando o [!DNL Flow Service] API.

### Lendo exemplos de chamadas de API {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários {#gather-values-for-required-headers}

Para fazer chamadas para APIs da plataforma, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos no Experience Platform, incluindo os pertencentes a [!DNL Flow Service], são isoladas em sandboxes virtuais específicas. Todas as solicitações para APIs da plataforma exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se a variável `x-sandbox-name` não for especificado, as solicitações serão resolvidas na variável `prod` sandbox.

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Pesquisar detalhes do fluxo de dados {#look-up-dataflow-details}

A primeira etapa na edição da conexão de destino é recuperar os detalhes do fluxo de dados usando a ID do fluxo. Você pode visualizar os detalhes atuais de um fluxo de dados existente fazendo uma solicitação do GET para a `/flows` endpoint .

>[!TIP]
>
>Você pode usar a interface do usuário do Experience Platform para obter a ID de fluxo de dados desejada de um destino. Ir para **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]**, selecione o fluxo de dados de destino desejado e encontre a ID de destino no painel direito. A ID de destino é o valor que você usará como ID de fluxo na próxima etapa.
>
> ![Obter a ID de destino usando a interface do usuário do Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O único `id` para o fluxo de dados de destino que você deseja recuperar. |

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

Uma resposta bem-sucedida retorna os detalhes atuais do fluxo de dados, incluindo a versão, o identificador exclusivo (`id`) e outras informações relevantes. Os mais relevantes para este tutorial são as IDs de conexão básica e de conexão de destino destacadas na resposta abaixo. Você usará essas IDs nas próximas seções para atualizar vários componentes da conexão de destino.

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

Os componentes de uma conexão de destino diferem de acordo com o destino. Por exemplo, para [!DNL Amazon S3] destinos , é possível atualizar o bucket e o caminho onde os arquivos são exportados. Para [!DNL Pinterest] destinos, você pode atualizar [!DNL Pinterest Advertiser ID] e [!DNL Google Customer Match] você pode atualizar seu [!DNL Pinterest Account ID].

Para atualizar os componentes de uma conexão de destino, execute uma solicitação de PATCH para o `/targetConnections/{TARGET_CONNECTION_ID}` endpoint ao fornecer a ID de conexão de destino, a versão e os novos valores que deseja usar. Lembre-se de que você obteve a ID de conexão do target na etapa anterior, ao inspecionar um fluxo de dados existente para o destino desejado.

>[!IMPORTANT]
>
>O `If-Match` é necessário usar o cabeçalho ao fazer uma solicitação de PATCH. O valor desse cabeçalho é a versão exclusiva da conexão de destino que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão do target e outras.
>
> Para obter a versão mais recente do valor da tag, execute uma solicitação de GET para o `/targetConnections/{TARGET_CONNECTION_ID}` endpoint, em que `{TARGET_CONNECTION_ID}` é a ID de conexão do target que você deseja atualizar.

Abaixo estão alguns exemplos de atualização de parâmetros na especificação da conexão do target para diferentes tipos de destinos. Mas a regra geral para atualizar parâmetros de qualquer destino é a seguinte:

Obtenha a ID do fluxo de dados da conexão > obtenha a ID da conexão de destino > PATCH da conexão de destino com valores atualizados para os parâmetros desejados.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão do público-alvo e uma Etag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID de conexão do target.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager e Google Ad Manager 360]

**Solicitação**

A solicitação a seguir atualiza os parâmetros de um [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) ou [[!DNL Google Ad Manager 360] destino](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) conexão para adicionar a nova [**[!UICONTROL Anexar ID de segmento ao nome do segmento]**](/help/release-notes/2023/april-2023.md#destinations) campo.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão do target e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID de conexão do target.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Solicitação**

A solicitação a seguir atualiza o `advertiserId` parâmetro de um [[!DNL Pinterest] conexão de destino](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão do target e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID de conexão do target.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Editar componentes de conexão básica (parâmetros de autenticação e outros componentes) {#patch-base-connection}

Os componentes de uma conexão base diferem de acordo com o destino. Por exemplo, para [!DNL Amazon S3] destinos , você pode atualizar a chave de acesso e a chave secreta para [!DNL Amazon S3] local.

Para atualizar os componentes de uma conexão base, execute uma solicitação de PATCH para o `/connections` endpoint ao fornecer a ID da conexão básica, a versão e os novos valores que deseja usar.

Lembre-se de que você obteve sua ID de conexão básica em uma etapa anterior, ao inspecionar um fluxo de dados existente para o destino desejado.

>[!IMPORTANT]
>
>O `If-Match` é necessário usar o cabeçalho ao fazer uma solicitação de PATCH. O valor desse cabeçalho é a versão exclusiva da conexão base que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão básica e outras.
>
> Para obter a versão mais recente do valor de Etag, execute uma solicitação de GET para o `/connections/{BASE_CONNECTION_ID}` endpoint, em que `{BASE_CONNECTION_ID}` é a ID de conexão básica que você deseja atualizar.

Abaixo estão alguns exemplos de atualização de parâmetros na especificação de conexão básica para diferentes tipos de destinos. Mas a regra geral para atualizar parâmetros de qualquer destino é a seguinte:

Obtenha a ID de fluxo de dados da conexão > obtenha a ID de conexão básica > PATCH a conexão base com valores atualizados para os parâmetros desejados.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão básica e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID de conexão básica.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Solicitação**

A solicitação a seguir atualiza os parâmetros de um [[!DNL Azure Blob] destino](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) conexão para atualizar a cadeia de conexão necessária para se conectar a uma instância do Azure Blob.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de conexão básica e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID de conexão básica.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Tratamento de erros da API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais da mensagem de erro da API de Experience Platform. Consulte [Códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma para obter mais informações sobre a interpretação das respostas dos erros.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você aprendeu a atualizar vários componentes de uma conexão de destino usando o [!DNL Flow Service] API. Para obter mais informações sobre destinos, consulte a [visão geral dos destinos](../home.md).
