---
keywords: Experience Platform; home; tópicos populares; mapear csv; mapear arquivo csv; mapear arquivo csv para xdm; mapear csv para xdm; guia da interface do usuário; mapeador; mapeamento; preparação de dados; preparação de dados;
solution: Experience Platform
title: Visão geral da preparação de dados
topic-legacy: overview
description: Este documento apresenta a Preparação de dados no Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Campos calculados

Os campos calculados permitem que os valores sejam criados com base nos atributos no schema de entrada. Esses valores podem ser atribuídos aos atributos no schema de destino e receber um nome e uma descrição para permitir uma referência mais fácil.

Para criar um campo calculado, selecione **[!UICONTROL Add calculated field]**.

![](./images/calculated-fields/add-calculated-field.png)

O painel **[!UICONTROL Criar campo calculado]** é exibido. A caixa de diálogo à esquerda contém os campos, as funções e os operadores suportados nos campos calculados. Selecione uma das guias para começar a adicionar funções, campos ou operadores ao editor de expressão.

![](./images/calculated-fields/create-calculated-field.png)

| Tabulação | Descrição |
| --- | ----------- |
| Função | A guia funções lista as funções disponíveis para transformar os dados. Para saber mais sobre as funções que você pode usar nos campos calculados, leia o guia em [usando as funções de Preparação de Dados (Mapeador)](./functions.md). |
| Campo | A guia fields lista campos e atributos disponíveis no schema de origem. |
| Operador | A guia operadores lista os operadores disponíveis para transformar os dados. |

É possível adicionar campos, funções e operadores manualmente usando o editor de expressão no centro. Selecione o editor para começar a criar uma expressão.

![](./images/calculated-fields/write-calculated-field.png)

Selecione **[!UICONTROL Salvar]** para continuar.

A tela de mapeamento é exibida novamente com o campo de origem recém-criado. Aplique o campo de destino correspondente apropriado e selecione **[!UICONTROL Finish]** para concluir o mapeamento.

![](./images/calculated-fields/new-calculated-field.png)