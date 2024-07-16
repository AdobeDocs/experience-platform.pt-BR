---
title: Tipo de Dados da Coleta Final da Lista de Estados
description: Saiba mais sobre o tipo de dados List of States End Collection Experience Data Model (XDM).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL Lista de Finalizações de Estados] tipo de dados

O tipo de dados List of States End Collection é um tipo de dados Experience Data Model (XDM) criado para representar informações relacionadas ao estado final de vários atributos do player. Inclui as propriedades [!UICONTROL Nome do Estado do Player], que indicam o estado do atributo específico (por exemplo, &quot;tela cheia&quot;, &quot;mudo&quot;, &quot;closedCaptioning&quot;). Esse tipo de dados é usado para capturar e descrever as condições iniciais de diferentes estados do player.

![Um diagrama do tipo de dados List of States End Collection.](../images/data-types/list-of-states-end-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome do estado do player] | `name` | sequência de caracteres | Não | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |

{style="table-layout:auto"}
