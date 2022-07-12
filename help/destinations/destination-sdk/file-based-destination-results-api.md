---
description: Esta página explica como usar o ponto de extremidade da API /testing/destinationInstance para visualizar os detalhes completos dos resultados do teste. Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar a API de Serviço de Fluxo para monitorar os fluxos de dados.
title: Exibir resultados detalhados da ativação
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# Exibir resultados detalhados da ativação {#view-test-results}

## Visão geral {#overview}

Esta página explica como usar a variável `/testing/destinationInstance` Ponto de extremidade da API para visualizar os detalhes completos de seus resultados de teste de destino com base em arquivo.

Se você já tiver [testou seu destino](file-based-destination-testing-api.md) e recebeu uma resposta de API válida, seu destino está funcionando corretamente.

Se você quiser ver informações mais detalhadas sobre o seu fluxo de ativação, poderá usar a variável `results` propriedade do [teste de destino](file-based-destination-testing-api.md) resposta do ponto final, conforme descrito abaixo.

>[!NOTE]
>
>Esse ponto de extremidade de API retorna o mesmo resultado que você obteria ao usar a variável [API de Serviço de Fluxo](../api/update-destination-dataflows.md) para monitorar os fluxos de dados.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de usar a variável `/testing/destinationInstance` , certifique-se de atender às seguintes condições:

* Você tem um destino com base em arquivo existente criado por meio do Destination SDK e pode vê-lo em seu [catálogo de destinos](../ui/destinations-workspace.md).
* Você criou pelo menos um fluxo de ativação para o seu destino na interface do usuário do Experience Platform.
* Para fazer a solicitação da API com êxito, é necessário a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, do URL, ao navegar em uma conexão com seu destino na interface do usuário da plataforma.

   ![Imagem da interface do usuário que mostra como obter a ID da instância de destino do URL.](assets/get-destination-instance-id.png)
* Você já [testou a configuração de destino](file-based-destination-testing-api.md)e receberam uma resposta de API válida, que inclui um `results` propriedade. Você usará `results` para testar ainda mais seu destino.

## Exibir resultados detalhados de testes de destino {#test-activation-results}

Depois de [validou sua configuração de destino](file-based-destination-testing-api.md), você pode visualizar resultados detalhados da ativação, fazendo uma solicitação do GET para o `authoring/testing/destinationInstance/` endpoint e fornecer a ID da instância de destino do destino que você está testando, além das IDs de execução de fluxo dos segmentos ativados.

Você pode encontrar o URL completo da API que precisa usar no `results` propriedade retornada em [resposta da chamada de teste de destino](file-based-destination-testing-api.md).

**Formato da API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Parâmetros de caminho | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino para a qual você está gerando perfis de amostra. Consulte a [pré-requisitos](#prerequisites) para obter detalhes sobre como obter essa ID. |

| Parâmetros da string de consulta | Descrição |
| -------- | ----------- |
| `flowRunIds` | As IDs de execução de fluxo correspondentes aos segmentos ativados. Você pode encontrar as IDs de execução de fluxo no `results` propriedade retornada em [resposta da chamada de teste de destino](file-based-destination-testing-api.md). |

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

A resposta contém os detalhes completos do fluxo de ativação. Você pode obter a mesma resposta, chamando a função [API de Serviço de Fluxo](../api/update-destination-dataflows.md) para monitorar os fluxos de dados.

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

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Após a leitura deste documento, você agora sabe como testar sua configuração de destino baseada em arquivo e ver os detalhes completos de seus resultados de ativação.

Se estiver criando um destino público, agora é possível [enviar sua configuração de destino](../destination-sdk/submit-destination.md) para Adobe para revisão.
