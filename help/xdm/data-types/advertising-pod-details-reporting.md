---
title: Tipo de dados de relatório de detalhes do pod do Advertising
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) dos detalhes do pod do Advertising.
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# [!UICONTROL Tipo de dados de Relatórios de Detalhes do Pod do Advertising]

[!UICONTROL Relatórios de Detalhes do Pod do Advertising] é um tipo de dados padrão do Experience Data Model (XDM). Ele define uma sequência ou grupo de anúncios normalmente reproduzidos em sucessão durante quebras de conteúdo. Use o tipo de dados [!UICONTROL Relatório de detalhes do pod do Advertising] para capturar detalhes como ID do ad break, um nome amigável para o ad break, o índice de anúncios no ad break e o deslocamento do ad break na linha do tempo do conteúdo em segundos.

![Um diagrama do tipo de dados do Relatório de Detalhes do Pod do Advertising.](../images/data-types/advertising-pod-details-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID do ad break] | `ID` | sequência de caracteres | A ID do ad break. |
| [!UICONTROL Nome Amigável do Pod] | `friendlyName` | sequência de caracteres | O nome facilmente compreensível do ad break. |
| [!UICONTROL Anúncio Na Posição Do Pod] | `index` | inteiro | O índice do anúncio dentro do início do ad break principal. |
| [!UICONTROL Deslocamento do pod] | `offset` | inteiro | **Obrigatório** O deslocamento do ad break no conteúdo, em segundos. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
