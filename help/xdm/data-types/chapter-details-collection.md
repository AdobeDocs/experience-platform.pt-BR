---
title: Tipo de dados da coleção de detalhes do capítulo
description: Saiba mais sobre o tipo de dados Coleção de detalhes do capítulo Modelo de dados de experiência (XDM).
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---

# [!UICONTROL Chapter Details] Tipo de dados da coleção

A Coleção [!UICONTROL Chapter Details] é um tipo de dados padrão do Experience Data Model (XDM) que descreve vários atributos relacionados a capítulos ou segmentos no conteúdo de mídia. Use o tipo de dados Coleção [!UICONTROL Chapter Details] para capturar detalhes como nome do capítulo, deslocamento, duração e índice do capítulo. Os campos de coleção de mídia capturam dados e os enviam para outros serviços da Adobe para processamento adicional.

![Um diagrama do tipo de dados Coleção de Detalhes de Capítulo.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Cada nome de exibição contém um link para informações adicionais sobre os parâmetros de áudio e vídeo. As páginas vinculadas contêm detalhes sobre os dados de anúncios de vídeo coletados pelo Adobe, valores de implementação, parâmetros de rede, relatórios e considerações importantes.

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Chapter Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | inteiro | Sim | A duração do capítulo, em segundos. |
| [[!UICONTROL Chapter Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | sequência de caracteres | Não | O nome do capítulo e/ou segmento. |
| [[!UICONTROL Chapter Offset]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | inteiro | Sim | O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início. |
| [[!UICONTROL Chapter Position]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | inteiro | Sim | A posição (índice, número inteiro) do capítulo dentro do conteúdo. |

{style="table-layout:auto"}
