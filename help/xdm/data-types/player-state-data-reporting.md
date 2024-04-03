---
title: Tipo de dados do relatório de dados do estado do player
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência (XDM) dos relatórios de dados do estado do player.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 4%

---

# [!UICONTROL Relatório de dados do estado do player] tipo de dados

[!UICONTROL Relatório de dados do estado do player] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os vários estados e suas ocorrências em um reprodutor de mídia. Use o [!UICONTROL Relatório de dados do estado do player] tipo de dados para capturar diferentes estados do player, como tela cheia, mudo, legendas ocultas, picture-in-picture e estados em foco. Para cada estado, ele registra se o estado está definido, a contagem de ocorrências e a duração total em que permanece ativo durante a reprodução da mídia.

![Um diagrama do tipo de dados do Relatório de dados do estado do player.](../images/data-types/player-state-data-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Nome do estado do player] | `name` | string | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |
| [!UICONTROL Conjunto do estado do player] | `isSet` | booleano | Se o estado do player está ou não definido nesse estado. |
| [!UICONTROL Contagem do estado do player] | `count` | inteiro | O número de vezes que o estado do player foi definido no stream. |
| [!UICONTROL Tempo do estado do player] | `time` | inteiro | A duração total desse estado do player. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
