---
keywords: destino de armazenamento na nuvem; armazenamento na nuvem
title: Visão geral dos destinos de armazenamento na nuvem
description: A Adobe Experience Platform pode fornecer seus segmentos como arquivos de dados para seus locais de armazenamento em nuvem Amazon S3, AWS Kinesis, Hubs de eventos do Azure ou SFTP.
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Visão geral dos destinos de armazenamento na nuvem {#cloud-storage-destinations}

A Adobe Experience Platform pode fornecer seus segmentos como arquivos de dados para seus locais de armazenamento na nuvem. Isso permite enviar públicos-alvo e seus atributos de perfil para seus sistemas internos, por meio de CSV ou arquivos delimitados por tabulação para [!DNL Amazon S3], [!DNL Azure Blob] e SFTP. Para destinos [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs], os dados são transmitidos do Experience Platform no formato JSON.

![Destinos de armazenamento na nuvem do Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Para obter informações sobre como se conectar aos destinos de armazenamento em nuvem, consulte [Fluxo de trabalho para criar destinos de armazenamento em nuvem](./workflow.md).

## Tipo de exportação de dados

**Exportação baseada em perfil**  - você está exportando detalhes sobre os indivíduos no público. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de segmentos e muito mais.

## Destinos de armazenamento em nuvem disponíveis

- [Conexão Amazon S3](./amazon-s3.md)
- [Conexão Blob do Azure](./azure-blob.md)
- [Conexão SFTP](./sftp.md)

## Destinos de fluxo de armazenamento em nuvem disponíveis

- [Conexão Amazon Kinesis](./amazon-kinesis.md)
- [Conexão de Hubs de Eventos do Azure](./azure-event-hubs.md)