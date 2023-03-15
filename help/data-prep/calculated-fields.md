---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia de interface do usuário;mapeador;mapeamento;preparação de dados;preparação de dados;
solution: Experience Platform
title: Visão geral da preparação de dados
description: Este documento apresenta o Preparo de dados na Adobe Experience Platform.
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# Campos calculados

Os campos calculados permitem que valores sejam criados com base nos atributos no esquema de entrada. Esses valores podem ser atribuídos a atributos no esquema de destino e receber um nome e uma descrição para facilitar a referência.

Para criar um campo calculado, selecione **[!UICONTROL Adicionar campo calculado]**.

![](./images/calculated-fields/add-calculated-field.png)

A variável **[!UICONTROL Criar campo calculado]** é exibido. A caixa de diálogo à esquerda contém os campos, funções e operadores compatíveis com os campos calculados. Selecione uma das guias para começar a adicionar funções, campos ou operadores ao editor de expressão.

![](./images/calculated-fields/create-calculated-field.png)

| Tabulação | Descrição |
| --- | ----------- |
| Função | A guia functions lista as funções disponíveis para transformar os dados. Para saber mais sobre as funções que você pode usar em campos calculados, leia o guia em [uso das funções de Preparo de dados (Mapeador)](./functions.md). |
| Campo | A guia fields lista campos e atributos disponíveis no schema de origem. |
| Operador | A guia operators lista os operadores disponíveis para transformar os dados. |

Você pode adicionar campos, funções e operadores manualmente usando o editor de expressão no centro. Selecione o editor para começar a criar uma expressão.

![](./images/calculated-fields/write-calculated-field.png)

Selecionar **[!UICONTROL Salvar]** para continuar.

A tela de mapeamento é exibida novamente com o campo de origem recém-criado. Aplique o campo de destino correspondente apropriado e selecione **[!UICONTROL Concluir]** para concluir o mapeamento.

![](./images/calculated-fields/new-calculated-field.png)
