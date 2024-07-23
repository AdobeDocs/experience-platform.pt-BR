---
title: idMigrationEnabled
description: Permite que o SDK da Web leia cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

A propriedade `idMigrationEnabled` permite que o SDK da Web leia cookies AMCV definidos por implementações anteriores do Adobe Experience Cloud. Se sua organização atualizar sua implementação para o SDK da Web, essa configuração permitirá uma transição mais suave para o serviço atual da Adobe Experience Cloud ID. Essa configuração é importante para que você não veja um aumento acentuado em visitantes únicos ao atualizar para o SDK da Web.

Se sua organização executar uma nova implementação do SDK da Web, habilitar essa configuração não terá impacto na coleta de dados ou na identificação do visitante. Não há desvantagens em deixá-lo ativado para todas as implementações.

## Habilitar a migração de ID usando a extensão de tag SDK da Web

Marque a caixa de seleção **[!UICONTROL Migrar ECID da VisitorAPI para o SDK da Web]** ao [configurar a extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Localize a seção [!UICONTROL Identidade] e marque a caixa de seleção **[!UICONTROL Migrar ECID da VisitorAPI para o SDK da Web]**.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Habilite a migração de ID usando a biblioteca JavaScript do SDK da Web

Defina o booleano `idMigrationEnabled` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK da Web, o padrão será `true`. Defina essa propriedade se desejar desativar a capacidade de ler cookies AMCV definidos pela API do visitante. A maioria das organizações não precisa definir essa propriedade.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
