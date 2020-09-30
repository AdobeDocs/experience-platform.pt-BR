---
keywords: Experience Platform;home;popular topics;query service;Query service;create queries;
solution: Experience Platform
title: Criação de query
topic: queries
type: Tutorial
description: Este documento vincula-se à documentação principal usada na criação e compreensão de query no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 3%

---


# Criação de query

A Adobe Experience Platform [!DNL Query Service] fornece o poder de executar query SQL em relação aos conjuntos de dados no [!DNL Data Lake] interior [!DNL Experience Platform]. À medida que você usa o SQL para interagir com conjuntos de dados no Data Lake, é importante entender que ele gerencia [!DNL Query Service] automaticamente certos aspectos, como a criação de nomes de tabela seguros para SQL para cada conjunto de dados no [!DNL Data Lake]. Também há considerações sobre como trabalhar com dados hierárquicos no [!DNL Data Lake], incluindo descobrir o schema no qual um conjunto de dados se baseia e garantir que você esteja selecionando o campo correto no modelo hierárquico.

A documentação a seguir o ajudará a entender melhor os conceitos principais em [!DNL Query Service]:

- [Conjuntos de dados vs tabelas e schemas](./datasets-and-tables.md)
- [Orientação geral para escrever query](./writing-queries.md)
- [Query ExperienceEvent](./experience-event-queries.md)
- [Como participar de conjuntos de dados](./joining-datasets.md)
- [Deduplicação de dados](./deduplication.md)
