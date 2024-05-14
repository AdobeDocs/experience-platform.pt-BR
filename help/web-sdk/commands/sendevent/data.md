---
title: dados
description: Saiba como enviar dados não XDM para o Adobe, por meio do objeto de dados.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

A variável `data` permite enviar um conteúdo para o Adobe que não corresponde a um esquema XDM. É útil em cenários que não sejam XDM, como o envio de dados diretamente para o Adobe Analytics, Adobe Target ou Adobe Audience Manager. Quando os dados chegam à sequência de dados, você pode usar [Mapeamento de preparação de dados](/help/data-prep/ui/mapping.md) para atribuir campos XDM a cada campo no `data` objeto.

>[!IMPORTANT]
>
>Os dados nesse objeto devem ter pelo menos uma das seguintes ações:
>
>* Um serviço no fluxo de dados deve ser configurado para recuperar dados de uma determinada propriedade na `data` objeto.
>* A propriedade especificada deve ser mapeada para um campo XDM usando o preparo de dados.
>
>Se uma determinada propriedade não for mapeada para um campo XDM ou usada por um serviço configurado, esses dados serão perdidos permanentemente.

## Use o `data` por meio da extensão de tag do SDK da Web {#tag-extension}

Forneça um elemento de dados no **[!UICONTROL Dados]** nas ações de uma regra de tag.

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o [!UICONTROL Extensão] campo suspenso até **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de ação] para **[!UICONTROL Enviar evento]**.
1. Forneça o elemento de dados que contém o objeto desejado na variável **[!UICONTROL Dados]** campo.
1. Clique em **[!UICONTROL Manter alterações]**, em seguida, execute o fluxo de trabalho de publicação.

## Use o `data` por meio da biblioteca JavaScript do SDK da Web {#library}

Defina o `data` como parte do objeto JSON no parâmetro da variável `sendEvent` comando. Para dados que você planeja mapear na sequência de dados, é possível estruturar esse objeto da maneira que você desejar. Para dados usados por determinados serviços, verifique se a hierarquia de objetos corresponde ao que o serviço espera. É possível incluir os `data` e o [`xdm`](xdm.md) objeto no mesmo `sendEvent` comando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Use o `data` objeto com o Adobe Analytics {#analytics}

Você pode usar o `data` com o Adobe Analytics para enviar dados a um conjunto de relatórios sem um esquema XDM. As variáveis são configuradas para usar a mesma sintaxe que [!DNL AppMeasurement] variáveis, simplificando o processo de atualização para o SDK da Web. Consulte [Mapeamento da variável de objeto de dados para o Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) no guia de implementação do Adobe Analytics para obter mais informações.
