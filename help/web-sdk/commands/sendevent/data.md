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

O objeto `data` permite enviar uma carga para o Adobe que não corresponde a um esquema XDM. É útil em cenários que não sejam XDM, como o envio de dados diretamente para o Adobe Analytics, Adobe Target ou Adobe Audience Manager. Quando os dados chegam à sequência de dados, você pode usar o [mapeamento do Preparo de Dados](/help/data-prep/ui/mapping.md) para atribuir campos XDM a cada campo no objeto `data`.

>[!IMPORTANT]
>
>Os dados nesse objeto devem ter pelo menos uma das seguintes ações:
>
>* Um serviço na sequência de dados deve ser configurado para recuperar dados de uma determinada propriedade no objeto `data`.
>* A propriedade especificada deve ser mapeada para um campo XDM usando o preparo de dados.
>
>Se uma determinada propriedade não for mapeada para um campo XDM ou usada por um serviço configurado, esses dados serão perdidos permanentemente.

## Usar o objeto `data` por meio da extensão de tag do SDK da Web {#tag-extension}

Forneça um elemento de dados no campo **[!UICONTROL Dados]** dentro das ações de uma regra de marca.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Regras]** e selecione a regra desejada.
1. Em [!UICONTROL Ações], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extensão] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina o [!UICONTROL Tipo de Ação] como **[!UICONTROL Enviar evento]**.
1. Forneça o elemento de dados que contém o objeto desejado no campo **[!UICONTROL Dados]**.
1. Clique em **[!UICONTROL Manter alterações]** e execute o fluxo de trabalho de publicação.

## Usar o objeto `data` por meio da biblioteca JavaScript do SDK da Web {#library}

Defina o objeto `data` como parte do objeto JSON dentro do parâmetro do comando `sendEvent`. Para dados que você planeja mapear na sequência de dados, é possível estruturar esse objeto da maneira que você desejar. Para dados usados por determinados serviços, verifique se a hierarquia de objetos corresponde ao que o serviço espera. Você pode incluir os objetos `data` e [`xdm`](xdm.md) no mesmo comando `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Usar o objeto `data` com o Adobe Analytics {#analytics}

Você pode usar o objeto `data` com o Adobe Analytics para enviar dados a um conjunto de relatórios sem um esquema XDM. As variáveis são configuradas para usar a mesma sintaxe que [!DNL AppMeasurement] variáveis, simplificando o processo de atualização para o SDK da Web. Consulte [Mapeamento de variável de objeto de dados para o Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) no guia de implementação do Adobe Analytics para obter mais informações.
