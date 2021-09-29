---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 4959b5227f777a2c8cab1317d67795678d1a6eea
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 11%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de setembro de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Assimilação de dados](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Fontes](#sources)

## Assimilação de dados {#ingestion}

A Assimilação de dados da Adobe Experience Platform representa os vários métodos pelos quais a Platform assimila dados de várias fontes, bem como como esses dados são mantidos no Data Lake para uso pelos serviços downstream da plataforma.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Atualizar ou corrigir registros de Perfil usando a assimilação em lote | O Perfil do cliente em tempo real agora permite atualizações para atributos de perfil em dados de registro de perfil individuais por meio da assimilação em lote. Para saber mais, consulte o [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md). |

Para saber mais sobre como assimilar dados na Platform, visite a [Documentação de assimilação de dados](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte para fluxos de dados de transmissão | Agora você pode usar funções de preparação de dados ao criar um fluxo de dados para [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] e [!DNL Google PubSub]. Consulte o tutorial em [criar um fluxo de dados de fluxo para fontes de armazenamento em nuvem](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) para obter mais informações. |

Para saber mais sobre [!DNL Data Prep] consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| [!DNL Data Landing Zone] | Agora você pode criar uma conexão de origem [!DNL Data Landing Zone] usando a [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) ou a [interface do usuário](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] O é uma interface  [!DNL Azure Blob] de armazenamento provisionada pela Platform, permitindo acessar uma instalação segura de armazenamento de arquivos baseada em nuvem para assimilar e retirar arquivos da Platform. Consulte a [[!DNL Data Landing Zone] visão geral](../../sources/connectors/cloud-storage/data-landing-zone.md) para obter mais informações. |
| [!DNL Snowflake] | Agora você pode criar uma conexão de origem [!DNL Snowflake] usando a [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) ou a [interface do usuário](../../sources/tutorials/ui/create/databases/snowflake.md) para trazer dados do seu banco de dados [!DNL Snowflake] para a Plataforma. Consulte a [[!DNL Snowflake] visão geral](../../sources/connectors/databases/snowflake.md) para obter mais informações. |
| [!DNL SFTP] melhorias na fonte | Você pode definir manualmente um número de porta personalizado ao criar uma conexão de origem [!DNL SFTP]. Consulte a [[!DNL SFTP] visão geral](../../sources/connectors/cloud-storage/sftp.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
