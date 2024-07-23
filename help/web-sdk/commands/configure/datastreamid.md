---
title: datastreamId
description: Determine a ID do fluxo de dados para a qual você deseja enviar dados.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# `datastreamId`

A propriedade `datastreamId` é uma cadeia de caracteres que determina para qual [sequência de dados](../../../datastreams/overview.md) do Adobe Experience Platform você deseja enviar dados. Essa propriedade é necessária ao enviar dados para o Adobe. As versões 2.20.0 ou anteriores do SDK da Web usam `edgeConfigId`.

Para localizar uma ID de sequência de dados:

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Sequências de dados]**.
1. Use o campo de pesquisa para localizar a sequência de dados desejada e selecione **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) ao lado da ID da sequência de dados.

Como alternativa, você pode selecionar o nome do fluxo de dados desejado e a ID do fluxo de dados aparece na coluna à direita para você copiar.

## Selecione a ID da sequência de dados usando a extensão de tag do SDK da Web

Escolha em uma lista de sequências de dados disponíveis ou insira uma ID de sequência de dados diretamente ao [configurar a extensão de marca](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Localize a seção [!UICONTROL Datastreams] e selecione o método desejado para determinar a sequência de dados.
   * Se estiver escolhendo em uma lista, selecione a sandbox e o fluxo de dados de cada lista suspensa.
   * Se estiver inserindo valores, insira a ID do fluxo de dados desejada.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

Você pode enviar dados para diferentes fluxos de dados para ambientes de tag de produção, de preparo e de desenvolvimento.

## Selecione a ID da sequência de dados usando a biblioteca JavaScript do SDK da Web

Defina a propriedade de cadeia de caracteres `datastreamID` ao executar o comando `configure`. Essa propriedade é necessária para todas as implementações do SDK da Web. Se você omitir essa propriedade, o SDK da Web não saberá para qual fluxo de dados enviar dados, causando a perda permanente desses dados.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Se você configurar várias instâncias do SDK da Web em uma única página, deverá configurar um `datastreamId` diferente para cada instância.
