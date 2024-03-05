---
title: dados
description: Saiba como enviar dados não XDM para o Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# dados

A variável `data` permite enviar dados para o Adobe que não corresponde a um esquema XDM. É útil em cenários que não sejam XDM, como atualizar uma [Perfil do Adobe Target](/help/web-sdk/personalization/adobe-target/target-overview.md). Quando os dados chegarem ao Adobe, você poderá usar a ferramenta de mapeamento de fluxo de dados para atribuir campos XDM a cada campo no `data` propriedade.

>[!IMPORTANT]
>
>Os dados nessa propriedade devem ter pelo menos uma das seguintes ações:
>
>* Um serviço no fluxo de dados deve ser configurado para recuperar dados de uma propriedade específica na `data` objeto
>* Cada propriedade deve ser mapeada para um campo XDM
>
>Se um determinado campo não for mapeado para um campo XDM ou usado por um serviço configurado, esses dados serão perdidos permanentemente.

## Usar a propriedade de dados usando a extensão de tag do SDK da Web

Forneça um elemento de dados no **[!UICONTROL Dados]** nas ações de uma regra de tag.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Forneça o elemento de dados que contém o objeto desejado na variável **[!UICONTROL Dados]** campo.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Usar a propriedade de dados usando a biblioteca JavaScript do SDK da Web

Defina o `data` como parte do objeto JSON no parâmetro da variável `sendEvent` comando. Para dados que você planeja mapear na sequência de dados, é possível estruturar essa propriedade da maneira que você desejar. Para dados usados por determinados serviços, verifique se a hierarquia de objetos corresponde ao que o serviço espera. É possível incluir os `data` e o [`xdm`](xdm.md) objeto no mesmo `sendEvent` comando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
