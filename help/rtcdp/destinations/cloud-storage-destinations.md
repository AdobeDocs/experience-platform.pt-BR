---
title: Destinos de armazenamentos na nuvem
seo-title: Destinos de armazenamentos na nuvem
description: A CDP em tempo real do Adobe pode fornecer seus segmentos como arquivos de dados para seus armazenamentos em nuvem Amazon S3, AWS Kinesis, Azure Evento Hubs ou SFTP.
seo-description: A CDP em tempo real do Adobe pode fornecer seus segmentos como arquivos de dados para seus armazenamentos em nuvem Amazon S3, AWS Kinesis, Azure Evento Hubs ou SFTP.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Destinos de armazenamentos na nuvem {#cloud-storage-destinations}

A CDP em tempo real do Adobe pode fornecer seus segmentos como arquivos de dados para os locais do armazenamento na nuvem. Isso permite que você envie audiências e seus atributos de perfil para seus sistemas internos, via CSV ou arquivos delimitados por tabulação para [!DNL Amazon S3] e SFTP. Para [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] destinos, os dados são transmitidos para fora do Experience Platform no formato JSON.

![Destinos de armazenamento da Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Para obter informações sobre como se conectar aos destinos de armazenamentos na nuvem, consulte [Fluxo de trabalho para criar destinos](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)de armazenamentos na nuvem.

## Tipo de exportação de dados

**Exportação** baseada em Perfis - você está exportando detalhes sobre os indivíduos na audiência. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de segmentos etc.

## Destinos de armazenamentos disponíveis na nuvem

* [Destino Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md)
* [Destino SFTP](/help/rtcdp/destinations/sftp-destination.md)

## Destinos de streaming de armazenamentos disponíveis na nuvem

* [Destino Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Destino dos Hubs de Evento do Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)