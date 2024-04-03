---
title: Tipo de Dados da Coleta Final da Lista de Estados
description: Saiba mais sobre o tipo de dados List of States End Collection Experience Data Model (XDM).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL Fim da lista de estados] tipo de dados

O tipo de dados List of States End Collection é um tipo de dados Experience Data Model (XDM) criado para representar informações relacionadas ao estado final de vários atributos do player. Inclui a [!UICONTROL Nome do estado do player] propriedades que indicam o estado específico do atributo (por exemplo, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Esse tipo de dados é usado para capturar e descrever as condições iniciais de diferentes estados do player.

![Um diagrama do tipo de dados List of States End Collection.](../images/data-types/list-of-states-end-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome do estado do player] | `name` | string | Não | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |

{style="table-layout:auto"}
