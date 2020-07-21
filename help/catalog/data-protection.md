---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Proteção de dados no Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Proteção de dados no Adobe Experience Platform

Todos os dados ingeridos e usados pelo Adobe Experience Platform são armazenados no [!DNL Data Lake], um armazenamento de dados altamente granular contendo todos os dados gerenciados por [!DNL Platform], independentemente da origem ou do formato de arquivo. Todos os dados persistentes no [!DNL Data Lake] são criptografados, armazenados e gerenciados em uma conta de [!DNL Microsoft Azure Data Lake] Armazenamento isolada exclusiva da sua organização.

O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, processados, criptografados e persistentes por [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Para obter detalhes sobre como os dados em repouso são criptografados em [!DNL Data Lake Storage], consulte o documento sobre criptografia de [dados no Armazenamento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)Azure Data Lake. Para obter informações sobre como os dados em repouso são criptografados em [!DNL Cosmos DB], consulte o documento sobre criptografia de [dados no Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).