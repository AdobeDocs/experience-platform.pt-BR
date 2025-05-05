---
title: Tipo de Dados do Par de Valores de Chave
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) do par de valores principal.
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 5%

---

# Tipo de dados [!UICONTROL Par de Valores de Chave]

[!UICONTROL Par de Valores-Chave] é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de um par de valores-chave genérico. Este tipo de dados é usado no [[[!UICONTROL grupo de campos &#x200B;]](../field-groups/event/analytics-full-extension.md) da &lbrace;Extensão Completa de ExperienceEvent do Adobe Analytics] para descrever os itens de matriz de uma variável de lista.

![Estrutura do par de valores de chave](../images/data-types/key-value-pair.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `key` | String | Uma chave (nome) para uma variável ou valor genérico. |
| `value` | String | O valor da variável. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte [o repositório XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
