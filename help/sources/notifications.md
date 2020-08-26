---
keywords: Experience Platform;home;popular topics; notifications
description: Com os Eventos de E/S de Adobe, você pode assinar eventos e usar webhooks para receber notificações sobre o status de suas execuções de fluxo. Essas notificações contêm informações sobre o sucesso de sua execução de fluxo ou erros que contribuíram para a falha de uma execução.
solution: Experience Platform
title: Notificações de execução de fluxo
topic: overview
translation-type: tm+mt
source-git-commit: b5b785d8415c15e3acb9e1155811a66c51477717
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---


# Notificações de execução de fluxo

A Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras.

[O [!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) é usado para coletar e centralizar dados do cliente de várias fontes diferentes dentro [!DNL Platform]. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Com Eventos de E/S de Adobe, você pode assinar eventos e usar webhooks para receber notificações sobre o status de suas execuções de fluxo. Essas notificações contêm informações sobre o sucesso de sua execução de fluxo ou erros que contribuíram para a falha de uma execução.

Este documento fornece etapas sobre como assinar eventos, registrar webhooks e receber notificações contendo informações sobre o status de suas execuções de fluxo.

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do [!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Perfil do cliente em tempo real]](../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [[!DNL ingestão de dados Adobe Experience Platform]](../ingestion/home.md): [!DNL Data Ingestion] representa os vários métodos pelos quais [!DNL Platform] ingere dados dessas fontes, bem como como como esses dados são mantidos dentro do [!DNL Data Lake] para uso pelos [!DNL Platform] serviços de downstream.

Este documento também requer um entendimento prático dos webhooks e como conectar um webhook de um aplicativo a outro. Consulte a [documentação](https://requestbin.com/blog/working-with-webhooks/) a seguir para obter mais informações sobre webhooks.

## Registrar seu webhook

Para receber notificações sobre o status de sua execução de fluxo, você deve registrar um webhook especificando um URL exclusivo do webhook como parte dos detalhes de registro do evento. Para conectar um webhook à sua [!DNL I/O Events] subscrição, visite o serviço [de](https://webhook.site/) webhook e copie o URL exclusivo fornecido.

![webhook](./images/notifications/webhook-url.png)

## Inscrever-se em eventos

Depois de adquirir um URL exclusivo do webhook, vá para Eventos [de E/S do](https://www.adobe.io/apis/experienceplatform/events.html) Adobe e siga as etapas descritas no documento de notificações [de ingestão de](../ingestion/quality/subscribe-events.md) dados para inscrição em eventos.

>[!IMPORTANT]
>Durante o processo de subscrição, selecione [!DNL Platform] as notificações como provedor de eventos e selecione as seguintes subscrições de eventos:
>
>* **[!UICONTROL Execução de Fluxo da Fonte de Experience Platform com Êxito]**
>* **[!UICONTROL Falha na Execução de Fluxo da Fonte de Experience Platform]**

>
>
Quando solicitado a fornecer um endereço de webhook, use o URL de webhook adquirido anteriormente.

## Receber notificações de execução de fluxo

Com o webhook conectado e a subscrição do evento concluída, você pode start recebendo notificações de fluxo pelo painel do webhook.

Uma notificação retorna informações como o número de trabalhos de ingestão executados, o tamanho do arquivo e os erros. Uma notificação também retorna uma carga associada à execução do fluxo no formato JSON. A carga de resposta pode ser classificada como `sources_flow_run_success` ou `sources_flow_run_failure`.

>[!IMPORTANT]
>Se a ingestão parcial estiver ativada durante o processo de criação de fluxo, um fluxo que contenha as ingestões bem-sucedidas e com falha será marcado como `sources_flow_run_success` somente se o número de erros estiver abaixo da porcentagem limite de erro definida durante o processo de criação de fluxo. Se uma execução de fluxo bem-sucedida contiver erros, esses erros ainda serão incluídos como parte da carga de retorno.

### Sucesso

Uma resposta bem-sucedida retorna um conjunto de `metrics` que define características de uma execução de fluxo específica e `activities` que descreve como os dados são transformados.

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
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
| `metrics` | Define as características dos dados na execução de fluxo. |
| `activities` | Define as diferentes etapas e atividades executadas para transformar os dados. |
| `durationSummary` | Define o start e a hora de término da execução do fluxo. |
| `sizeSummary` | Define o volume dos dados em bytes. |
| `recordSummary` | Define a contagem de registros dos dados. |
| `fileSummary` | Define a contagem de arquivos dos dados. |
| `fileInfo` | Um URL que leva a uma visão geral dos arquivos assimilados com êxito. |
| `statusSummary` | Define se a execução do fluxo é bem-sucedida ou uma falha. |

### Falha

A resposta a seguir é um exemplo de falha na execução do fluxo, com um erro ocorrendo à medida que os dados copiados são processados. Os erros também podem ocorrer enquanto os dados são copiados da fonte. Uma execução de fluxo com falha inclui informações sobre os erros que contribuíram para a falha da execução, incluindo seu erro e descrição.

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
>Consulte o [apêndice](#errors) para obter mais informações sobre mensagens de erro.

## Próximas etapas

Agora você pode se inscrever em eventos que permitem receber notificações em tempo real nos status de execução de fluxo. Para obter mais informações sobre execuções e fontes de fluxo, consulte a visão geral [das](./home.md)fontes.

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com notificações de execução de fluxo.

### Noções básicas sobre mensagens de erro {#errors}

Erros de ingestão podem ocorrer quando os dados estão sendo copiados da fonte ou quando os dados copiados estão sendo processados para [!DNL Platform]. Consulte a tabela abaixo para obter mais informações sobre erros específicos.

| Erro | Descrição |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Erro ao copiar dados de uma fonte. |
| `CONNECTOR-2001-500` | Ocorreu um erro ao processar os dados copiados para [!DNL Platform]. Esse erro pode ser relacionado à análise, validação ou transformação. |
