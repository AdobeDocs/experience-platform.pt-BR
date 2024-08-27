---
title: Criar um filtro global
description: Saiba como filtrar seus insights de dados com um filtro aplicado globalmente e personalizado.
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: 5dd821383e1b1a7bd4998a6cf14a941bfdf3f26c
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Criar um filtro global {#create-global-filter}

Para criar um filtro global, primeiro selecione **[!UICONTROL Adicionar filtro]** no modo de exibição de painel e, em seguida, **[!UICONTROL Filtro global]** no menu suspenso.

>[!IMPORTANT]
>
>Mapeie os filtros globais para todos os gráficos. Esse não é um processo automático. Para usar um filtro global, você deve incluir um [parâmetro de consulta](../../../../query-service/ui/parameterized-queries.md) no SQL do seu gráfico, [habilitar o filtro global](#enable-global-filter) no widget composer e [selecionar um valor de tempo de execução](#select-global-filter) para o parâmetro na caixa de diálogo de filtro global. Consulte o manual do query pro para saber como editar seu SQL se precisar incorporar um parâmetro de consulta.

![Um painel personalizado com Adicionar filtro e seu menu suspenso realçado.](../../../images/query-pro-mode/add-filter.png)

Você pode alterar rapidamente os insights fornecidos pelo SQL com filtros globais personalizados.

A caixa de diálogo [!UICONTROL Criar um filtro global] é aberta. A criação de um filtro global segue o mesmo processo que a criação de um insight com SQL. Primeiro, selecione um banco de dados (modelo de dados de insights) para consultar, em seguida, insira seu SQL personalizado no Editor de Consultas e, finalmente, selecione o ícone de execução (![Um ícone de execução.](/help/images/icons/play.png)).

>[!IMPORTANT]
>
>Você deve incluir uma ID e um valor ao criar um filtro global. Os valores de amostra permitem executar a instrução SQL e criar o gráfico. Observe que os valores de amostra fornecidos ao compor a instrução são substituídos pelos valores reais selecionados para o filtro de data ou global no tempo de execução.

Após executar o query com êxito, a guia results exibe os resultados. Selecione **[!UICONTROL Próximo]**.

![A [!UICONTROL caixa de diálogo Criar um filtro global] com o menu suspenso do conjunto de dados, o ícone Executar e o Próximo realçados.](../../../images/query-pro-mode/global-filter.png)

A etapa final do fluxo de trabalho de criação do filtro global requer a adição de um rótulo para o filtro. Adicione um rótulo ao campo de texto **[!UICONTROL Rótulo do filtro]** e selecione um tipo de filtro na caixa suspensa.

>[!NOTE]
>
>Somente a opção de tipo de filtro [!UICONTROL Caixa de combinação] tem suporte no momento.

Finalmente, selecione **[!UICONTROL Selecionar]** para retornar ao modo de exibição de painel.

![A [!UICONTROL caixa de diálogo Criar um filtro global] com a entrada de texto Selecionar e Rótulo de filtro realçada.](../../../images/query-pro-mode/global-filter-label.png)

## Ativar o filtro global para cada insight {#enable-global-filter}

>[!TIP]
>
>Habilite os filtros globais em cada gráfico criado. Isso garante que os valores escolhidos como filtro global sejam refletidos em todos os gráficos.

Depois de criar o filtro global para o painel, o botão de alternância para esse filtro global fica disponível como parte do widget composer.

![O widget composer com a opção Filtro Global realçada.](../../../images/query-pro-mode/global-filter-consent.png)

>[!IMPORTANT]
>
>Verifique se o parâmetro do filtro global está incluído no SQL de cada insight.

## Selecionar um filtro global {#select-global-filter}

Para abrir a caixa de diálogo [!UICONTROL Filtros], que lista todos os filtros personalizados, selecione o ícone de filtro (![Um ícone de filtro.](/help/images/icons/filter.png)) à esquerda do seu painel. Em seguida, para aplicar os efeitos nos insights do painel, escolha uma opção no menu suspenso do filtro global e selecione **[!UICONTROL Aplicar]**.

![Um painel personalizado com a caixa de diálogo de filtro realçada.](../../../images/query-pro-mode/custom-filters.png)

## Limpar filtro global {#clear-global-filter}

Para limpar todos os filtros globais personalizados, selecione **[!UICONTROL Limpar tudo]** na caixa de diálogo [!UICONTROL Filtros].

![A caixa de diálogo Filtros com Limpar tudo realçado.](../../../images/query-pro-mode/clear-all.png)

