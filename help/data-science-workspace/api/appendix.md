---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Apêndice
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---


# Apêndice

As seções a seguir fornecem informações de referência para vários recursos da [!DNL Sensei Machine Learning] API.

## Parâmetros de Query para recuperação de ativos {#query}

A [!DNL Sensei Machine Learning] API fornece suporte para parâmetros de query com a recuperação de ativos. Os parâmetros de query disponíveis e seus usos estão descritos na tabela a seguir:

| Parâmetro de consulta | Descrição | Valor padrão |
| --------------- | ----------- | ------- |
| `start` | Indica o índice inicial para paginação. | `start=0` |
| `limit` | Indica o número máximo de resultados a serem retornados. | `limit=25` |
| `orderby` | Indica as propriedades a serem usadas para classificação na ordem de prioridade. Inclua um traço (**-**) antes de um nome de propriedade para classificar em ordem decrescente; caso contrário, os resultados são classificados em ordem crescente. | `orderby=created` |
| `property` | Indica a expressão de comparação que um objeto deve satisfazer para ser retornado. | `property=deleted==false` |

>[!NOTE]
>
>Ao combinar vários parâmetros de query, eles devem ser separados por e-mails (**&amp;**).

## Configurações de CPU Python e GPU {#cpu-gpu-config}

Os mecanismos Python têm a capacidade de escolher entre uma CPU ou uma GPU para seus propósitos de treinamento ou pontuação, e são definidos em uma [MLInposition](./mlinstances.md) como uma especificação de tarefa (`tasks.specification`).

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

Os recursos podem ser especificados em uma instância [MLI](./mlinstances.md) como (A) treinamento individual ou parâmetros de pontuação, ou (B) dentro de um objeto de especificação adicional (`specification`). Por exemplo, as seguintes configurações de recursos são as mesmas para treinamento e pontuação:

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
