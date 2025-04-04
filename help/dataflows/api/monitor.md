---
keywords: Experience Platform;página inicial;tópicos populares;monitorar fluxos de dados;api do serviço de fluxo;Serviço de fluxo
solution: Experience Platform
title: Monitorar fluxos de dados usando a API do serviço de fluxo
type: Tutorial
description: Este tutorial aborda as etapas para monitorar a integridade, os erros e as métricas da execução do fluxo usando a API do serviço de fluxo.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 8%

---

# Monitorar fluxos de dados usando a API de serviço de fluxo

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras. Além disso, o Experience Platform permite que os dados sejam ativados para parceiros externos.

O [!DNL Flow Service] é usado para coletar e centralizar dados do cliente de várias fontes diferentes na Adobe Experience Platform. O serviço fornece uma interface de usuário e a API RESTful a partir da qual todas as fontes e destinos compatíveis são conectáveis.

Este tutorial aborda as etapas para monitorar dados de execução do fluxo para integridade, erros e métricas usando o [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer que você tenha o valor de ID de um fluxo de dados válido. Se você não tiver uma ID de fluxo de dados válida, selecione seu conector escolhido na [visão geral das fontes](../../sources/home.md) ou na [visão geral dos destinos](../../destinations/catalog/overview.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer que você tenha uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Destinos](../../destinations/home.md): os destinos são integrações pré-criadas com aplicativos usados com frequência que permitem a ativação contínua de dados do Experience Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
- [Fontes](../../sources/home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para monitorar com êxito as execuções de fluxo usando a API [!DNL Flow Service].

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

- `Content-Type: application/json`

## Monitorar execuções de fluxo

Depois de fazer um fluxo de dados, execute uma solicitação GET para a API [!DNL Flow Service].

**Formato da API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O valor `id` exclusivo para o fluxo de dados que você deseja monitorar. |

**Solicitação**

A solicitação a seguir recupera as especificações de um fluxo de dados existente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes sobre a execução do fluxo, incluindo informações sobre a data de criação, conexões de origem e destino, bem como o identificador exclusivo da execução do fluxo (`id`).

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
            "imsOrgId": "{ORG_ID}",
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
| `items` | Contém uma única carga de metadados associada à execução do fluxo específico. |
| `metrics` | As características dos dados na execução do fluxo. |
| `activities` | Mostra como os dados são transformados. |
| `durationSummary` | As horas inicial e final da execução do fluxo. |
| `sizeSummary` | O volume dos dados em bytes. |
| `recordSummary` | A contagem de registros dos dados. |
| `fileSummary` | O arquivo conta os dados. |
| `fileSummary.extensions` | Contém informações específicas da atividade. Por exemplo, `manifest` é apenas parte da &quot;Atividade de promoção&quot; e, portanto, está incluída no objeto `extensions`. |
| `statusSummary` | Mostra se a execução do fluxo foi bem-sucedida ou falhou. |

## Próximas etapas

Seguindo este tutorial, você recuperou métricas e informações de erro no fluxo de dados usando a API [!DNL Flow Service]. Agora é possível continuar a monitorar o fluxo de dados, dependendo da programação de assimilação, para rastrear o status e as taxas de assimilação. Para obter informações sobre como monitorar fluxos de dados de fontes, leia o [tutorial sobre monitoramento de fluxos de dados de fontes usando a interface do usuário](../ui/monitor-sources.md). Para obter mais informações sobre como monitorar fluxos de dados para destinos, leia o [tutorial sobre monitoramento de fluxos de dados para destinos usando a interface do usuário](../ui/monitor-destinations.md).
