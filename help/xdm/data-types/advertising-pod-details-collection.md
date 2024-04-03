---
title: Tipo de dados da coleção de detalhes do pod de publicidade
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) da coleção de detalhes do pod de publicidade.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---

# [!UICONTROL Detalhes do pod de publicidade] Tipo de dados de coleção

[!UICONTROL Detalhes do pod de publicidade] A coleção é um tipo de dados padrão do Experience Data Model (XDM). Ele define uma sequência ou grupo de anúncios normalmente reproduzidos em sucessão durante quebras de conteúdo. Use o [!UICONTROL Detalhes do pod de publicidade] Tipo de dados da coleção para capturar detalhes como ID do ad break, um nome amigável para o ad break, o índice de anúncios no intervalo e o deslocamento do ad break na linha do tempo do conteúdo em segundos.

![Um diagrama do tipo de dados Coleção de informações de detalhes do pod de anúncios.](../images/data-types/advertising-pod-details-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Posição do pod de anúncio] | `index` | inteiro | Sim | O índice do anúncio dentro do início do ad break principal. |
| [!UICONTROL Nome amigável do pod] | `friendlyName` | string | Não | O nome facilmente compreensível do ad break. |
| [!UICONTROL Deslocamento do pod] | `offset` | inteiro | Sim | O deslocamento do ad break no conteúdo, em segundos. |
