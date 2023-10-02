---
keywords: destino de armazenamento na nuvem;armazenamento na nuvem
title: Visão geral dos destinos do Cloud Storage
description: A Adobe Experience Platform pode fornecer seus públicos-alvo como arquivos de dados para seus locais de armazenamento na nuvem do Amazon S3, AWS Kinesis, Azure Event Hubs ou SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 4%

---

# Visão geral dos destinos de armazenamento na nuvem {#cloud-storage-destinations}

## Visão geral {#overview}

A Adobe Experience Platform pode fornecer seus públicos-alvo como arquivos de dados para seus locais de armazenamento na nuvem. Isso permite enviar públicos-alvo e seus atributos de perfil para seus sistemas internos, por meio de arquivos CSV para [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage]e SFTP. Para [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs] destinos, os dados são transmitidos do Experience Platform em [!DNL JSON] formato.

![Destinos de armazenamento na nuvem do Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinos de armazenamento na nuvem compatíveis {#supported-destinations}

O Adobe Experience Platform oferece suporte a exportações de dados para os seguintes destinos de armazenamento na nuvem:

* [Conexão com o Amazon Kinesis](amazon-kinesis.md)
* [Conexão com o Amazon S3](amazon-s3.md)
* [Conexão do Blob do Azure](azure-blob.md)
* [Armazenamento Azure Data Lake Gen2](adls-gen2.md)
* [Conexão do Azure Event Hubs](azure-event-hubs.md)
* [Zona de aterrissagem de dados](data-landing-zone.md)
* [Armazenamento em nuvem Google](google-cloud-storage.md)
* [Conexão SFTP](sftp.md)

## Conectar-se a um novo destino de armazenamento na nuvem {#connect-destination}

Para enviar públicos-alvo para destinos de armazenamento na nuvem de suas campanhas, a Platform deve primeiro se conectar ao destino. Consulte a [tutorial de criação do destino](../../ui/connect-destination.md) para obter informações detalhadas sobre como configurar um novo destino.


## Use macros para criar uma pasta no seu local de armazenamento {#use-macros}

>[!NOTE]
>
> A funcionalidade descrita nesta seção está disponível para [Amazon S3](amazon-s3.md) somente destinos.

Para criar uma pasta personalizada por arquivo de público-alvo no local de armazenamento, você pode usar macros no campo de entrada do caminho da pasta. Insira as macros no final do campo de entrada, como mostrado abaixo.

![Como usar macros para criar uma pasta em seu armazenamento](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Os exemplos abaixo fazem referência a um público-alvo de amostra `Luxury Audience` com ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

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

Os destinos de armazenamento na nuvem são compatíveis com os seguintes tipos de exportação:
* **Exportação baseada em perfil**. Isso significa que você está exportando detalhes sobre os indivíduos no público-alvo. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de público-alvo e muito mais.
* **Exportação do conjunto de dados**. Essa funcionalidade permite exportar conjuntos de dados inteiros para destinos de armazenamento na nuvem. [Leia mais](/help/destinations/ui/export-datasets.md) sobre a funcionalidade.

## Próximas etapas {#next-steps}

Depois de selecionar qual dos [destinos na nuvem compatíveis](#supported-destinations) que você deseja usar, leia as [tutorial conectar-se a destinos](/help/destinations/ui/connect-destination.md) para saber como estabelecer uma conexão com o destino. Em seguida, leia o tutorial de ativação nos destinos baseados em arquivo para saber como iniciar [exportação](/help/destinations/ui/activate-batch-profile-destinations.md) para seu destino de armazenamento na nuvem.
