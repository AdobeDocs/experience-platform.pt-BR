---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Como participar de conjuntos de dados
topic: queries
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 3%

---


# Como participar de conjuntos de dados

Ingressar em conjuntos de dados permite incluir dados de outros conjuntos de dados em seu query. Este exemplo usa um conjunto de dados de sistema operacional personalizado para mapear o `operatingsystemID` para o `operatingsystem` valor.

Conjuntos de dados:
- your_analytics_table
- custom_operating_system_lookup

Crie uma `SELECT` declaração para os 50 principais sistemas operacionais por número de visualizações de página.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Imagem](../images/queries/joining-datasets/select-operating-systems.png)