---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Proteção de dados no Adobe Experience Platform
topic: data protection
description: Todos os dados persistentes no Data Lake são criptografados, armazenados e gerenciados em uma conta isolada do Armazenamento Data Lake do Microsoft Azure que é exclusiva para sua organização. O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, processados, criptografados e persistentes pelo Experience Platform.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Proteção de dados no Adobe Experience Platform

Todos os dados ingeridos e usados pela Adobe Experience Platform são armazenados no [!DNL Data Lake], um armazenamento de dados altamente granular contendo todos os dados gerenciados por [!DNL Platform], independentemente da origem ou do formato de arquivo. Todos os dados persistentes no [!DNL Data Lake] são criptografados, armazenados e gerenciados em uma conta de [!DNL Microsoft Azure Data Lake] Armazenamento isolada exclusiva da sua organização.

O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, processados, criptografados e persistentes por [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Para obter detalhes sobre como os dados em repouso são criptografados em [!DNL Data Lake Storage], consulte o documento sobre criptografia de [dados no Armazenamento](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)Azure Data Lake. Para obter informações sobre como os dados em repouso são criptografados em [!DNL Cosmos DB], consulte o documento sobre criptografia de [dados no Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).