---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector HDFS
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Conector HDFS (Beta) [!DNL Apache]

>[!NOTE]
>O conector HDFS Apache está em beta. Consulte a visão geral [das](../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform]e [!DNL Azure], permitindo que você traga seus dados desses sistemas. Os dados ingeridos podem ser formatados como JSON, parquet ou delimitados. O suporte para provedores de armazenamentos em nuvem inclui o [!DNL Apache] HDFS.

## lista de permissões de endereço IP

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

A documentação abaixo fornece informações sobre como conectar o [!DNL Apache] HDFS a [!DNL Platform] APIs ou a interface do usuário:

## Conectar [!DNL Apache] HDFS a [!DNL Platform] APIs

- [Criar um conector HDFS usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

## Conectar [!DNL Apache] HDFS para [!DNL Platform] usar a interface do usuário

- [Criar um conector de origem HDFS Apache na interface do usuário](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)