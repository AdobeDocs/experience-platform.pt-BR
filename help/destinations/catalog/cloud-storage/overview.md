---
keywords: destino do armazenamento em nuvem;armazenamento em nuvem
title: Visão geral dos destinos de Armazenamentos na nuvem
description: A Adobe Experience Platform pode fornecer seus segmentos como arquivos de dados para seus locais de armazenamentos em nuvem Amazon S3, AWS Kinesis, Azure Evento Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Visão geral dos destinos de armazenamentos na nuvem {#cloud-storage-destinations}

A Adobe Experience Platform pode fornecer seus segmentos como arquivos de dados para os locais do armazenamento na nuvem. Isso permite que você envie audiências e seus atributos de perfil para seus sistemas internos, via CSV ou arquivos delimitados por tabulação para [!DNL Amazon S3] e SFTP. Para destinos [!DNL AWS Kinesis] e [!DNL Azure Event Hubs], os dados são transmitidos para fora do Experience Platform no formato JSON.

![Destinos do armazenamento na nuvem Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Para obter informações sobre como se conectar aos destinos do armazenamento na nuvem, consulte [Fluxo de trabalho para criar destinos do armazenamento na nuvem](./workflow.md).

## Tipo de exportação de dados

**Exportação**  baseada em perfis - você está exportando detalhes sobre os indivíduos na audiência. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de segmentos etc.

## Destinos de armazenamento na nuvem disponíveis

- [Destino Amazon S3](./amazon-s3.md)
- [Destino Blob do Azure](./azure-blob.md)
- [Destino SFTP](./sftp.md)

## Destinos de streaming de armazenamentos na nuvem disponíveis

- [Destino Amazon Kinesis](./amazon-kinesis.md)
- [Destino dos Hubs de Evento do Azure](./azure-event-hubs.md)