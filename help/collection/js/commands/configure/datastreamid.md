---
title: datastreamId
description: Determine a ID do fluxo de dados para a qual você deseja enviar dados.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# `datastreamId`

A propriedade `datastreamId` é uma cadeia de caracteres que determina para qual [sequência de dados](/help/datastreams/overview.md) do Adobe Experience Platform você deseja enviar dados. Essa propriedade é necessária ao enviar dados para a Adobe. As versões 2.20.0 ou anteriores do Web SDK usam `edgeConfigId`.

Para localizar uma ID de sequência de dados:

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Use o campo de pesquisa para localizar a sequência de dados desejada e selecione **[!UICONTROL Copy]** ![Copiar](../../assets/copy.png) ao lado da ID da sequência de dados.

Como alternativa, você pode selecionar o nome do fluxo de dados desejado e a ID do fluxo de dados aparece na coluna à direita para você copiar.

## Exemplo de código

Defina a propriedade de cadeia de caracteres `datastreamID` ao executar o comando `configure`. Essa propriedade é necessária para todas as implementações do Web SDK. Se você omitir essa propriedade, o Web SDK não saberá para qual fluxo de dados enviar dados, causando a perda permanente desses dados.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Se você configurar várias instâncias do Web SDK em uma única página, deverá configurar um `datastreamId` diferente para cada instância.

## Selecione a ID do fluxo de dados usando a extensão de tag do Web SDK

Consulte [Configurações da sequência de dados](/help/tags/extensions/client/web-sdk/configure/datastreams.md) na documentação da extensão de tag do Web SDK para saber como definir a sequência de dados desejada para cada ambiente usando tags. Você pode enviar dados para diferentes fluxos de dados para ambientes de tag de produção, de preparo e de desenvolvimento.
