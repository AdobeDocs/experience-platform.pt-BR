---
title: Tipo de dados da coleção de início da lista de estados
description: Saiba mais sobre o tipo de dados List of States Start Data Model (XDM).
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Tipo de dados Início da Lista de Estados]

O tipo de dados [!UICONTROL Lista de Estados Início] é um tipo de dados Experience Data Model (XDM) criado para representar informações relacionadas ao estado inicial de vários atributos do player. Inclui as propriedades [!UICONTROL Nome do Estado do Player], que indicam o estado do atributo específico (por exemplo, &quot;tela cheia&quot;, &quot;mudo&quot;, &quot;closedCaptioning&quot;). Esse tipo de dados é usado para capturar e descrever as condições iniciais de diferentes estados do player.

![Um diagrama do tipo de dados [!UICONTROL List of States Start].](../images/data-types/list-of-states-start-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome do estado do player] | `name` | sequência de caracteres | Não | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |

{style="table-layout:auto"}
