---
title: Sobreposições avançadas de público-alvo
description: Saiba como analisar interseções de público-alvo e tomar decisões orientadas por dados usando o painel Sobreposições avançadas de público-alvo. Filtre públicos, compare sobreposições e exporte insights para melhorar as estratégias de direcionamento.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 2%

---

# Sobreposições avançadas de público-alvo

Obtenha insights valiosos para otimizar a segmentação de público e as estratégias de direcionamento analisando como diferentes segmentos de público se cruzam com o painel [!UICONTROL Sobreposições de público avançadas]. Examine as métricas tabuladas para identificar sobreposições, refinar a segmentação e reduzir as mensagens redundantes. Por fim, você pode usar esses insights para criar campanhas mais direcionadas e esforços de marketing eficientes. Nesse painel, você pode revisar as interseções de público-alvo, aplicar filtros e executar análises detalhadas de sobreposição para tomar decisões orientadas por dados e melhorar os resultados do engajamento.

## Filtrar públicos {#filter-audiences}

Para filtrar públicos específicos para análise de sobreposição, selecione o ícone de filtro (![O ícone de filtro.](../../../images/icons/filter-icon-white.png)) para abrir o diálogo [!UICONTROL Filtro]. Aqui, é possível adicionar ou remover públicos-alvo do modelo de sobreposição para refinar a análise.

![O modo de exibição de Sobreposição de Público Avançado com o ícone de filtro realçado.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-filter-icon.png)

A caixa de diálogo [!UICONTROL Filtros] é exibida. Para escolher um público-alvo para análise de sobreposição, selecione um nome de público-alvo na lista suspensa **[!UICONTROL Público-alvo]**. O nome de qualquer público-alvo adicionado é exibido com uma tag abaixo da lista suspensa. Depois de adicionado, você pode selecionar o &#39;X&#39; pelo nome para removê-los. Para remover todos os filtros aplicados, selecione **[!UICONTROL Limpar tudo]**.

## Filtros aplicados {#applied-filters}

Depois que um filtro é aplicado ([!UICONTROL Segmento de amoxicilina] no exemplo da captura de tela), os dados do público-alvo exibidos são limitados. Qualquer público adicional que você optar por adicionar será exibido ao lado da tag [!UICONTROL Filtragem por], acima do gráfico [!UICONTROL Sobreposições de público-alvo avançadas].

![O painel Sobreposição de Público-Alvo Avançado com Filtragem por Segmento de Amoxicilina realçado.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-applied-filters.png)

## Tabela avançada de sobreposições de público {#advanced-audience-overlaps-table}

A seção principal do painel exibe a tabela [!UICONTROL Sobreposições avançadas de público-alvo], que fornece uma comparação detalhada das sobreposições de público-alvo entre segmentos diferentes. As colunas da tabela são as seguintes:

| Nome da coluna | Descrição |
|------------------------------------|----------------------------------------------------------------------------------------------|
| **[!UICONTROL Source_Segment_Name]** | O público original que está sendo analisado (por exemplo, &quot;Segmento de amoxicilina&quot;). |
| **[!UICONTROL Sobrepor_Nome_Do_Segmento]** | O público cujas sobreposições estão sendo comparadas (por exemplo, &quot;Glicose no sangue > 100&quot;). |
| **[!UICONTROL Contagem_De_Público_Do_Segmento_Source]** | O número total de perfis do público de origem. |
| **[!UICONTROL Contagem_De_Público_De_Segmento_Sobreposição]** | O tamanho do público-alvo sobreposto, que varia dependendo da sobreposição. |
| **[!UICONTROL Contagem_De_Público_Sobreposição]** | O tamanho do público-alvo real sobreposto entre os públicos-alvo de origem e de sobreposição. |

{style="table-layout:auto"}

## Exportar Insights {#export-insights}

Depois de filtrar e analisar os públicos-alvo, é possível exportar os dados para fins de análise offline ou relatórios. Para exportar seus insights, selecione **[!UICONTROL Exportar]** na parte superior direita da tabela. A caixa de diálogo PDF de impressão é exibida, permitindo salvar os dados como um PDF ou imprimi-los.

![O modo de exibição Sobreposição de Público Avançado com Exportação realçado.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-export.png)

Para retornar à visão geral do [!UICONTROL Modelo], selecione **[!UICONTROL Modelos]**.

![O modo de exibição de Sobreposição de Público-Alvo Avançado com Modelos foi realçado.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-navigation.png)

## Próximas etapas

Depois de ler este documento, você aprendeu a analisar interseções de público-alvo e tomar decisões orientadas por dados usando o painel **[!UICONTROL Sobreposições de público-alvo avançadas]**. Para otimizar ainda mais sua segmentação de público e estratégias de direcionamento, explore outros Modelos de Distiller de dados que fornecem insights valiosos. Consulte os guias da interface de [Tendências de público-alvo](./trends.md), [Comparação de público-alvo](./comparison.md) e [Sobreposições de identidade de público-alvo](./identity-overlaps.md) para continuar aprimorando seus esforços de envolvimento e segmentação de público-alvo.

