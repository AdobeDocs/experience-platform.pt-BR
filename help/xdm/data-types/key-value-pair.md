---
title: Tipo de dados do par de valores-chave
description: Este documento fornece uma visão geral do tipo de dados XDM (Key Value Pair Experience Data Model).
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 5%

---

# [!UICONTROL Par. Valor Chave] tipo de dados

[!UICONTROL Par. Valor Chave] é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de um par de valores-chave genérico. Esse tipo de dados é usado na variável [[!UICONTROL Extensão completa do Adobe Analytics ExperienceEvent] grupo de campos](../field-groups/event/analytics-full-extension.md) para descrever os itens de matriz de uma variável de lista.

![Estrutura do par de valores-chave](../images/data-types/key-value-pair.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `key` | String | Uma chave (nome) para uma variável genérica ou valor. |
| `value` | String | O valor da variável. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte [o repositório XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
