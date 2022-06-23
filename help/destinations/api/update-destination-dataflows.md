---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, atualizar fluxos de dados de destino
solution: Experience Platform
title: Atualizar fluxos de dados de destino usando a API de Serviço de Fluxo
topic-legacy: overview
type: Tutorial
description: Este tutorial aborda as etapas para atualizar um fluxo de dados de destino. Saiba como habilitar ou desabilitar o fluxo de dados, atualizar suas informações básicas ou adicionar e remover segmentos e atributos usando a API do Serviço de Fluxo.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 2%

---

# Atualizar fluxos de dados de destino usando a API de Serviço de Fluxo

Este tutorial aborda as etapas para atualizar um fluxo de dados de destino. Saiba como ativar ou desativar o fluxo de dados, atualizar suas informações básicas ou adicionar e remover segmentos e atributos usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Para obter informações sobre como editar fluxos de dados de destino usando a interface do usuário do Experience Platform, leia [Editar fluxos de ativação](/help/destinations/ui/edit-activation.md).

## Introdução {#get-started}

Este tutorial requer uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione o destino escolhido na [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas em [conectar-se ao destino](../ui/connect-destination.md) e [ativar dados](../ui/activation-overview.md) antes de tentar este tutorial.

>[!NOTE]
>
> Os termos *fluxo* e *fluxo de dados* são usados alternadamente neste tutorial. No contexto deste tutorial, o tem o mesmo significado.

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

A primeira etapa na atualização do fluxo de dados de destino é recuperar os detalhes do fluxo de dados usando a ID do fluxo. Você pode visualizar os detalhes atuais de um fluxo de dados existente fazendo uma solicitação do GET para a `/flows` endpoint .

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

Uma resposta bem-sucedida retorna os detalhes atuais do fluxo de dados, incluindo a versão, o identificador exclusivo (`id`) e outras informações relevantes.

```json
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
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Atualizar nome e descrição do fluxo de dados {#update-dataflow}

Para atualizar o nome e a descrição do seu fluxo de dados, execute uma solicitação de PATCH para a [!DNL Flow Service] API enquanto fornece a ID do fluxo, a versão e os novos valores que deseja usar.

>[!IMPORTANT]
>
>O `If-Match` é necessário usar o cabeçalho ao fazer uma solicitação de PATCH. O valor desse cabeçalho é a versão exclusiva do fluxo de dados que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de um fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir atualiza o nome e a descrição do seu fluxo de dados.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Ativar ou desativar o fluxo de dados {#enable-disable-dataflow}

Quando ativado, um fluxo de dados exporta perfis para o destino. Os fluxos de dados são ativados por padrão, mas podem ser desativados para pausar as exportações de perfil.

Você pode ativar ou desativar um fluxo de dados de destino existente, fazendo uma solicitação de POST para a [!DNL Flow Service] e fornecendo o estado para o qual você deseja atualizar o fluxo.

**Formato da API**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Solicitação**

A solicitação a seguir atualiza o estado do fluxo de dados para ativado.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

A solicitação a seguir atualiza o estado do fluxo de dados para desativado.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Adicionar um segmento a um fluxo de dados {#add-segment}

Para adicionar um segmento ao fluxo de dados de destino, execute uma solicitação de PATCH para a [!DNL Flow Service] API, fornecendo a ID do fluxo, a versão e o segmento que deseja adicionar.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir adiciona um novo segmento a um fluxo de dados de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. Para adicionar um segmento a um fluxo de dados, use o `add` operação. |
| `path` | Define a parte do fluxo que deve ser atualizada. Ao adicionar um segmento a um fluxo de dados, use o caminho especificado no exemplo. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |
| `id` | Especifique a ID do segmento que você está adicionando ao fluxo de dados de destino. |
| `name` | **(Opcional)**. Especifique o nome do segmento que você está adicionando ao fluxo de dados de destino. Observe que este campo não é obrigatório e você pode adicionar um segmento com êxito ao fluxo de dados de destino sem fornecer seu nome. |
| `filenameTemplate` | Para *destinos em lote* somente. Esse campo é necessário somente ao adicionar um segmento a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Esse campo determina o formato do nome do arquivo dos arquivos exportados para o seu destino. <br> As opções disponíveis são as seguintes: <br> <ul><li>`%DESTINATION_NAME%`: Obrigatório. Os arquivos exportados contêm o nome do destino.</li><li>`%SEGMENT_ID%`: Obrigatório. Os arquivos exportados contêm a ID do segmento exportado.</li><li>`%SEGMENT_NAME%`: **(Opcional)**. Os arquivos exportados contêm o nome do segmento exportado.</li><li>`DATETIME(YYYYMMdd_HHmmss)` ou `%TIMESTAMP%`: **(Opcional)**. Selecione uma dessas duas opções para que seus arquivos incluam o tempo em que são gerados pelo Experience Platform.</li><li>`custom-text`: **(Opcional)**. Substitua esse espaço reservado por qualquer texto personalizado que você gostaria de anexar ao final dos nomes de arquivo.</li></ul> <br> Para obter mais informações sobre como configurar nomes de arquivos, consulte o [configurar nomes de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) no tutorial de ativação de destinos em lote. |
| `exportMode` | Para *destinos em lote* somente. Esse campo é necessário somente ao adicionar um segmento a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. Selecione `"DAILY_FULL_EXPORT"` ou `"FIRST_FULL_THEN_INCREMENTAL"`. Para obter mais informações sobre as duas opções, consulte [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [exportar arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) no tutorial de ativação de destinos em lote. |
| `startDate` | Selecione a data em que o segmento deve começar a exportar perfis para seu destino. |
| `frequency` | Para *destinos em lote* somente. Esse campo é necessário somente ao adicionar um segmento a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. <br> <ul><li>Para o `"DAILY_FULL_EXPORT"` modo de exportação, é possível selecionar `ONCE` ou `DAILY`.</li><li>Para o `"FIRST_FULL_THEN_INCREMENTAL"` modo de exportação, é possível selecionar `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Para *destinos em lote* somente. Este campo é necessário somente ao selecionar a variável `"DAILY_FULL_EXPORT"` no modo `frequency` seletor. <br> Obrigatório. <br> <ul><li>Selecionar `"AFTER_SEGMENT_EVAL"` para que o trabalho de ativação seja executado imediatamente após a conclusão do trabalho diário de segmentação de lote da Platform. Isso garante que, quando o trabalho de ativação for executado, os perfis mais atualizados sejam exportados para o seu destino.</li><li>Selecionar `"SCHEDULED"` para que o trabalho de ativação seja executado em um horário fixo. Isso garante que os dados do perfil do Experience Platform sejam exportados ao mesmo tempo a cada dia, mas os perfis que você exporta podem não ser os mais atualizados, dependendo se o trabalho de segmentação em lote foi concluído antes do início do trabalho de ativação. Ao selecionar essa opção, você também deve adicionar uma `startTime` para indicar em que momento em UTC as exportações diárias devem ocorrer.</li></ul> |
| `endDate` | Para *destinos em lote* somente. Esse campo é necessário somente ao adicionar um segmento a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Não aplicável ao selecionar `"exportMode":"DAILY_FULL_EXPORT"` e `"frequency":"ONCE"`. <br> Define a data em que os membros do segmento param de ser exportados para o destino. |
| `startTime` | Para *destinos em lote* somente. Esse campo é necessário somente ao adicionar um segmento a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. Selecione a hora em que os arquivos contendo membros do segmento devem ser gerados e exportados para o seu destino. |

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Remover um segmento de um fluxo de dados {#remove-segment}

Para remover um segmento de um fluxo de dados de destino existente, execute uma solicitação de PATCH para a [!DNL Flow Service] API, fornecendo a ID do fluxo, a versão e o seletor de índice do segmento que deseja remover. A indexação começa em `0`. Por exemplo, a solicitação de amostra mais abaixo remove o primeiro e o segundo segmentos do fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir remove dois segmentos de um fluxo de dados de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. Para remover um segmento de um fluxo de dados, use o `remove` operação. |
| `path` | Especifica qual segmento existente deve ser removido do fluxo de dados de destino, com base no índice do seletor de segmentos. Para recuperar a ordem dos segmentos em um fluxo de dados, execute uma chamada de GET para a `/flows` endpoint e inspecione o `transformations.segmentSelectors` propriedade. Para excluir o primeiro segmento no fluxo de dados, use `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Atualizar componentes de um segmento em um fluxo de dados {#update-segment}

Você pode atualizar os componentes de um segmento em um fluxo de dados de destino existente. Por exemplo, é possível alterar a frequência de exportação ou editar o modelo de nome de arquivo. Para fazer isso, execute uma solicitação de PATCH para a função [!DNL Flow Service] API, fornecendo a ID do fluxo, a versão e o seletor de índice do segmento que deseja atualizar. A indexação começa em `0`. Por exemplo, a solicitação abaixo atualiza o nono segmento em um fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

Ao atualizar um segmento em um fluxo de dados de destino existente, você deve primeiro executar uma operação de GET para recuperar os detalhes do segmento que deseja atualizar. Em seguida, forneça todas as informações do segmento no payload, não apenas os campos que deseja atualizar. No exemplo abaixo, o texto personalizado é adicionado ao final do modelo de nome de arquivo e a frequência do agendamento de exportação é atualizada de 6 horas para 12 horas.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Para obter descrições das propriedades no payload, consulte a seção [Adicionar um segmento a um fluxo de dados](#add-segment).


**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Consulte os exemplos abaixo para obter mais exemplos de componentes do segmento que você pode atualizar em um fluxo de dados.

## Atualizar o modo de exportação de um segmento de agendado para depois da avaliação do segmento {#update-export-mode}

+++ Clique em para ver um exemplo em que uma exportação de segmento é atualizada de ser ativada todos os dias em um horário especificado para ser ativada todos os dias após a conclusão do trabalho de segmentação de lote da Platform.

O segmento é exportado todos os dias às 16:00 UTC.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

O segmento é exportado todos os dias após a conclusão do trabalho diário de segmentação em lote.

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Atualize o modelo de nome de arquivo para incluir campos adicionais no nome do arquivo {#update-filename-template}

+++ Clique em para ver um exemplo onde o modelo de nome de arquivo é atualizado para incluir campos adicionais no nome do arquivo

Os arquivos exportados contêm o nome de destino e a ID de segmento de Experience Platform

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

Os arquivos exportados contêm o nome de destino, a ID de Experience Platform segment, a data e a hora em que o arquivo foi gerado pelo Experience Platform e o texto personalizado anexado ao final dos arquivos.


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## Adicionar um atributo de perfil a um fluxo de dados {#add-profile-attribute}

Para adicionar um atributo de perfil ao fluxo de dados de destino, execute uma solicitação de PATCH para a função [!DNL Flow Service] API, fornecendo a ID do fluxo, a versão e o atributo de perfil que deseja adicionar.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir adiciona um novo atributo de perfil a um fluxo de dados de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. Para adicionar um atributo de perfil a um fluxo de dados, use o `add` operação. |
| `path` | Define a parte do fluxo que deve ser atualizada. Ao adicionar um atributo de perfil a um fluxo de dados, use o caminho especificado no exemplo. |
| `value.path` | O valor do atributo de perfil que você está adicionando ao fluxo de dados. |

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Remover um atributo de perfil de um fluxo de dados {#remove-profile-attribute}

Para remover um atributo de perfil de um fluxo de dados de destino existente, execute uma solicitação de PATCH para a [!DNL Flow Service] API ao fornecer a ID do fluxo, a versão e o seletor de índice do atributo de perfil que deseja remover. A indexação começa em `0`. Por exemplo, a solicitação de amostra mais abaixo remove o quinto atributo de perfil do fluxo de dados.


**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir remove um atributo de perfil de um fluxo de dados de destino existente.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. Para remover um segmento de um fluxo de dados, use o `remove` operação. |
| `path` | Especifica qual atributo de perfil existente deve ser removido do fluxo de dados de destino, com base no índice do seletor de segmentos. Para recuperar a ordem dos atributos do perfil em um fluxo de dados, execute uma chamada de GET para a função `/flows` endpoint e inspecione o `transformations.profileSelectors` propriedade. Para excluir o primeiro segmento no fluxo de dados, use `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Tratamento de erros da API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais da mensagem de erro da API de Experience Platform. Consulte [Códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma para obter mais informações sobre a interpretação das respostas dos erros.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você aprendeu a atualizar vários componentes de um fluxo de dados de destino, como adicionar ou remover segmentos ou atributos de perfil usando [!DNL Flow Service] API. Para obter mais informações sobre destinos, consulte a [visão geral dos destinos](../home.md).
