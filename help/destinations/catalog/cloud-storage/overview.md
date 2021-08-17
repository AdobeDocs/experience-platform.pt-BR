---
keywords: destino de armazenamento na nuvem; armazenamento na nuvem
title: Visão geral dos destinos de armazenamento na nuvem
description: A Adobe Experience Platform pode fornecer seus segmentos como arquivos de dados para seus locais de armazenamento em nuvem Amazon S3, AWS Kinesis, Hubs de eventos do Azure ou SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Visão geral dos destinos de armazenamento na nuvem {#cloud-storage-destinations}

## Visão geral {#overview}

A Adobe Experience Platform pode fornecer seus segmentos como arquivos de dados para seus locais de armazenamento na nuvem. Isso permite enviar públicos-alvo e seus atributos de perfil para seus sistemas internos, por meio de CSV ou arquivos delimitados por tabulação para [!DNL Amazon S3], [!DNL Azure Blob] e SFTP. Para destinos [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs], os dados são transmitidos do Experience Platform no formato [!DNL JSON].

![Destinos de armazenamento na nuvem do Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinos de armazenamento em nuvem suportados {#supported-destinations}

O Adobe Experience Platform é compatível com os seguintes destinos de armazenamento em nuvem:

* [Conexão Amazon Kinesis](amazon-kinesis.md)
* [Conexão Amazon S3](amazon-s3.md)
* [Conexão Blob do Azure](azure-blob.md)
* [Conexão de Hubs de Eventos do Azure](azure-event-hubs.md)
* [Conexão SFTP](sftp.md)

## Conectar-se a um novo destino de armazenamento em nuvem {#connect-destination}

Para enviar segmentos para destinos de armazenamento em nuvem para suas campanhas, a Platform deve primeiro se conectar ao destino. Consulte o [tutorial de criação de destino](../../ui/connect-destination.md) para obter informações detalhadas sobre como configurar um novo destino.


## Usar macros para criar uma pasta no local de armazenamento {#use-macros}

>[!NOTE]
>
> A funcionalidade descrita nesta seção está disponível somente para destinos [Amazon S3](amazon-s3.md).

Para criar uma pasta personalizada por arquivo de segmento no local de armazenamento, você pode usar macros no campo de entrada do caminho da pasta. Insira as macros no final do campo de entrada, conforme mostrado abaixo.

![Como usar macros para criar uma pasta no seu armazenamento](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Os exemplos abaixo fazem referência a um segmento de amostra `Luxury Audience` com ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%`
Caminho da pasta no local de armazenamento: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_ID%`
Caminho da pasta no local de armazenamento: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Caminho da pasta no local de armazenamento: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Tipo de exportação de dados {#export-type}

Os destinos de armazenamento em nuvem oferecem suporte para **Exportação baseada em perfil**. Isso significa que você está exportando detalhes sobre os indivíduos no público-alvo. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de segmentos e muito mais.