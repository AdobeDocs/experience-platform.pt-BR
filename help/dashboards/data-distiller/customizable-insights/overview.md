---
title: Insights personalizáveis para relatórios estendidos do aplicativo
description: Saiba como usar consultas SQL para gerar insights para seus painéis personalizados.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Insights personalizáveis para relatórios estendidos do aplicativo

Use consultas SQL personalizadas para extrair insights de diversos conjuntos de dados estruturados com eficiência. Os técnicos podem usar o modo query pro para executar análises complexas com SQL e, em seguida, compartilhar essa análise com usuários não técnicos por meio de gráficos em seu painel personalizado ou exportá-los em arquivos CSV. Esse método de criação de insights é adequado para tabelas com relações claras e permite um maior grau de personalização em seus insights e filtros que podem atender a casos de uso de nicho.

>[!IMPORTANT]
>
>O modo Query pro está disponível somente para usuários que compraram o [SKU do Data Distiller](../../../query-service/data-distiller/overview.md).

Para gerar insights do SQL, primeiro você deve criar um painel.

## Criar um painel personalizado {#create-custom-dashboard}

Para criar um painel personalizado, selecione **[!UICONTROL Painéis]** no painel de navegação esquerdo, para abrir o espaço de trabalho Painéis. Em seguida, selecione **[!UICONTROL Criar painel]**.

![O inventário do Painel com a opção Criar painel realçada.](../../images/customizable-insights/create-dashboard.png)

A variável **[!UICONTROL Criar painel]** será exibida. Há duas opções para escolher o método de criação de painel. Para criar seus insights, é possível usar um modelo de dados existente com o [[!UICONTROL Modo de design guiado]](../../user-defined-dashboards.md) ou seu próprio SQL com o [!UICONTROL Modo pro da consulta].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

O uso de um modelo de dados existente tem os benefícios de fornecer uma estrutura estruturada, eficiente e escalável personalizada para suas necessidades comerciais específicas. Para saber como [criar insights a partir de um modelo de dados existente](../../user-defined-dashboards.md#create-widget), consulte o guia do painel personalizado.

Os insights gerados a partir de consultas SQL oferecem muito mais flexibilidade e personalização. Os técnicos podem usar o modo query pro para realizar análises complexas no SQL e, em seguida, compartilhar essa análise com usuários não técnicos por meio desse recurso do painel. Selecionar **[!UICONTROL Modo pro da consulta]** seguido por **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Depois de fazer uma seleção, não é possível alterar essa seleção nesse painel. Em vez disso, você deve criar um novo painel com um método de criação de painel diferente.

![A variável [!UICONTROL Criar painel] caixa de diálogo com o modo Query pro e Salvar realçados.](../../images/customizable-insights/query-pro-mode.png)

## Criar um gráfico {#create-a-chart}

Consulte a [guia do modo query pro](./query-pro-mode.md) para obter instruções passo a passo sobre como criar um gráfico com SQL.
