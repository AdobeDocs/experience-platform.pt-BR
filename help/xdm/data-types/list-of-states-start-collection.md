---
title: Tipo de dados da coleção de início da lista de estados
description: Saiba mais sobre o tipo de dados List of States Start Data Model (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 8%

---

# [!UICONTROL List of States Start] tipo de dados

O tipo de dados [!UICONTROL List of States Start] é um tipo de dados do Experience Data Model (XDM) criado para representar informações relacionadas ao estado inicial de vários atributos do player. Inclui as propriedades [!UICONTROL Player State Name] que indicam o estado de atributo específico (por exemplo, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Esse tipo de dados é usado para capturar e descrever as condições iniciais de diferentes estados do player.

![Um diagrama de [!UICONTROL List of States Start] tipo de dados.](../images/data-types/list-of-states-start-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | sequência de caracteres | Não | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |

{style="table-layout:auto"}
