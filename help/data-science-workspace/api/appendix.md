---
keywords: Experience Platform;guia do desenvolvedor;endpoint;Data Science Workspace;tópicos populares;
solution: Experience Platform
title: Apêndice do Guia da API de Aprendizado de Máquina do Sensei
description: As seções a seguir fornecem informações de referência para vários recursos da API do Sensei Machine Learning.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# Apêndice do guia de API [!DNL Sensei Machine Learning]

As seções a seguir fornecem informações de referência para vários recursos da API [!DNL Sensei Machine Learning].

## Parâmetros de consulta para recuperação de ativos {#query}

A API [!DNL Sensei Machine Learning] fornece suporte para parâmetros de consulta com a recuperação de ativos. Os parâmetros de query disponíveis e seus usos são descritos na tabela a seguir:

| Parâmetro de consulta | Descrição | Valor padrão |
| --------------- | ----------- | ------- |
| `start` | Indica o índice inicial para paginação. | `start=0` |
| `limit` | Indica o número máximo de resultados a serem retornados. | `limit=25` |
| `orderby` | Indica as propriedades a serem usadas para classificar em ordem de prioridade. Inclua um traço (**-**) antes do nome de uma propriedade para classificar em ordem decrescente, caso contrário, os resultados serão classificados em ordem crescente. | `orderby=created` |
| `property` | Indica a expressão de comparação que um objeto deve satisfazer para ser retornado. | `property=deleted==false` |

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados por &quot;E&quot; comercial (**&amp;**).

## Configurações de CPU e GPU Python {#cpu-gpu-config}

Os Mecanismos Python podem escolher entre uma CPU ou uma GPU para fins de treinamento ou pontuação e são definidos em uma [MLInstance](./mlinstances.md) como uma especificação de tarefa (`tasks.specification`).

Este é um exemplo de configuração que especifica o uso de uma CPU para treinamento e de uma GPU para pontuação:

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
>Os valores de `cpus` e `gpus` não significam o número de CPUs ou GPUs, mas sim o número de máquinas físicas. Esses valores são permitidos `"1"` e lançarão uma exceção caso contrário.

## Configurações de recursos do PySpark e do Spark {#resource-config}

Os Spark Engines têm a capacidade de modificar recursos computacionais para fins de treinamento e pontuação. Esses recursos são descritos na tabela a seguir:

| Recurso | Descrição | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memória do driver em megabytes | int |
| driverCores | Número de núcleos usados pelo driver | int |
| executorMemory | Memória do executor em megabytes | int |
| executorCores | Número de núcleos usados pelo executor | int |
| numExecutors | Número de executores | int |

Os recursos podem ser especificados em uma [MLInstance](./mlinstances.md) como (A) treinamento individual ou parâmetros de pontuação, ou (B) dentro de um objeto de especificações adicionais (`specification`). Por exemplo, as configurações de recursos a seguir são as mesmas para treinamento e pontuação:

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
