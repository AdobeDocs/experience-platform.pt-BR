---
title: Recuperando informações da biblioteca
seo-title: Recuperando informações da biblioteca com o Adobe Experience Platform Web SDK
description: Saiba como recuperar informações sobre a biblioteca carregada no site
seo-description: Saiba como recuperar informações sobre a biblioteca carregada no site pelo O SDK da Adobe Experience Cloud coleta automaticamente
keywords: library; library information;getLibraryInfo;libraryInfo;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Recuperando informações da biblioteca

Geralmente, é útil acessar alguns detalhes por trás da biblioteca que você carregou em seu site. Para fazer isso, execute o `getLibraryInfo` comando da seguinte maneira:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Atualmente, o objeto fornecido `libraryInfo` contém as seguintes propriedades:

* `version` Esta é a versão da biblioteca carregada. Por exemplo, se a versão da biblioteca que está sendo carregada fosse 1.0.0, o valor seria `1.0.0`.