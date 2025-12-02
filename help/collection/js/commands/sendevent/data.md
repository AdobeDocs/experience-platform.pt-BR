---
title: dados
description: Saiba como enviar dados não XDM para o Adobe, por meio do objeto de dados.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

O objeto `data` permite enviar uma carga para o Adobe que não corresponde a um esquema XDM. É útil em cenários que não sejam XDM, como o envio de dados diretamente para o Adobe Analytics, Adobe Target ou Adobe Audience Manager. Quando os dados chegam à sequência de dados, você pode usar o [mapeamento do Preparo de Dados](/help/data-prep/ui/mapping.md) para atribuir campos XDM a cada campo no objeto `data`. Se um produto já estiver configurado pelo Adobe para detectar campos no objeto `data`, você poderá enviar esses dados como estão para um fluxo de dados.

>[!IMPORTANT]
>
>Os dados nesse objeto devem ter pelo menos uma das seguintes ações:
>
>* Um serviço na sequência de dados deve ser configurado para recuperar dados de uma determinada propriedade no objeto `data`.
>* A propriedade especificada deve ser mapeada para um campo XDM usando o preparo de dados.
>
>Se uma determinada propriedade não for mapeada para um campo XDM ou usada por um serviço configurado, esses dados serão perdidos permanentemente.

Defina o objeto `data` como parte do objeto JSON dentro do parâmetro do comando `sendEvent`. Para dados que você planeja mapear na sequência de dados, é possível estruturar esse objeto da maneira que você desejar. Para dados usados por determinados serviços, verifique se a hierarquia de objetos corresponde ao que o serviço espera. Você pode incluir os objetos `data` e [`xdm`](xdm.md) no mesmo comando `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Usar o objeto `data` com o Adobe Analytics {#analytics}

Você pode usar o objeto `data` com o Adobe Analytics para enviar dados a um conjunto de relatórios sem um esquema XDM. As variáveis são configuradas para usar a mesma sintaxe das variáveis do AppMeasurement, simplificando o processo de atualização para o Web SDK. Consulte [Mapeamento de variável de objeto de dados para o Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) no guia de implementação do Adobe Analytics para obter mais informações.

## Usar o objeto `data` usando a extensão de tag do Web SDK

O objeto `data` está disponível como um [Elemento de dados de variável](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) ao usar a extensão de marca do Web SDK.
