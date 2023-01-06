---
keywords: Experience Platform, guia do desenvolvedor, endpoint, Data Science Workspace, tópicos populares;
solution: Experience Platform
title: Apêndice do Guia da API do Sensei Machine Learning
description: As seções a seguir fornecem informações de referência para vários recursos da API Sensei Machine Learning.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] Apêndice do guia de API

As seções a seguir fornecem informações de referência para vários recursos do [!DNL Sensei Machine Learning] API.

## Parâmetros de consulta para recuperação de ativos {#query}

O [!DNL Sensei Machine Learning] A API fornece suporte para parâmetros de consulta com a recuperação de ativos. Os parâmetros de consulta disponíveis e seus usos estão descritos na tabela a seguir:

| Parâmetro de consulta | Descrição | Valor padrão |
| --------------- | ----------- | ------- |
| `start` | Indica o índice inicial para paginação. | `start=0` |
| `limit` | Indica o número máximo de resultados a serem retornados. | `limit=25` |
| `orderby` | Indica as propriedades a serem usadas para classificação em ordem de prioridade. Incluir um traço (**-**) antes de um nome de propriedade para classificar em ordem decrescente, caso contrário, os resultados são classificados em ordem crescente. | `orderby=created` |
| `property` | Indica a expressão de comparação que um objeto deve atender para ser retornado. | `property=deleted==false` |

>[!NOTE]
>
>Ao combinar vários parâmetros de consulta, eles devem ser separados por &quot;E&quot; comercial (**&amp;**).

## Configurações de CPU Python e GPU {#cpu-gpu-config}

Os mecanismos Python têm a capacidade de escolher entre uma CPU ou uma GPU para seus propósitos de treinamento ou pontuação, e são definidos em um [InstânciaMLI](./mlinstances.md) como uma especificação de tarefa (`tasks.specification`).

A seguir, um exemplo de configuração que especifica o uso de uma CPU para treinamento e uma GPU para pontuação:

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
>Os valores de `cpus` e `gpus` O não significa o número de CPUs ou GPUs, mas sim o número de máquinas físicas. Esses valores são permitidos `"1"` e lançará uma exceção de outra forma.

## Configurações de recursos PySpark e Spark {#resource-config}

Os Mecanismos Spark têm a capacidade de modificar recursos tecnológicos para fins de treinamento e pontuação. Esses recursos estão descritos na tabela a seguir:

| Recurso | Descrição | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memória para driver em megabytes | int |
| driverCores | Número de núcleos usados pelo driver | int |
| executorMemory | Memória para executor em megabytes | int |
| executorCores | Número de núcleos usados pelo executor | int |
| numExecutors | Número de executores | int |

Os recursos podem ser especificados em um [InstânciaMLI](./mlinstances.md) como (A) treinamento individual ou parâmetros de pontuação, ou (B) dentro de um objeto de especificações adicionais (`specification`). Por exemplo, as seguintes configurações de recursos são as mesmas para treinamento e pontuação:

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
