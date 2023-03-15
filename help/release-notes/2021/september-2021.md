---
title: Notas de versão da Adobe Experience Platform de setembro de 2021
description: As notas de versão de setembro de 2021 para o Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 8%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 29 de setembro de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Assimilação de dados](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Fontes](#sources)

## Assimilação de dados {#ingestion}

A assimilação de dados da Adobe Experience Platform representa os vários métodos pelos quais a Platform assimila dados de várias fontes e também como esses dados são mantidos no Data Lake para uso pelos serviços downstream da plataforma.

**Novos recursos**

| Recurso | Descrição |
|------- | -----------|
| Inserir ou corrigir registros de Perfil usando Assimilação em lote | O Perfil do cliente em tempo real agora permite atualizações em atributos de perfil em dados de registro de perfil individual por meio da assimilação em lote. Para saber mais, consulte o [guia do desenvolvedor de assimilação em lote](../../ingestion/batch-ingestion/api-overview.md). |

Para saber mais sobre a assimilação de dados na Platform, visite o [Documentação de assimilação de dados](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte para fluxos de dados de transmissão | Agora é possível usar as funções de preparação de dados ao criar um fluxo de dados de transmissão para [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], e [!DNL Google PubSub]. Veja o tutorial sobre [criação de um fluxo de dados de transmissão para fontes de armazenamento em nuvem](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) para obter mais informações. |

Para saber mais sobre [!DNL Data Prep] consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| [!DNL Data Landing Zone] | Agora você pode criar um [!DNL Data Landing Zone] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) ou o [interface do usuário](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] é um [!DNL Azure Blob] interface de armazenamento de dados provisionada pela Platform, permitindo que você acesse um recurso de armazenamento de arquivos seguro e baseado em nuvem para trazer arquivos para a Platform. Consulte a [[!DNL Data Landing Zone] visão geral](../../sources/connectors/cloud-storage/data-landing-zone.md) para obter mais informações. |
| [!DNL Snowflake] | Agora você pode criar um [!DNL Snowflake] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) ou o [interface do usuário](../../sources/tutorials/ui/create/databases/snowflake.md) para trazer dados de seu [!DNL Snowflake] banco de dados para a Platform. Consulte a [[!DNL Snowflake] visão geral](../../sources/connectors/databases/snowflake.md) para obter mais informações. |
| [!DNL SFTP] aprimoramentos na origem | Você pode definir manualmente um número de porta personalizado ao criar uma [!DNL SFTP] conexão de origem. Consulte a [[!DNL SFTP] visão geral](../../sources/connectors/cloud-storage/sftp.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
