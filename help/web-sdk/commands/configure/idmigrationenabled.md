---
title: idMigrationEnabled
description: Permite que o SDK da Web leia cookies AMCV.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

A variável `idMigrationEnabled` permite que o SDK da Web leia cookies AMCV definidos por implementações anteriores do Adobe Experience Cloud. Se sua organização atualizar sua implementação para o SDK da Web, essa configuração permitirá uma transição mais suave para o serviço atual da Adobe Experience Cloud ID. Essa configuração é importante para que você não veja um aumento acentuado em visitantes únicos ao atualizar para o SDK da Web.

Se sua organização executar uma nova implementação do SDK da Web, habilitar essa configuração não terá impacto na coleta de dados ou na identificação do visitante. Não há desvantagens em deixá-lo ativado para todas as implementações.

## Habilitar a migração de ID usando a extensão de tag SDK da Web

Selecione o **[!UICONTROL Migrar ECID da API do visitante para o SDK da Web]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Localize o [!UICONTROL Identidade] e marque a caixa de seleção **[!UICONTROL Migrar ECID da API do visitante para o SDK da Web]**.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Habilite a migração de ID usando a biblioteca JavaScript do SDK da Web

Defina o `idMigrationEnabled` booleano ao executar o `configure` comando. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina essa propriedade se desejar desativar a capacidade de ler cookies AMCV definidos pela API do visitante. A maioria das organizações não precisa definir essa propriedade.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
