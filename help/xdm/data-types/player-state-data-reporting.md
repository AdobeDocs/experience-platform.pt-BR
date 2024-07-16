---
title: Tipo de dados do relatório de dados do estado do player
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência (XDM) dos relatórios de dados do estado do player.
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 21%

---

# [!UICONTROL Tipo de dados do Relatório de dados do estado do player]

[!UICONTROL Relatórios de dados de estado do player] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os vários estados e suas ocorrências em um reprodutor de mídia. Use o tipo de dados [!UICONTROL Relatório de Dados do Estado do Player] para capturar diferentes estados do player, como tela cheia, mudo, legendas ocultas, picture-in-picture e estados em foco. Para cada estado, ele registra se o estado está definido, a contagem de ocorrências e a duração total em que permanece ativo durante a reprodução da mídia.

![Um diagrama do tipo de dados do Relatório de Dados do Estado do Player.](../images/data-types/player-state-data-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Nome do estado do player] | `name` | sequência de caracteres | O nome do estado do player. Enumerado: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;picture in picture&quot;, &quot;in focus&quot; com os respectivos significados. |
| [!UICONTROL Conjunto de estados do player] | `isSet` | booleano | Se o estado do player está ou não definido nesse estado. |
| [!UICONTROL Contagem do estado do player] | `count` | inteiro | O número de vezes que o estado do player foi definido no stream. |
| [!UICONTROL Hora do estado do player] | `time` | inteiro | A duração total desse estado do player. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
