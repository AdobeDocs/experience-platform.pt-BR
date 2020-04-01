---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Proteção de dados na plataforma Adobe Experience
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Proteção de dados na plataforma Adobe Experience

Todos os dados ingeridos e usados pela Adobe Experience Platform são armazenados no Data Lake, um armazenamento de dados altamente granular contendo todos os dados gerenciados pela Platform, independentemente da origem ou do formato de arquivo. Todos os dados persistentes no Data Lake são criptografados, armazenados e gerenciados em uma conta isolada do Armazenamento Data Lake do Microsoft Azure que é exclusiva para sua organização.

O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, processados, criptografados e persistentes pela plataforma da experiência:

![](images/data-protection/flow.png)

Para obter detalhes sobre como os dados em repouso são criptografados no Armazenamento Data Lake, consulte o documento sobre criptografia de [dados no Armazenamento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)Azure Data Lake. Para obter informações sobre como os dados em repouso são criptografados no Cosmos DB, consulte o documento sobre criptografia de [dados no Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).