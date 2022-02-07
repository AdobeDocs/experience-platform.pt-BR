---
keywords: Experience Platform; home; tópicos populares; notificações
description: Ao se inscrever em Adobe I/O Events, você pode usar webhooks para receber notificações sobre os status de execução de fluxo das conexões de origem. Essas notificações contêm informações sobre o sucesso de sua execução de fluxo ou erros que contribuíram para uma falha de execução.
solution: Experience Platform
title: Notificações de Execução de Fluxo
topic-legacy: overview
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: a51c878bbfd3004cb597ce9244a9ed2f2318604b
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# Notificações de execução de fluxo

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) é usada para coletar e centralizar dados do cliente de várias fontes diferentes no [!DNL Platform]. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Com Adobe I/O Events, você pode assinar eventos e usar webhooks para receber notificações sobre o status de suas execuções de fluxo. Essas notificações contêm informações sobre o sucesso de sua execução de fluxo ou erros que contribuíram para uma falha de execução.

Este documento fornece etapas sobre como se inscrever em eventos, registrar webhooks e receber notificações contendo informações sobre o status de suas execuções de fluxo.

## Introdução

Este tutorial pressupõe que você já criou pelo menos uma conexão de origem cujo fluxo é executado e deseja monitorar. Se ainda não tiver configurado uma conexão de origem, comece visitando a [visão geral das fontes](./home.md) para configurar a fonte de sua escolha antes de retornar a este guia.

Este documento também requer uma compreensão funcional de webhooks e como conectar um webhook de um aplicativo a outro. Consulte a [[!DNL I/O Events] documentação](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para uma introdução aos webhooks.

## Registrar um webhook para notificações de execução de fluxo

Para receber notificações de execução de fluxo, você deve usar o Console do desenvolvedor do Adobe para registrar um webhook em seu [!DNL Experience Platform] integração.

Siga o tutorial em [assinando notificações do [!DNL I/O Event]](../observability/alerts/subscribe.md) para obter etapas detalhadas sobre como fazer isso.

>[!IMPORTANT]
>
>Durante o processo de assinatura, certifique-se de selecionar **[!UICONTROL Notificações da plataforma]** como provedor de eventos e selecione as seguintes assinaturas de eventos:
>
>* **[!UICONTROL Êxito na Execução do Fluxo da Fonte de Experience Platform]**
>* **[!UICONTROL Falha na Execução de Fluxo da Fonte Experience Platform]**


## Receber notificações de execução de fluxo

Com seu webhook conectado e sua assinatura de evento concluída, você pode começar a receber notificações de execução de fluxo pelo painel do webhook.

Uma notificação retorna informações como o número de trabalhos de assimilação executados, o tamanho do arquivo e erros. Uma notificação também retorna uma carga associada à execução do fluxo no formato JSON. A carga de resposta pode ser classificada como `sources_flow_run_success` ou `sources_flow_run_failure`.

>[!IMPORTANT]
>
>Se a assimilação parcial estiver ativada durante o processo de criação do fluxo, um fluxo que contenha assimilações bem-sucedidas e com falha será marcado como `sources_flow_run_success` somente se o número de erros estiver abaixo da porcentagem do limite de erro definida durante o processo de criação de fluxo. Se uma execução de fluxo bem-sucedida contiver erros, esses erros ainda serão incluídos como parte da carga útil de retorno.

### Sucesso

Uma resposta bem-sucedida retorna um conjunto de `metrics` que definam características de um fluxo específico e `activities` que descrevem como os dados são transformados.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{IMS_ORG}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `metrics` | Define características dos dados na execução do fluxo. |
| `activities` | Define as diferentes etapas e atividades que são executadas para transformar os dados. |
| `durationSummary` | Define a hora inicial e final da execução do fluxo. |
| `sizeSummary` | Define o volume dos dados em bytes. |
| `recordSummary` | Define a contagem de registros dos dados. |
| `fileSummary` | Define a contagem de arquivos dos dados. |
| `fileInfo` | Um URL que leva a uma visão geral dos arquivos assimilados com êxito. |
| `statusSummary` | Define se a execução do fluxo é bem-sucedida ou uma falha. |

### Falha

A resposta a seguir é um exemplo de falha na execução do fluxo, com um erro ocorrendo à medida que os dados copiados são processados. Erros também podem ocorrer enquanto os dados estão sendo copiados da fonte. Uma execução de fluxo com falha inclui informações sobre os erros que contribuíram para a falha da execução, incluindo seu erro e descrição.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{IMS_ORG}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Propriedade | Descrição |
| ---------- | ----------- |
| `fileInfo` | Um URL que leva a uma visão geral dos arquivos que foram assimilados com êxito e sem êxito. |

>[!NOTE]
>
>Consulte a [apêndice](#errors) para obter mais informações sobre mensagens de erro.

## Próximas etapas

Agora é possível assinar eventos que permitem receber notificações em tempo real nos status de execução de fluxo. Para obter mais informações sobre execuções e fontes de fluxo, consulte o [visão geral das fontes](./home.md).

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com notificações de execução de fluxo.

### Noções básicas sobre mensagens de erro {#errors}

Erros de assimilação podem ocorrer quando os dados estão sendo copiados da fonte ou quando os dados copiados estão sendo processados para o [!DNL Platform]. Consulte a tabela abaixo para obter mais informações sobre erros específicos.

| Erro | Descrição |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Ocorreu um erro ao copiar dados de uma origem. |
| `CONNECTOR-2001-500` | Ocorreu um erro ao processar os dados copiados para o [!DNL Platform]. Esse erro pode ser relacionado à análise, validação ou transformação. |
