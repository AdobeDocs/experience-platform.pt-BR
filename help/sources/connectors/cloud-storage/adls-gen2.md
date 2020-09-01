---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Conector Gen2 do Armazenamento Azure Data Lake
topic: overview
description: A documentação abaixo fornece informações sobre como conectar o Armazenamento Gen2 do Azure Data Lake à Plataforma usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Conector Gen2 do Armazenamento Azure Data Lake

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform]e [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamentos na nuvem podem inserir seus próprios dados [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite trazer dados do [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) por lotes.

## LISTA DE PERMISSÕES de endereço IP

Os seguintes endereços IP devem ser adicionados a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes.

### Região Leste dos EUA

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Região da Europa Ocidental

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Austrália Oriental

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Conectar-se [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform] APIs ou à interface do usuário:

### Uso de APIs

- [Criar um conector ADLS-Gen2 usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

## Uso da interface

- [Criar um conector de origem ADLS-Gen2 na interface do usuário](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)