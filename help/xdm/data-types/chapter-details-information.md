---
title: Detalhes do capítulo Informações Tipo de dados
description: Saiba mais sobre o tipo de dados Detalhes do capítulo Informações do Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 6%

---

# [!UICONTROL Informações de detalhes do capítulo] tipo de dados

[!UICONTROL Informações de detalhes do capítulo] é um tipo de dados padrão do Experience Data Model (XDM) que descreve vários atributos relacionados a capítulos ou segmentos no conteúdo de mídia. Use o [!UICONTROL Informações de detalhes do capítulo] tipo de dados para registrar detalhes como nome do capítulo, duração, posição, ID, status de reprodução (iniciado/concluído) e o tempo gasto em cada capítulo.

![Um diagrama do tipo de dados Informações detalhadas do capítulo.](../images/data-types/chapter-details-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL Nome do capítulo] | `friendlyName` | string | O nome do capítulo e/ou segmento. |
| [!UICONTROL Duração Ou Comprimento Do Capítulo] | `length` | inteiro | **Obrigatório** A duração do capítulo, em segundos. |
| [!UICONTROL Deslocamento de capítulo] | `offset` | inteiro | **Obrigatório** O deslocamento do capítulo dentro do conteúdo (em segundos) desde o início. |
| [!UICONTROL Posição do capítulo] | `index` | inteiro | **Obrigatório** A posição (índice, número inteiro) do capítulo dentro do conteúdo. |
| [!UICONTROL ID do capítulo] | `ID` | string | A ID gerada automaticamente do capítulo. |
| [!UICONTROL Capítulo iniciado] | `isStarted` | booleano | Se o capítulo foi iniciado. |
| [!UICONTROL Capítulo concluído] | `isCompleted` | booleano | Se o capítulo foi concluído. |
| [!UICONTROL Tempo de reprodução do capítulo] | `timePlayed` | inteiro | O tempo gasto no capítulo, em segundos. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
