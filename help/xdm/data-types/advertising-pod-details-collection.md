---
title: Tipo de dados da coleção de detalhes do pod do Advertising
description: Saiba mais sobre o tipo de dados Coleção de detalhes do pod do Advertising Experience Data Model (XDM).
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Detalhes do pod do Advertising] Tipo de dados da coleção

A Coleção [!UICONTROL Detalhes do pod do Advertising] é um tipo de dados padrão do Experience Data Model (XDM). Ele define uma sequência ou grupo de anúncios normalmente reproduzidos em sucessão durante quebras de conteúdo. Use o tipo de dados Coleção [!UICONTROL Detalhes do pod do Advertising] para capturar detalhes como ID do ad break, um nome amigável para o ad break, o índice de anúncios no ad break e o deslocamento do ad break na linha do tempo do conteúdo em segundos.

![Um diagrama do tipo de dados Coleta de Informações de Detalhes do Pod do Advertising.](../images/data-types/advertising-pod-details-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Anúncio Na Posição Do Pod] | `index` | inteiro | Sim | O índice do anúncio dentro do início do ad break principal. |
| [!UICONTROL Nome Amigável do Pod] | `friendlyName` | sequência de caracteres | Não | O nome facilmente compreensível do ad break. |
| [!UICONTROL Deslocamento do pod] | `offset` | inteiro | Sim | O deslocamento do ad break no conteúdo, em segundos. |
