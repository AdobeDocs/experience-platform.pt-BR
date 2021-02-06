---
keywords: Experience Platform;guia do desenvolvedor;endpoint;Data Science Workspace;topics populares;
solution: Experience Platform
title: Apêndice do Guia API de Aprendizagem de Máquinas do Sensei
topic: Developer guide
description: As seções a seguir fornecem informações de referência para vários recursos da API Sensei Machine Learning.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---


# [!DNL Sensei Machine Learning] Apêndice do guia API

As seções a seguir fornecem informações de referência para vários recursos da API [!DNL Sensei Machine Learning].

## Parâmetros de query para recuperação de ativos {#query}

A API [!DNL Sensei Machine Learning] fornece suporte para parâmetros de query com a recuperação de ativos. Os parâmetros de query disponíveis e seus usos estão descritos na tabela a seguir:

| Parâmetro de consulta | Descrição | Valor padrão |
| --------------- | ----------- | ------- |
| `start` | Indica o índice inicial para paginação. | `start=0` |
| `limit` | Indica o número máximo de resultados a serem retornados. | `limit=25` |
| `orderby` | Indica as propriedades a serem usadas para classificação na ordem de prioridade. Inclua um traço (**-**) antes de um nome de propriedade para classificar em ordem decrescente; caso contrário, os resultados são classificados em ordem crescente. | `orderby=created` |
| `property` | Indica a expressão de comparação que um objeto deve satisfazer para ser retornado. | `property=deleted==false` |

>[!NOTE]
>
>Ao combinar vários parâmetros de query, eles devem ser separados por E comercial (**&amp;**).

## Configurações de CPU Python e GPU {#cpu-gpu-config}

Os mecanismos Python têm a capacidade de escolher entre uma CPU ou uma GPU para seus propósitos de treinamento ou pontuação, e são definidos em uma [MLIntent](./mlinstances.md) como uma especificação de tarefa (`tasks.specification`).

A seguir está um exemplo de configuração que especifica o uso de uma CPU para treinamento e uma GPU para pontuação:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>Os valores de `cpus` e `gpus` não significam o número de CPUs ou GPUs, mas sim o número de máquinas físicas. Esses valores são permitidos `"1"` e, caso contrário, lançarão uma exceção.

## Configurações de recursos PySpark e Spark {#resource-config}

Os mecanismos Spark têm a capacidade de modificar recursos computacionais para fins de treinamento e pontuação. Esses recursos estão descritos na tabela a seguir:

| Recurso | Descrição | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memória para driver em megabytes | int |
| driverCores | Número de núcleos usados pelo driver | int |
| executeMemory | Memória para executor em megabytes | int |
| executorCores | Número de núcleos usados pelo executor | int |
| numExecutors | Número de executores | int |

Os recursos podem ser especificados em [MLIntent](./mlinstances.md) como (A) parâmetros individuais de treinamento ou pontuação, ou (B) em um objeto de especificações adicionais (`specification`). Por exemplo, as seguintes configurações de recursos são as mesmas para treinamento e pontuação:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
