---
description: Esta página explica como usar o endpoint da API /testing/destinationInstance para exibir os detalhes completos dos resultados de seus testes. Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar a API de serviço de fluxo para monitorar os fluxos de dados.
title: Exibir resultados detalhados da ativação
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# Exibir resultados detalhados da ativação {#view-test-results}

## Visão geral {#overview}

Esta página explica como usar a variável `/testing/destinationInstance` Endpoint da API para exibir os detalhes completos dos resultados do teste de destino baseado em arquivo.

Se você já tiver [testou seu destino](file-based-destination-testing-api.md) e tiver recebido uma resposta de API válida, seu destino está funcionando corretamente.

Se quiser ver informações mais detalhadas sobre o fluxo de ativação, use o `results` propriedade do [teste de destino](file-based-destination-testing-api.md) resposta do terminal, conforme descrito mais abaixo.

>[!NOTE]
>
>Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar o [API do serviço de fluxo](../../../api/update-destination-dataflows.md) para monitorar fluxos de dados.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de poder usar o `/testing/destinationInstance` verifique se você atende às seguintes condições:

* Você tem um destino baseado em arquivo existente criado por meio do Destination SDK e pode visualizá-lo em seu [catálogo de destinos](../../../ui/destinations-workspace.md).
* Você criou pelo menos um fluxo de ativação para o destino na interface do usuário do Experience Platform.
* Para fazer a solicitação de API com êxito, é necessário ter a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, no URL, ao navegar por uma conexão com seu destino na interface do Platform.

  ![Imagem da interface mostrando como obter a ID da instância de destino do URL.](../../assets/testing-api/get-destination-instance-id.png)
* Você já [testou a configuração de destino](file-based-destination-testing-api.md)e recebeu uma resposta de API válida, que inclui uma `results` propriedade. Você usará este `results` para testar ainda mais seu destino.

## Exibir resultados detalhados do teste de destino {#test-activation-results}

Depois de [validou sua configuração de destino](file-based-destination-testing-api.md), você poderá ver os resultados detalhados da ativação fazendo uma solicitação GET ao `authoring/testing/destinationInstance/` e fornecer a ID de instância de destino do destino que você está testando, bem como as IDs de execução de fluxo dos públicos ativados.

Você pode encontrar o URL completo da API que precisa usar no `results` propriedade retornada na variável [resposta da chamada de teste de destino](file-based-destination-testing-api.md).

**Formato da API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Parâmetros de caminho | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino para a qual você está gerando perfis de amostra. Consulte a [pré-requisitos](#prerequisites) para obter detalhes sobre como obter essa ID. |

| Parâmetros da string de consulta | Descrição |
| -------- | ----------- |
| `flowRunIds` | As IDs de execução do fluxo correspondentes aos públicos ativados. Você pode encontrar as IDs de execução de fluxo na `results` propriedade retornada na variável [resposta da chamada de teste de destino](file-based-destination-testing-api.md). |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta contém os detalhes completos do fluxo de ativação. Você pode obter a mesma resposta chamando o [API do serviço de fluxo](../../../api/update-destination-dataflows.md) para monitorar fluxos de dados.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como testar a configuração de destino baseada em arquivo e ver os detalhes completos dos resultados da ativação.

Se você estiver criando um destino público, poderá [enviar sua configuração de destino](../../guides/submit-destination.md) para Adobe para revisão.
