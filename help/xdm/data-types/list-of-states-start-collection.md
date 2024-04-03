---
title: Tipo de dados da coleção de início da lista de estados
description: Saiba mais sobre o tipo de dados List of States Start Data Model (XDM).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 5%

---

# [!UICONTROL Lista de Início de Estados] tipo de dados

A variável [!UICONTROL Lista de Início de Estados] O tipo de dados é um tipo de dados do Experience Data Model (XDM) criado para representar informações relacionadas ao estado inicial de vários atributos do player. Inclui a [!UICONTROL Nome do estado do player] propriedades que indicam o estado específico do atributo (por exemplo, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Esse tipo de dados é usado para capturar e descrever as condições iniciais de diferentes estados do player.

![Um diagrama de [!UICONTROL Lista de Início de Estados] tipo de dados.](../images/data-types/list-of-states-start-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome do estado do player] | `name` | string | Não | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |

{style="table-layout:auto"}
