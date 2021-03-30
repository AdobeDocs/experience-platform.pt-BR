---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform para 31 de março de 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 9%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 31 de março de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

As seguintes atualizações de fontes estão incluídas na versão de março de 2021 do Experience Platform:

| Recurso | Descrição |
| ------- | ----------- |
| Fontes beta movendo-se para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Suporte a API para assimilação de arquivo compactado | Agora você pode visualizar e assimilar arquivos compactados JSON ou delimitados usando fontes de armazenamento em nuvem. Para obter mais informações, consulte o tutorial em [coletar dados de armazenamento em nuvem usando APIs](../../sources/tutorials/api/collect/cloud-storage.md). |
| Suporte à interface do usuário para upload de arquivo recursivo | Agora é possível assimilar pastas inteiras recursivamente ao usar uma fonte de armazenamento em nuvem. Ao assimilar uma pasta inteira, você deve garantir que seu conteúdo compartilhe o mesmo schema. Para obter mais informações, consulte o tutorial em [configurar um fluxo de dados para conectores de armazenamento em nuvem na interface do usuário](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
