---
title: Criar um filtro global
description: Saiba como filtrar seus insights de dados com um filtro aplicado globalmente e personalizado.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Criar um filtro global {#create-global-filter}

Para criar um filtro global, primeiro selecione **[!UICONTROL Adicionar filtro]** na exibição do painel, depois **[!UICONTROL Filtro global]** no menu suspenso.

>[!IMPORTANT]
>
>Mapeie os filtros globais para todos os gráficos. Esse não é um processo automático. Para usar um filtro global, você deve incluir um [parâmetro de consulta](../../../../query-service/ui/parameterized-queries.md) no SQL do seu gráfico, [ativar o filtro global](#enable-global-filter) no widget composer e [selecionar um valor de tempo de execução](#select-global-filter) para o parâmetro na caixa de diálogo filtro global. Consulte o manual do query pro para saber como editar seu SQL se precisar incorporar um parâmetro de consulta.

![Um painel personalizado com Adicionar filtro e seu menu suspenso realçado.](../../../images/customizable-insights/add-filter.png)

Você pode alterar rapidamente os insights fornecidos pelo SQL com filtros globais personalizados.

A variável [!UICONTROL Criar um filtro global] será aberta. A criação de um filtro global segue o mesmo processo que a criação de um insight com SQL. Primeiro, selecione um banco de dados (modelo de dados do insights) para consultar, em seguida, insira seu SQL personalizado no Editor de consultas e finalmente selecione o ícone de execução (![Um ícone de execução.](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>Você deve incluir uma ID e um valor ao criar um filtro global. Os valores de amostra permitem executar a instrução SQL e criar o gráfico. Observe que os valores de amostra fornecidos ao compor a instrução são substituídos pelos valores reais selecionados para o filtro de data ou global no tempo de execução.

Após executar o query com êxito, a guia results exibe os resultados. Selecione **[!UICONTROL Próximo]**.

![A variável [!UICONTROL Caixa de diálogo Criar um filtro global] com o menu suspenso do conjunto de dados, o ícone executar e Próximo ficam realçados.](../../../images/customizable-insights/global-filter.png)

A etapa final do fluxo de trabalho de criação do filtro global requer a adição de um rótulo para o filtro. Adicione um rótulo à **[!UICONTROL Rótulo do filtro]** e selecione um tipo de filtro na caixa suspensa.

>[!NOTE]
>
>Somente o [!UICONTROL Caixa de combinação] a opção de tipo de filtro é compatível no momento.

Finalmente, selecione **[!UICONTROL Selecionar]** para retornar à visualização de painel.

![A variável [!UICONTROL Caixa de diálogo Criar um filtro global] com Select e a entrada de texto Filter label realçada.](../../../images/customizable-insights/global-filter-label.png)

## Ativar o filtro global para cada insight {#enable-global-filter}

>[!TIP]
>
>Habilite os filtros globais em cada gráfico criado. Isso garante que os valores escolhidos como filtro global sejam refletidos em todos os gráficos.

Depois de criar o filtro global para o painel, o botão de alternância para esse filtro global fica disponível como parte do widget composer.

![O compositor de widgets com a opção Filtro global selecionada.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Verifique se o parâmetro do filtro global está incluído no SQL de cada insight.

## Selecionar um filtro global {#select-global-filter}

Para abrir o [!UICONTROL Filtros] que lista todos os filtros personalizados, selecione o ícone de filtro (![Um ícone de filtro.](../../../images/customizable-insights/filter.png)) à esquerda do painel. Em seguida, para aplicar os efeitos nos insights do painel, escolha uma opção no menu suspenso do filtro global e selecione **[!UICONTROL Aplicar]**.

![Um painel personalizado com a caixa de diálogo de filtro realçada.](../../../images/customizable-insights/custom-filters.png)
