---
title: Tipo de dados de relatório de detalhes do capítulo
description: Saiba mais sobre o capítulo Detalhes do modelo de dados de experiência (XDM).
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# [!UICONTROL Chapter Details] Tipo de dados de relatório

Os relatórios do [!UICONTROL Chapter Details] são um tipo de dados padrão do Experience Data Model (XDM) que descrevem vários atributos relacionados aos capítulos ou segmentos no conteúdo de mídia. Use o tipo de dados de Relatório [!UICONTROL Chapter Details] para capturar detalhes como nome do capítulo, duração, posição, ID, status de reprodução (iniciado/concluído) e o tempo gasto em cada capítulo. Os campos de relatórios de mídia são usados pelos serviços da Adobe para analisar os campos Coleção de mídia enviados pelos usuários. Esses dados, juntamente com outras métricas específicas do usuário, são calculados e relatados.

![Um diagrama do tipo de dados Relatórios de Detalhes do Capítulo.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapter Completed]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | booleano | Se o capítulo foi concluído ou não. |
| [[!UICONTROL Chapter ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | sequência de caracteres | A ID gerada automaticamente do capítulo. |
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | inteiro | A duração do capítulo, em segundos. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | sequência de caracteres | O nome do capítulo e/ou segmento. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | inteiro | O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | inteiro | A posição (índice, número inteiro) do capítulo dentro do conteúdo. |
| [[!UICONTROL Chapter Started]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | booleano | Se o capítulo foi iniciado ou não. |
| [[!UICONTROL Chapter Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | inteiro | O tempo gasto no capítulo, em segundos. |
