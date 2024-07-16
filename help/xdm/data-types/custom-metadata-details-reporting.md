---
title: Detalhes de metadados personalizados Tipo de dados de relatório
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de relatório de detalhes de metadados personalizados (XDM).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# [!UICONTROL Detalhes de metadados personalizados] Tipo de dados de relatório

[!UICONTROL Detalhes de metadados personalizados] Os relatórios são um tipo de dados padrão do Experience Data Model (XDM) e definem uma estrutura para armazenar metadados personalizados. O tipo de dados de relatório [!UICONTROL Detalhes de metadados personalizados] captura detalhes como o nome e o valor dos metadados personalizados associados ao conteúdo ou às interações. Os campos de relatórios de mídia são usados pelos serviços da Adobe para analisar os campos de coleção de mídia enviados pelos usuários. Esses dados, juntamente com outras métricas específicas do usuário, são calculados e relatados.

![Um diagrama do tipo de dados Relatórios de Detalhes de Metadados Personalizados.](../images/data-types/the-custom-metadata-reporting.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nome do campo de metadados personalizado] | `name` | sequência de caracteres | O nome do campo personalizado. |
| [!UICONTROL Valor do campo de metadados personalizado] | `value` | sequência de caracteres | O valor do campo personalizado. |

{style="table-layout:auto"}
