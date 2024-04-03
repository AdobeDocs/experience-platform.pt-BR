---
title: Tipo de dados de relatório de detalhes do pod de publicidade
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) dos relatórios de detalhes do Pod de publicidade.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 4%

---

# [!UICONTROL Relatório de detalhes do pod de publicidade] tipo de dados

[!UICONTROL Relatório de detalhes do pod de publicidade] é um tipo de dados padrão do Experience Data Model (XDM). Ele define uma sequência ou grupo de anúncios normalmente reproduzidos em sucessão durante quebras de conteúdo. Use o [!UICONTROL Relatório de detalhes do pod de publicidade] tipo de dados para capturar detalhes como ID do ad break, um nome amigável para o ad break, o índice de anúncios no intervalo e o deslocamento do ad break na linha do tempo do conteúdo em segundos.

![Um diagrama do tipo de dados Relatórios de detalhes do pod de anúncios.](../images/data-types/advertising-pod-details-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID do ad break] | `ID` | string | A ID do ad break. |
| [!UICONTROL Nome amigável do pod] | `friendlyName` | string | O nome facilmente compreensível do ad break. |
| [!UICONTROL Posição do pod de anúncio] | `index` | inteiro | O índice do anúncio dentro do início do ad break principal. |
| [!UICONTROL Deslocamento do pod] | `offset` | inteiro | **Obrigatório** O deslocamento do ad break no conteúdo, em segundos. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
