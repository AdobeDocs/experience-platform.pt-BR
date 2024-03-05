---
title: edgeConfigId
description: Determine a ID do fluxo de dados para a qual você deseja enviar dados.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

A variável `edgeConfigId` propriedade é uma string que determina qual [sequência de dados](../../../datastreams/overview.md) no Adobe Experience Platform, você deseja enviar dados para o. Essa propriedade é necessária ao enviar dados para o Adobe.

Para localizar uma ID de sequência de dados:

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Datastreams]**.
1. Use o campo de pesquisa para localizar o fluxo de dados desejado e selecione **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) ao lado da ID do fluxo de dados.

Você também pode selecionar o nome do fluxo de dados desejado e a ID do fluxo de dados aparece na coluna à direita para você copiar.

## Selecione a ID da sequência de dados usando a extensão de tag do SDK da Web

Escolha em uma lista de fluxos de dados disponíveis ou insira uma ID de fluxo de dados diretamente ao [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Localize o [!UICONTROL Datastreams] e selecione o método desejado para determinar o fluxo de dados.
   * Se estiver escolhendo em uma lista, selecione a sandbox e o fluxo de dados de cada lista suspensa.
   * Se estiver inserindo valores, insira a ID do fluxo de dados desejada.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

Você pode enviar dados para diferentes fluxos de dados para ambientes de tag de produção, de preparo e de desenvolvimento.

## Selecione a ID do fluxo de dados usando a biblioteca JavaScript do SDK da Web

Defina o `edgeConfigId` propriedade de string ao executar o `configure` comando. Essa propriedade é necessária para todas as implementações do SDK da Web. Se você omitir essa propriedade, o SDK da Web não saberá para qual fluxo de dados enviar dados, causando a perda permanente desses dados.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Se você configurar várias instâncias do SDK da Web em uma única página, será necessário configurar um SDK diferente `edgeConfigId` para cada instância.
