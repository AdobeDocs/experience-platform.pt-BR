---
title: Tipo de dados da coleção de detalhes do capítulo
description: Saiba mais sobre o tipo de dados Coleção de detalhes do capítulo Modelo de dados de experiência (XDM).
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL Detalhes do capítulo] Tipo de dados da coleção

A Coleção [!UICONTROL Detalhes do capítulo] é um tipo de dados padrão do Experience Data Model (XDM) que descreve vários atributos relacionados a capítulos ou segmentos no conteúdo de mídia. Use o tipo de dados Coleção [!UICONTROL Detalhes do capítulo] para capturar detalhes como nome do capítulo, deslocamento, duração e índice do capítulo. Os campos de coleção de mídia capturam dados e os enviam para outros serviços da Adobe para processamento adicional.

![Um diagrama do tipo de dados Coleção de Detalhes de Capítulo.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Duração Ou Comprimento Do Capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=pt-BR#chapter-length) | `length` | inteiro | Sim | A duração do capítulo em segundos. |
| [[!UICONTROL Nome do capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=pt-BR#chapter-name) | `friendlyName` | sequência de caracteres | Não | O nome do capítulo e/ou segmento. |
| [[!UICONTROL Deslocamento de capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=pt-BR#chapter-offset) | `offset` | inteiro | Sim | O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início. |
| [[!UICONTROL Posição do capítulo]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=pt-BR#chapter-position) | `index` | inteiro | Sim | A posição (índice, número inteiro) do capítulo dentro do conteúdo. |

{style="table-layout:auto"}
