---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo, atualizar fluxos de dados
solution: Experience Platform
title: Atualizar fluxos de dados usando a API de serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Este tutorial aborda as etapas para atualizar um fluxo de dados, incluindo seu nome, descrição e programação, usando a API do Serviço de Fluxo.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---

# Atualizar fluxos de dados usando a API do Serviço de Fluxo

Este tutorial aborda as etapas para atualizar um fluxo de dados, incluindo informações básicas, programação e conjuntos de mapeamento usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este tutorial requer uma ID de fluxo válida. Se você não tiver uma ID de fluxo válida, selecione o conector escolhido na [visão geral das fontes](../../home.md) e siga as etapas descritas antes de tentar este tutorial.

Este tutorial também requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).

## Pesquisar detalhes do fluxo de dados

A primeira etapa na atualização do fluxo de dados é recuperar os detalhes do fluxo de dados usando a ID do fluxo. Você pode visualizar os detalhes atuais de um fluxo de dados existente fazendo uma solicitação do GET para a `/flows` endpoint .

**Formato da API**

```http
GET /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{FLOW_ID}` | O único `id` para o fluxo de dados que você deseja recuperar. |

**Solicitação**

A solicitação a seguir recupera informações atualizadas em relação à ID do fluxo.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes atuais do fluxo de dados, incluindo a versão, o agendamento e o identificador exclusivo (`id`).

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## Atualizar fluxo de dados

Para atualizar o cronograma de execução, o nome e a descrição do seu fluxo de dados, execute uma solicitação de PATCH para a [!DNL Flow Service] API, fornecendo a ID do fluxo, a versão e o novo agendamento que deseja usar.

>[!IMPORTANT]
>
>O `If-Match` é necessário usar o cabeçalho ao fazer uma solicitação de PATCH. O valor desse cabeçalho é a versão exclusiva da conexão que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de um fluxo de dados.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir atualiza o agendamento da execução do fluxo, bem como o nome e a descrição do seu fluxo de dados.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
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

## Atualizar mapeamento

Você pode atualizar o conjunto de mapeamentos de um fluxo de dados existente, fazendo uma solicitação de PATCH para o [!DNL Flow Service] API e fornecimento de valores atualizados para sua `mappingId` e `mappingVersion`.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitação**

A solicitação a seguir atualiza o conjunto de mapeamento do fluxo de dados.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| Propriedade | Descrição |
| --- | --- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace`e `remove`. |
| `path` | Define a parte do fluxo que deve ser atualizada. Neste exemplo, `transformations` O está sendo atualizado. |
| `value.name` | O nome da propriedade que deve ser atualizada. |
| `value.params.mappingId` | A nova ID de mapeamento a ser usada para atualizar o conjunto de mapeamento do fluxo de dados. |
| `value.params.mappingVersion` | A nova versão de mapeamento associada à ID de mapeamento atualizada. |

**Resposta**

Uma resposta bem-sucedida retorna a ID do fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação do GET para o [!DNL Flow Service] API, enquanto fornece a ID do fluxo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você atualizou as informações básicas, o agendamento e os conjuntos de mapeamento do seu fluxo de dados usando o [!DNL Flow Service] API. Para obter mais informações sobre o uso de conectores de origem, consulte o [visão geral das fontes](../../home.md).
