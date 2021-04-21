---
keywords: Experience Platform, home, tópicos populares, catálogo, proteção de dados, criptografar data lake
solution: Experience Platform
title: Proteção de dados no Adobe Experience Platform
topic-legacy: data protection
description: Todos os dados persistentes no Data Lake são criptografados, armazenados e gerenciados em uma conta isolada do Armazenamento Data Lake do Microsoft Azure exclusiva para sua organização. O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, processados, criptografados e persistentes pelo Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Proteção de dados no Adobe Experience Platform

Todos os dados assimilados e usados pelo Adobe Experience Platform são armazenados no [!DNL Data Lake], um armazenamento de dados altamente granular que contém todos os dados gerenciados por [!DNL Platform], independentemente da origem ou do formato de arquivo. Todos os dados persistentes em [!DNL Data Lake] são criptografados, armazenados e gerenciados em uma conta de armazenamento [!DNL Microsoft Azure Data Lake] isolada exclusiva à sua organização.

O diagrama de fluxo de processo a seguir ilustra como os dados são assimilados, processados, criptografados e mantidos por [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Para obter detalhes sobre como os dados em repouso são criptografados em [!DNL Data Lake Storage], consulte o documento em [criptografia de dados no Armazenamento Azure Data Lake](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Para obter informações sobre como os dados em repouso são criptografados em [!DNL Cosmos DB], consulte o documento em [criptografia de dados no Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).
