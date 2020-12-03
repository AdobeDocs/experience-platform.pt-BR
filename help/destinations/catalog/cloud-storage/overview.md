---
keywords: cloud storage destination;cloud storage
title: Destinos de armazenamentos na nuvem
seo-title: Destinos de armazenamentos na nuvem
description: A CDP em tempo real pode fornecer seus segmentos como arquivos de dados para os locais dos armazenamentos em nuvem do Amazon S3, AWS Kinesis, Azure Evento Hubs ou SFTP.
seo-description: A CDP em tempo real pode fornecer seus segmentos como arquivos de dados para os locais dos armazenamentos em nuvem do Amazon S3, AWS Kinesis, Azure Evento Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Destinos de armazenamentos na nuvem {#cloud-storage-destinations}

A CDP em tempo real pode fornecer seus segmentos como arquivos de dados para os locais do armazenamento na nuvem. Isso permite que você envie audiências e seus atributos de perfil para seus sistemas internos, via CSV ou arquivos delimitados por tabulação para [!DNL Amazon S3] e SFTP. Para [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] destinos, os dados são transmitidos para fora do Experience Platform no formato JSON.

![Destinos de armazenamento da Adobe Cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Para obter informações sobre como se conectar aos destinos de armazenamentos na nuvem, consulte [Fluxo de trabalho para criar destinos](./workflow.md)de armazenamentos na nuvem.

## Tipo de exportação de dados

**Exportação** baseada em perfis - você está exportando detalhes sobre os indivíduos na audiência. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de segmentos etc.

## Destinos de armazenamentos disponíveis na nuvem

- [Destino Amazon S3](./amazon-s3.md)
- [Destino SFTP](./sftp.md)

## Destinos de streaming de armazenamentos disponíveis na nuvem

- [Destino Amazon Kinesis](./amazon-kinesis.md)
- [Destino dos Hubs de Evento do Azure](./azure-event-hubs.md)