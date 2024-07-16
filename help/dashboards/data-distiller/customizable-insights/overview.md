---
title: Insights personalizáveis para relatórios estendidos do aplicativo
description: Saiba como usar consultas SQL para gerar insights para seus painéis personalizados.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Insights personalizáveis para relatórios estendidos do aplicativo

Use consultas SQL personalizadas para extrair insights de diversos conjuntos de dados estruturados com eficiência. Os técnicos podem usar o modo query pro para executar análises complexas com SQL e, em seguida, compartilhar essa análise com usuários não técnicos por meio de gráficos em seu painel personalizado ou exportá-los em arquivos CSV. Esse método de criação de insights é adequado para tabelas com relações claras e permite um maior grau de personalização em seus insights e filtros que podem atender a casos de uso de nicho.

>[!IMPORTANT]
>
>O modo pro de consulta só está disponível para usuários que compraram a [SKU do Data Distiller](../../../query-service/data-distiller/overview.md).

Para gerar insights do SQL, primeiro você deve criar um painel.

## Criar um painel personalizado {#create-custom-dashboard}

Para criar um painel personalizado, selecione **[!UICONTROL Painéis]** no painel de navegação esquerdo para abrir o espaço de trabalho Painéis. Em seguida, selecione **[!UICONTROL Criar painel]**.

![O inventário de Painel com Criar painel realçado.](../../images/customizable-insights/create-dashboard.png)

A caixa de diálogo **[!UICONTROL Criar painel]** é exibida. Há duas opções para escolher o método de criação de painel. Para criar seus insights, você pode usar um modelo de dados existente com o [[!UICONTROL Modo de design guiado]](../../user-defined-dashboards.md) ou seu próprio SQL com o [!UICONTROL Modo profissional de consulta].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

O uso de um modelo de dados existente tem os benefícios de fornecer uma estrutura estruturada, eficiente e escalável personalizada para suas necessidades comerciais específicas. Para saber como [criar insights de um modelo de dados existente](../../user-defined-dashboards.md#create-widget), consulte o guia do painel personalizado.

Os insights gerados a partir de consultas SQL oferecem muito mais flexibilidade e personalização. Os técnicos podem usar o modo query pro para realizar análises complexas no SQL e, em seguida, compartilhar essa análise com usuários não técnicos por meio desse recurso do painel. Selecione **[!UICONTROL Modo profissional de consulta]** seguido por **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Depois de fazer uma seleção, não é possível alterar essa seleção nesse painel. Em vez disso, você deve criar um novo painel com um método de criação de painel diferente.

![A caixa de diálogo [!UICONTROL Criar painel] com o modo profissional Consulta e Salvar realçado.](../../images/customizable-insights/query-pro-mode.png)

## Criar um gráfico {#create-a-chart}

Consulte o [guia de modo profissional de consulta](./query-pro-mode.md) para obter instruções passo a passo sobre como criar um gráfico com SQL.
