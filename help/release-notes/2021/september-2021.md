---
title: Notas de versão da Adobe Experience Platform de setembro de 2021
description: As notas de versão de setembro de 2021 para o Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 26%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 29 de setembro de 2021**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [Assimilação de dados](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Origens](#sources)

## Assimilação de dados {#ingestion}

A assimilação de dados da Adobe Experience Platform representa os vários métodos pelos quais a Platform assimila dados de várias fontes e também como esses dados são mantidos no Data Lake para uso pelos serviços downstream da plataforma.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Inserir ou corrigir registros de Perfil usando Assimilação em lote | O Perfil do cliente em tempo real agora permite atualizações em atributos de perfil em dados de registro de perfil individual por meio da assimilação em lote. Para saber mais, consulte o [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md). |

Para saber mais sobre assimilação de dados na Platform, visite a [documentação de Assimilação de dados](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte para fluxos de dados de transmissão | Agora você pode usar as funções de preparação de dados ao criar um fluxo de dados de streaming para [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] e [!DNL Google PubSub]. Consulte o tutorial sobre [criação de um fluxo de dados de transmissão para fontes de armazenamento na nuvem](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) para obter mais informações. |

Para saber mais sobre [!DNL Data Prep], consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| [!DNL Data Landing Zone] | Agora você pode criar uma conexão de origem [!DNL Data Landing Zone] usando a [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) ou a [interface de usuário](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). O [!DNL Data Landing Zone] é uma interface de armazenamento do [!DNL Azure Blob] provisionada pela Platform, que concede a você acesso a um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Platform. Consulte a [[!DNL Data Landing Zone] visão geral](../../sources/connectors/cloud-storage/data-landing-zone.md) para obter mais informações. |
| [!DNL Snowflake] | Agora você pode criar uma conexão de origem [!DNL Snowflake] usando a [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) ou a [interface do usuário](../../sources/tutorials/ui/create/databases/snowflake.md) para trazer dados do banco de dados [!DNL Snowflake] para a Platform. Consulte a [[!DNL Snowflake] visão geral](../../sources/connectors/databases/snowflake.md) para obter mais informações. |
| [!DNL SFTP] aprimoramentos na origem | Você pode definir manualmente um número de porta personalizado ao criar uma conexão de origem [!DNL SFTP]. Consulte a [[!DNL SFTP] visão geral](../../sources/connectors/cloud-storage/sftp.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
