---
title: Recuperando informações da biblioteca
seo-title: Recuperando informações da biblioteca com o SDK da Web do Adobe Experience Platform
description: Saiba como recuperar informações sobre a biblioteca carregada no site
seo-description: Saiba como recuperar informações sobre a biblioteca carregada no site pelo O SDK da Adobe Experience Cloud coleta automaticamente
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Recuperando informações da biblioteca

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Geralmente, é útil acessar alguns detalhes por trás da biblioteca que você carregou em seu site. Para fazer isso, execute o `getLibraryInfo` comando da seguinte maneira:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Atualmente, o objeto fornecido `libraryInfo` contém as seguintes propriedades:

* `version` Esta é a versão da biblioteca carregada. Por exemplo, se a versão da biblioteca que está sendo carregada fosse 1.0.0, o valor seria `1.0.0`.