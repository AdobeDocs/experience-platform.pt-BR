---
keywords: Experience Platform;página inicial;tópicos populares;serviço de fluxo;atualizar fluxos de dados de destino
solution: Experience Platform
title: Atualizar fluxos de dados de destino usando a API de serviço de fluxo
type: Tutorial
description: Este tutorial aborda as etapas para atualizar um fluxo de dados de destino. Saiba como habilitar ou desabilitar o fluxo de dados, atualizar suas informações básicas ou adicionar e remover públicos-alvo e atributos usando a API do Serviço de fluxo.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 7f8fbbec8927dffb3c8456b2a1d908d27d4b03c2
workflow-type: tm+mt
source-wordcount: '2471'
ht-degree: 4%

---

# Atualizar fluxos de dados de destino usando a API de serviço de fluxo

Este tutorial aborda as etapas para atualizar um fluxo de dados de destino. Saiba como habilitar ou desabilitar o fluxo de dados, atualizar suas informações básicas ou adicionar e remover públicos e atributos usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Para obter informações sobre como editar fluxos de dados de destino usando a interface do Experience Platform, leia [Editar fluxos de ativação](/help/destinations/ui/edit-activation.md).

## Introdução {#get-started}

Este tutorial requer que você tenha uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione seu destino escolhido no [catálogo de destinos](../catalog/overview.md) e siga as etapas descritas para [conectar-se ao destino](../ui/connect-destination.md) e [ativar dados](../ui/activation-overview.md) antes de tentar este tutorial.

>[!NOTE]
>
> Os termos *fluxo* e *fluxo de dados* são usados alternadamente neste tutorial. No contexto deste tutorial, eles têm o mesmo significado.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
* [Sandboxes](../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para atualizar seu fluxo de dados com êxito usando a API [!DNL Flow Service].

### Leitura de chamadas de API de amostra {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos obrigatórios {#gather-values-for-required-headers}

Para fazer chamadas para APIs do Experience Platform, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos no Experience Platform, incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para APIs do Experience Platform exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Se o cabeçalho `x-sandbox-name` não for especificado, as solicitações serão resolvidas na sandbox `prod`.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Pesquisar detalhes do fluxo de dados {#look-up-dataflow-details}

A primeira etapa na atualização do fluxo de dados de destino é recuperar os detalhes do fluxo de dados usando a ID do fluxo. Você pode exibir os detalhes atuais de um fluxo de dados existente fazendo uma solicitação GET para o ponto de extremidade `/flows`.

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O valor `id` exclusivo para o fluxo de dados de destino que você deseja recuperar. |

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

Para atualizar o nome e a descrição do fluxo de dados, execute uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID do fluxo, a versão e os novos valores que deseja usar.

>[!IMPORTANT]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação PATCH. O valor desse cabeçalho é a versão exclusiva do fluxo de dados que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de um fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir atualiza o nome e a descrição do fluxo de dados.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Ativar ou desativar fluxo de dados {#enable-disable-dataflow}

Quando ativado, um fluxo de dados exporta perfis para o destino. Os fluxos de dados são ativados por padrão, mas podem ser desativados para pausar as exportações de perfil.

Você pode habilitar ou desabilitar um fluxo de dados de destino existente fazendo uma solicitação POST para a API [!DNL Flow Service] e fornecendo o estado para o qual deseja atualizar o fluxo.

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

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Adicionar um público a um fluxo de dados {#add-segment}

Para adicionar um público-alvo ao fluxo de dados de destino, execute uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID do fluxo, a versão e o público-alvo que deseja adicionar.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir adiciona um novo público-alvo a um fluxo de dados de destino existente.

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. Para adicionar uma audiência a um fluxo de dados, use a operação `add`. |
| `path` | Define a parte do fluxo que deve ser atualizada. Ao adicionar um público-alvo a um fluxo de dados, use o caminho especificado no exemplo. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |
| `id` | Especifique a ID do público-alvo que você está adicionando ao fluxo de dados de destino. |
| `name` | **(Opcional)**. Especifique o nome do público-alvo que você está adicionando ao fluxo de dados de destino. Observe que esse campo não é obrigatório e que você pode adicionar um público-alvo ao fluxo de dados de destino com êxito sem fornecer seu nome. |
| `filenameTemplate` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Este campo determina o formato do nome de arquivo dos arquivos exportados para o seu destino. <br> As seguintes opções estão disponíveis: <br> <ul><li>`%DESTINATION_NAME%`: Obrigatório. Os arquivos exportados contêm o nome de destino.</li><li>`%SEGMENT_ID%`: Obrigatório. Os arquivos exportados contêm a ID do público-alvo exportado.</li><li>`%SEGMENT_NAME%`: **(Opcional)**. Os arquivos exportados contêm o nome do público exportado.</li><li>`DATETIME(YYYYMMdd_HHmmss)` ou `%TIMESTAMP%`: **(Opcional)**. Selecione uma dessas duas opções para que seus arquivos incluam a hora em que são gerados pelo Experience Platform.</li><li>`custom-text`: **(Opcional)**. Substitua esse espaço reservado por qualquer texto personalizado que queira anexar ao final dos nomes de arquivo.</li></ul> <br> Para obter mais informações sobre como configurar nomes de arquivos, consulte a seção [configurar nomes de arquivos](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) no tutorial de ativação de destinos em lote. |
| `exportMode` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. Selecione `"DAILY_FULL_EXPORT"` ou `"FIRST_FULL_THEN_INCREMENTAL"`. Para obter mais informações sobre as duas opções, consulte [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [exportar arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) no tutorial de ativação de destinos em lote. |
| `startDate` | Selecione a data em que o público-alvo deve começar a exportar perfis para o seu destino. |
| `frequency` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. <br> <ul><li>Para o modo de exportação `"DAILY_FULL_EXPORT"`, você pode selecionar `ONCE` ou `DAILY`.</li><li>Para o modo de exportação `"FIRST_FULL_THEN_INCREMENTAL"`, você pode selecionar `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Somente para *destinos em lote*. Este campo é necessário somente ao selecionar o modo `"DAILY_FULL_EXPORT"` no seletor `frequency`. <br> Obrigatório. <br> <ul><li>Selecione `"AFTER_SEGMENT_EVAL"` para que o trabalho de ativação seja executado imediatamente após a conclusão diária do trabalho de segmentação em lote do Experience Platform. Isso garante que, quando o trabalho de ativação for executado, os perfis mais atualizados sejam exportados para o seu destino.</li><li>Selecione `"SCHEDULED"` para que o trabalho de ativação seja executado em um horário fixado. Isso garante que os dados de perfil do Experience Platform sejam exportados ao mesmo tempo todos os dias, mas os perfis exportados podem não ser os mais atualizados, dependendo se o trabalho de segmentação em lote foi concluído antes do início do trabalho de ativação. Ao selecionar essa opção, você também deve adicionar um `startTime` para indicar em que horário em UTC as exportações diárias devem ocorrer.</li></ul> |
| `endDate` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Não aplicável ao selecionar `"exportMode":"DAILY_FULL_EXPORT"` e `"frequency":"ONCE"`. <br> Define a data em que os membros do público-alvo param de ser exportados para o destino. |
| `startTime` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. Selecione a hora em que os arquivos que contêm membros do público-alvo devem ser gerados e exportados para o seu destino. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Remover um público-alvo de um fluxo de dados {#remove-segment}

Para remover um público-alvo de um fluxo de dados de destino existente, execute uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID de fluxo, a versão e o seletor de índice do público-alvo que você deseja remover. A indexação começa às `0`. Por exemplo, a solicitação de amostra mais abaixo remove o primeiro e o segundo públicos-alvo do fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir remove dois públicos-alvo de um fluxo de dados de destino existente.

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
   "path":"/transformations/0/params/segmentSelectors/selectors/0",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/1",
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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. Para remover um público de um fluxo de dados, use a operação `remove`. |
| `path` | Especifica qual público-alvo existente deve ser removido do fluxo de dados de destino, com base no índice do seletor de público-alvo. Para recuperar a ordem dos públicos em um fluxo de dados, execute uma chamada GET para o ponto de extremidade `/flows` e inspecione a propriedade `transformations.segmentSelectors`. Para excluir o primeiro público no fluxo de dados, use `"path":"/transformations/0/params/segmentSelectors/selectors/0"`. |


**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Atualizar componentes de um público em um fluxo de dados {#update-segment}

Você pode atualizar componentes de um público-alvo em um fluxo de dados de destino existente. Por exemplo, você pode alterar a frequência de exportação ou editar o modelo de nome de arquivo. Para fazer isso, execute uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID do fluxo, a versão e o seletor de índice do público-alvo que você deseja atualizar. A indexação começa às `0`. Por exemplo, a solicitação abaixo atualiza o nono público-alvo em um fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

Ao atualizar um público-alvo em um fluxo de dados de destino existente, primeiro execute uma operação do GET para recuperar os detalhes do público-alvo que deseja atualizar. Em seguida, forneça todas as informações do público-alvo na carga, não apenas os campos que você deseja atualizar. No exemplo abaixo, o texto personalizado é adicionado ao final do modelo de nome de arquivo e a frequência de programação de exportação é atualizada de 6 horas para 12 horas.

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

Para obter descrições das propriedades na carga, consulte a seção [Adicionar uma audiência a um fluxo de dados](#add-segment).


**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Consulte os exemplos abaixo para obter mais exemplos de componentes de público-alvo que você pode atualizar em um fluxo de dados.

## Atualizar o modo de exportação de um público do agendado para o depois da avaliação do público {#update-export-mode}

+++ Clique para ver um exemplo em que uma exportação de público-alvo é atualizada de ser ativada todos os dias em um horário especificado para ser ativada todos os dias após a conclusão do trabalho de segmentação em lote do Experience Platform.

O público é exportado todos os dias às 16:00 UTC.

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

O público-alvo é exportado todos os dias após a conclusão diária do trabalho de segmentação em lote.

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

## Atualizar o modelo de nome de arquivo para incluir campos adicionais no nome do arquivo {#update-filename-template}

+++ Clique para ver um exemplo em que o modelo de nome de arquivo é atualizado para incluir campos adicionais no nome do arquivo

Os arquivos exportados contêm o nome de destino e a ID de público-alvo do Experience Platform

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

Os arquivos exportados contêm o nome de destino, a ID de público-alvo do Experience Platform, a data e a hora em que o arquivo foi gerado pelo Experience Platform e o texto personalizado anexado ao final dos arquivos.


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

Para adicionar um atributo de perfil ao fluxo de dados de destino, execute uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID do fluxo, a versão e o atributo de perfil que você deseja adicionar.

>[!IMPORTANT]
>
>**Requisitos de mapeamento específicos do destino**
>
>O método `profileSelectors` descrito nesta seção funciona para a maioria dos destinos de streaming. No entanto, alguns destinos de streaming, incluindo **Adobe Target**, exigem o fluxo de trabalho do conjunto de mapeamento Preparo de Dados.
>
>**Se os atributos de perfil não aparecerem na interface do usuário do Experience Platform após uma resposta de API bem-sucedida (202)**, você deverá usar o método de conjunto de mapeamento documentado em [Ativar públicos para destinos em lote](../api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. Para adicionar um atributo de perfil a um fluxo de dados, use a operação `add`. |
| `path` | Define a parte do fluxo que deve ser atualizada. Ao adicionar um atributo de perfil a um fluxo de dados, use o caminho especificado no exemplo. |
| `value.path` | O valor do atributo de perfil que você está adicionando ao fluxo de dados. |

**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Remover um atributo de perfil de um fluxo de dados {#remove-profile-attribute}

Para remover um atributo de perfil de um fluxo de dados de destino existente, execute uma solicitação PATCH para a API [!DNL Flow Service] enquanto fornece a ID de fluxo, a versão e o seletor de índice do atributo de perfil que você deseja remover. A indexação começa às `0`. Por exemplo, a solicitação de amostra mais abaixo remove o quinto atributo de perfil do fluxo de dados.


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
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. Para remover um público de um fluxo de dados, use a operação `remove`. |
| `path` | Especifica qual atributo de perfil existente deve ser removido do fluxo de dados de destino, com base no índice do seletor de público-alvo. Para recuperar a ordem dos atributos de perfil em um fluxo de dados, execute uma chamada GET para o ponto de extremidade `/flows` e inspecione a propriedade `transformations.profileSelectors`. Para excluir o primeiro público no fluxo de dados, use `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Manipulação de erros de API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform para obter mais informações sobre como interpretar respostas de erro.

## Próximas etapas {#next-steps}

Seguindo este tutorial, você aprendeu a atualizar vários componentes de um fluxo de dados de destino, como adicionar ou remover públicos ou atributos de perfil usando a API [!DNL Flow Service]. Para obter mais informações sobre destinos, consulte a [visão geral sobre destinos](../home.md).
