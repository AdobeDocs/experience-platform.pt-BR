---
title: idMigrationEnabled
description: Permite que o Web SDK leia cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

A propriedade `idMigrationEnabled` permite que o Web SDK leia cookies AMCV definidos por implementações anteriores do Adobe Experience Cloud. Se sua organização atualizar sua implementação para o Web SDK, essa configuração permitirá uma transição mais suave para o serviço atual da Adobe Experience Cloud ID. Essa configuração é importante para que você não veja um aumento acentuado em visitantes únicos ao atualizar para o Web SDK.

Se sua organização executar uma nova implementação do Web SDK, ativar essa configuração não terá impacto na coleta de dados ou na identificação do visitante. Não há desvantagens em deixá-lo ativado para todas as implementações.

Defina o booleano `idMigrationEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o Web SDK, o padrão será `true`. Defina essa propriedade se desejar desativar a capacidade de ler cookies AMCV definidos pela API do visitante. A maioria das organizações não precisa definir essa propriedade.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Habilitar a migração de ID de visitante usando a extensão de tag da Web SDK

Essas configurações podem ser definidas na extensão de marca do Web SDK usando [configurações de identidade](/help/tags/extensions/client/web-sdk/configure/identity.md).
