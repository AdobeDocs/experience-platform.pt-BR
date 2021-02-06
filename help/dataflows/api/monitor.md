---
keywords: Experience Platform;home;popular topics;monitor dataflows;flow service api;Flow Service Service
solution: Experience Platform
title: Monitorar fluxos de dados usando a API de serviço de fluxo
topic: overview
type: Tutorial
description: Este tutorial aborda as etapas para monitorar os dados de execução do fluxo para obter integridade, erros e métricas usando a API de Serviço de Fluxo.
translation-type: tm+mt
source-git-commit: f8186e467dc982003c6feb01886ed16d23572955
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# Monitorar fluxos de dados usando a API de Serviço de Fluxo

A Adobe Experience Platform permite que os dados sejam ingeridos de fontes externas e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamentos baseados em nuvem, bancos de dados e muitas outras. Além disso, o Experience Platform permite que os dados sejam ativados para parceiros externos.

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes e destinos suportados são conectáveis.

Este tutorial aborda as etapas para monitorar os dados de execução do fluxo para obter integridade, erros e métricas usando [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Introdução

Este tutorial requer que você tenha o valor de ID de um fluxo de dados válido. Se você não tiver uma ID de fluxo de dados válida, selecione seu conector de escolha na [visão geral das fontes](../../sources/home.md) ou [visão geral dos destinos](../../destinations/catalog/overview.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também exige que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação contínua de dados da Plataforma para campanhas de marketing entre canais, campanhas de email, anúncios direcionados e muitos outros casos de uso.
- [Fontes](../../sources/home.md):  [!DNL Experience Platform] permite que os dados sejam ingeridos de várias fontes e, ao mesmo tempo, fornece a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando  [!DNL Platform] serviços.
- [Caixas de proteção](../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para monitorar com êxito as execuções de fluxo usando a API [!DNL Flow Service].

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

- `Content-Type: application/json`

## O fluxo do monitor é executado

Depois de fazer um fluxo de dados, execute uma solicitação de GET para a API [!DNL Flow Service].

**Formato da API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O valor exclusivo `id` para o fluxo de dados que você deseja monitorar. |

**Solicitação**

A solicitação a seguir recupera as especificações de um fluxo de dados existente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes sobre a execução do fluxo, incluindo informações sobre a data de criação, as conexões de origem e de público alvo, bem como o identificador exclusivo da execução do fluxo (`id`).

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `items` | Contém uma única carga de metadados associada à sua execução de fluxo específica. |
| `metrics` | As características dos dados na execução do fluxo. |
| `activities` | Mostra como os dados são transformados. |
| `durationSummary` | O start e a hora de término da execução do fluxo. |
| `sizeSummary` | O volume dos dados em bytes. |
| `recordSummary` | A contagem de registros dos dados. |
| `fileSummary` | O arquivo conta os dados. |
| `fileSummary.extensions` | Contém informações específicas da atividade. Por exemplo, `manifest` é apenas parte da &quot;Atividade de promoção&quot; e, portanto, está incluída no objeto `extensions`. |
| `statusSummary` | Mostra se a execução do fluxo é bem-sucedida ou uma falha. |

## Próximas etapas

Ao seguir este tutorial, você recuperou métricas e informações de erro no seu fluxo de dados usando a API [!DNL Flow Service]. Agora você pode continuar monitorando seu fluxo de dados, dependendo do seu agendamento de ingestão, para rastrear seu status e taxas de ingestão. Para obter informações sobre como monitorar fluxos de dados para fontes, leia o tutorial [fluxo de dados de monitoramento para fontes usando a interface do usuário](../ui/monitor-sources.md). Para obter mais informações sobre como monitorar fluxos de dados para destinos, leia o tutorial [fluxo de dados de monitoramento para destinos usando a interface do usuário](../ui/monitor-destinations.md).