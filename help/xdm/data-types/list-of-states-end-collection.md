---
title: Tipo de Dados da Coleta Final da Lista de Estados
description: Saiba mais sobre o tipo de dados List of States End Collection Experience Data Model (XDM).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# [!UICONTROL List of States End] tipo de dados

O tipo de dados List of States End Collection é um tipo de dados Experience Data Model (XDM) criado para representar informações relacionadas ao estado final de vários atributos do player. Inclui as propriedades [!UICONTROL Player State Name] que indicam o estado de atributo específico (por exemplo, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Esse tipo de dados é usado para capturar e descrever as condições iniciais de diferentes estados do player.

![Um diagrama do tipo de dados List of States End Collection.](../images/data-types/list-of-states-end-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | sequência de caracteres | Não | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |

{style="table-layout:auto"}
