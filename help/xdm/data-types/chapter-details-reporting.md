---
title: Tipo de dados de relatório de detalhes do capítulo
description: Saiba mais sobre o capítulo Detalhes do modelo de dados de experiência (XDM).
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL Detalhes do capítulo] Tipo de dados do relatório

[!UICONTROL Detalhes do capítulo] Os relatórios são um tipo de dados padrão do Experience Data Model (XDM) que descreve vários atributos relacionados aos capítulos ou segmentos dentro do conteúdo de mídia. Use o tipo de dados de relatório [!UICONTROL Detalhes do capítulo] para capturar detalhes como nome do capítulo, duração, posição, ID, status de reprodução (iniciado/concluído) e o tempo gasto em cada capítulo. Os campos de relatórios de mídia são usados pelos serviços da Adobe para analisar os campos Coleção de mídia enviados pelos usuários. Esses dados, juntamente com outras métricas específicas do usuário, são calculados e relatados.

![Um diagrama do tipo de dados Relatórios de Detalhes do Capítulo.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Capítulo concluído]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | booleano | Se o capítulo foi concluído ou não. |
| [[!UICONTROL ID do capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | sequência de caracteres | A ID gerada automaticamente do capítulo. |
| [[!UICONTROL Duração Ou Comprimento Do Capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | inteiro | A duração do capítulo em segundos. |
| [[!UICONTROL Nome do capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | sequência de caracteres | O nome do capítulo e/ou segmento. |
| [[!UICONTROL Deslocamento de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | inteiro | O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início. |
| [[!UICONTROL Posição do capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | inteiro | A posição (índice, número inteiro) do capítulo dentro do conteúdo. |
| [[!UICONTROL Capítulo iniciado]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | booleano | Se o capítulo foi iniciado ou não. |
| [[!UICONTROL Tempo de reprodução do capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | inteiro | O tempo gasto no capítulo, em segundos. |
