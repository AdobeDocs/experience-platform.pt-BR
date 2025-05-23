---
title: Exportar dados para ambientes externos de ML
description: Saiba como compartilhar um conjunto de dados de treinamento preparado, criado com o Data Distiller, em um local de armazenamento em nuvem que seu ambiente de aprendizado de máquina possa ler para treinamento e pontuação de seu modelo.
exl-id: 75022acf-fafd-41d6-8dfa-ff3fd4c4fa7e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 5%

---

# Exportar dados para ambientes externos de ML

Este documento demonstra como compartilhar um conjunto de dados de treinamento preparado criado com o Data Distiller em um local de armazenamento na nuvem que seu ambiente de aprendizado de máquina pode ler para treinamento e pontuação em seu modelo. O exemplo aqui exporta o conjunto de dados de treinamento para a [Data Landing Zone (DLZ)](../../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). Você pode alterar o destino de armazenamento conforme necessário para trabalhar com seu ambiente de aprendizado de máquina.

O [Serviço de Fluxo para Destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/) é usado para concluir o pipeline de recursos, colocando um conjunto de dados de recursos computados em um local de armazenamento na nuvem apropriado.

## Criar a conexão de origem {#create-source-connection}

A conexão de origem é responsável por configurar a conexão com seu conjunto de dados do Adobe Experience Platform para que o fluxo resultante saiba exatamente onde procurar os dados e em que formato.

```python
from aepp import flowservice
flow_conn = flowservice.FlowService()

training_dataset_id = <YOUR_TRAINING_DATASET_ID>

source_res = flow_conn.createSourceConnectionDataLake(
    name=f"[CMLE] Featurized Dataset source connection created by {username}",
    dataset_ids=[training_dataset_id],
    format="parquet"
)
source_connection_id = source_res["id"]
```

## Criar a conexão de destino {#create-target-connection}

A conexão de destino é responsável pela conexão com o sistema de arquivos de destino. Isso requer primeiro a criação de uma conexão básica com a conta de armazenamento na nuvem (a Data Landing Zone neste exemplo) e, em seguida, uma conexão de destino com um caminho de arquivo específico com opções de compactação e formato especificadas.

Os destinos de armazenamento em nuvem disponíveis são identificados por uma ID de especificação de conexão:

| Tipo de armazenamento na nuvem | ID de especificação da conexão |
|-----------------------|--------------------------------------|
| Amazon S3 | 4fce964d-3f37-408f-9778-e597338a21ee |
| Armazenamento Azure Blob | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |
| Azure Data Lake | be2c3209-53bc-47e7-ab25-145db8b873e1 |
| Data Landing Zone | 10440537-2a7b-4583-ac39-ed38d4b848e8 |
| Google Cloud Storage | c5d93acb-ea8b-4b14-8f53-02138444ae99 |
| SFTP | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

```python
connection_spec_id = "10440537-2a7b-4583-ac39-ed38d4b848e8"
base_connection_res = flow_conn.createConnection(data={
    "name": "Base Connection to DLZ created by",
    "auth": None,
    "connectionSpec": {
        "id": connection_spec_id,
        "version": "1.0"
    }
})
base_connection_id = base_connection_res["id"]

target_res = flow_conn.createTargetConnection(
    data={
        "name": "Data Landing Zone target connection",
        "baseConnectionId": base_connection_id,
        "params": {
            "mode": "Server-to-server",
            "compression": config.get("Cloud", "compression_type"),
            "datasetFileType": config.get("Cloud", "data_format"),
            "path": config.get("Cloud", "export_path")
        },
        "connectionSpec": {
            "id": connection_spec_id,
            "version": "1.0"
        }
    }
)
target_connection_id = target_res["id"]
```

## Criar o fluxo de dados {#create-data-flow}

A etapa final é criar um fluxo de dados entre o conjunto de dados especificado na conexão de origem e o caminho do arquivo de destino especificado na conexão de destino.

Cada tipo de armazenamento na nuvem disponível é identificado por uma ID de especificação de fluxo:

| Tipo de armazenamento na nuvem | ID da especificação de fluxo |
|-----------------------|--------------------------------------|
| Amazon S3 | 269ba276-16fc-47db-92b0-c1049a3c131f |
| Armazenamento Azure Blob | 95bd8965-fc8a-4119-b9c3-944c2c2df6d2 |
| Azure Data Lake | 17be2013-2549-41ce-96e7-a70363bec293 |
| Data Landing Zone | cd2fc47e-e838-4f38-a581-8fff2f99b63a |
| Google Cloud Storage | 585c15c4-6cbf-4126-8f87-e26bff78b657 |
| SFTP | 354d6aad-4754-46e4-a576-1b384561c440 |

O código a seguir cria um fluxo de dados com uma programação definida para iniciar no futuro. Isso permite acionar fluxos ad hoc durante o desenvolvimento do modelo. Depois de ter um modelo treinado, você pode atualizar o agendamento do fluxo de dados para compartilhar o conjunto de dados do recurso no agendamento desejado.

```python
import time

on_schedule = False
if on_schedule:
    schedule_params = {
        "interval": 3,
        "timeUnit": "hour",
        "startTime": int(time.time())
    }
else:
    schedule_params = {
        "interval": 1,
        "timeUnit": "day",
        "startTime": int(time.time() + 60*60*24*365) # Start the schedule far in the future
    }

flow_spec_id = "cd2fc47e-e838-4f38-a581-8fff2f99b63a"
flow_obj = {
    "name": "Flow for Feature Dataset to DLZ",
    "flowSpec": {
        "id": flow_spec_id,
        "version": "1.0"
    },
    "sourceConnectionIds": [
        source_connection_id
    ],
    "targetConnectionIds": [
        target_connection_id
    ],
    "transformations": [],
    "scheduleParams": schedule_params
}
flow_res = flow_conn.createFlow(
    obj = flow_obj,
    flow_spec_id = flow_spec_id
)
dataflow_id = flow_res["id"]
```

Com o fluxo de dados criado, agora é possível acionar uma execução de fluxo ad hoc para compartilhar o conjunto de dados do recurso sob demanda:

```python
from aepp import connector

connector = connector.AdobeRequest(
  config_object=aepp.config.config_object,
  header=aepp.config.header,
  loggingEnabled=False,
  logger=None,
)

endpoint = aepp.config.endpoints["global"] + "/data/core/activation/disflowprovider/adhocrun"

payload = {
    "activationInfo": {
        "destinations": [
            {
                "flowId": dataflow_id, 
                "datasets": [
                    {"id": created_dataset_id}
                ]
            }
        ]
    }
}

connector.header.update({"Accept":"application/vnd.adobe.adhoc.dataset.activation+json; version=1"})
activation_res = connector.postData(endpoint=endpoint, data=payload)
activation_res
```

## Compartilhamento simplificado na Data Landing Zone

Para compartilhar um conjunto de dados com a Data Landing Zone mais facilmente, a biblioteca `aepp` fornece uma função `exportDatasetToDataLandingZone` que executa as etapas acima em uma única chamada de função:

```python
from aepp import exportDatasetToDataLandingZone

export = exportDatasetToDataLandingZone.ExportDatasetToDataLandingZone()

dataflow_id = export.createDataFlowRunIfNotExists(
    dataset_id = created_dataset_id,
    data_format = data_format, 
    export_path= export_path, 
    compression_type = compression_type, 
    on_schedule = False, 
    config_path = config_path, 
    entity_name = "Flow for Featurized Dataset to DLZ"
)
```

Esse código cria a conexão de origem, a conexão de destino e o fluxo de dados com base nos parâmetros fornecidos, e executa uma execução ad hoc do fluxo de dados em uma única etapa.
