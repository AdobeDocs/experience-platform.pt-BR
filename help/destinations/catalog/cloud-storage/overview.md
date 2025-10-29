---
keywords: destino de armazenamento na nuvem;armazenamento na nuvem
title: Visão geral dos destinos do Cloud Storage
description: A Adobe Experience Platform pode fornecer seus públicos-alvo como arquivos de dados para seus locais de armazenamento na nuvem Amazon S3, AWS Kinesis, Azure Event Hubs ou SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 5%

---

# Visão geral dos destinos de armazenamento na nuvem {#cloud-storage-destinations}

## Visão geral {#overview}

A Adobe Experience Platform pode fornecer seus públicos-alvo como arquivos de dados para seus locais de armazenamento na nuvem. Isso permite que você envie públicos-alvo e seus atributos de perfil para seus sistemas internos, por meio de arquivos CSV para [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] e SFTP. Para os destinos [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs], os dados são transmitidos pelo Experience Platform no formato [!DNL JSON].

![Destinos de armazenamento na nuvem do Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinos de armazenamento na nuvem compatíveis {#supported-destinations}

O Adobe Experience Platform oferece suporte a exportações de dados para os seguintes destinos de armazenamento na nuvem:

* [Conexão Amazon Kinesis](amazon-kinesis.md)
* [Conexão com o Amazon S3](amazon-s3.md)
* [Conexão do Blob do Azure](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Conexão do Azure Event Hubs](azure-event-hubs.md)
* [Data Landing Zone](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [Conexão SFTP](sftp.md)

## Conectar-se a um novo destino de armazenamento na nuvem {#connect-destination}

Para enviar públicos-alvo para destinos de armazenamento na nuvem de suas campanhas, o Experience Platform deve primeiro se conectar ao destino. Consulte o [tutorial de criação de destino](../../ui/connect-destination.md) para obter informações detalhadas sobre a configuração de um novo destino.


## Use macros para criar uma pasta no seu local de armazenamento {#use-macros}

>[!NOTE]
>
> A funcionalidade descrita nesta seção está disponível para todos os destinos de armazenamento na nuvem. No entanto, o destino [Amazon S3](amazon-s3.md) só oferece suporte atualmente às macros `%SEGMENT_ID%` e `%SEGMENT_NAME%`.

Para criar uma pasta personalizada por arquivo de público-alvo no local de armazenamento, você pode usar macros no campo de entrada do caminho da pasta. Insira as macros no final do campo de entrada, como mostrado abaixo.

![Como usar macros para criar uma pasta em seu armazenamento](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Os exemplos abaixo fazem referência a um público-alvo de exemplo `Luxury Audience` com ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%`
Caminho da pasta no local de armazenamento: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_ID%`
Caminho da pasta no local de armazenamento: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Caminho da pasta no local de armazenamento: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**Mais macros**

Semelhante aos exemplos acima, você pode usar mais macros para criar uma estrutura de pastas personalizada no local da pasta:

* `%DATETIME%` ou `%TIMESTAMP%` para adicionar um nome de pasta personalizado com base no tempo de exportação dos arquivos. O formato da primeira macro é `MMDDYYYY_HHMMSS` e um formato UNIX de 10 dígitos para a segunda macro.
* `%DESTINATION_NAME%` para adicionar uma pasta personalizada com base no nome do fluxo de dados de destino.

## Tipo de exportação de dados {#export-type}

Os destinos de armazenamento na nuvem são compatíveis com os seguintes tipos de exportação:

* **Exportação baseada em perfil**. Isso significa que você está exportando detalhes sobre os indivíduos no público-alvo. Esses detalhes são necessários para personalização e podem incluir atributos, eventos, associações de público-alvo e muito mais.
* **Exportação do conjunto de dados**. Essa funcionalidade permite exportar conjuntos de dados inteiros para destinos de armazenamento na nuvem. [Leia mais](/help/destinations/ui/export-datasets.md) sobre a funcionalidade.

## Próximas etapas {#next-steps}

Depois de selecionar qual dos [destinos na nuvem com suporte](#supported-destinations) você deseja usar, leia o [tutorial sobre conexão com destinos](/help/destinations/ui/connect-destination.md) para saber como estabelecer uma conexão com o destino. Em seguida, leia o tutorial de ativação para destinos baseados em arquivo para saber como iniciar a [exportação](/help/destinations/ui/activate-batch-profile-destinations.md) de dados para o seu destino de armazenamento na nuvem.
