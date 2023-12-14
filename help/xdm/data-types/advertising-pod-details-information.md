---
title: Detalhes do pod de publicidade Informações Tipo de dados
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência (XDM) de detalhes do pod de publicidade.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL Informações de detalhes do pod de publicidade] tipo de dados

[!UICONTROL Informações de detalhes do pod de publicidade] é um tipo de dados padrão do Experience Data Model (XDM). Ele define uma sequência ou grupo de anúncios normalmente reproduzidos em sucessão durante quebras de conteúdo. Use o [!UICONTROL Informações de detalhes do pod de publicidade] tipo de dados para capturar detalhes como ID do ad break, um nome amigável para o ad break, o índice de anúncios no intervalo e o deslocamento do ad break na linha do tempo do conteúdo em segundos.

![Um diagrama do tipo de dados Advertising Pod Details Information.](../images/data-types/advertising-pod-details-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID do ad break] | `ID` | string | A ID do ad break. |
| [!UICONTROL Nome amigável do pod] | `friendlyName` | string | O nome facilmente compreensível do ad break. |
| [!UICONTROL Posição do pod de anúncio] | `index` | inteiro | O índice do anúncio dentro do início do ad break principal. |
| [!UICONTROL Deslocamento do pod] | `offset` | inteiro | **Obrigatório** O deslocamento do ad break no conteúdo, em segundos. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
