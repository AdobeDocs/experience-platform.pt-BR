---
title: Ver mais
description: Saiba mais sobre as diferentes opções de exibição para seus dados analisados por SQL. No painel personalizado, é possível visualizar os resultados tabulados da análise ou baixar os dados processados no formato CSV.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Exibir mais {#view-more}

Depois de criar um [insight personalizado](./overview.md) com o [modo profissional de consulta](./overview.md#query-pro-mode), você poderá exibir os dados do seu gráfico em diferentes formatos. Você pode exibir um formulário tabulado dos resultados ou baixar os dados como um arquivo CSV para exibir em uma planilha.

## Resultados em tabela {#tabulated-results}

Para cada gráfico criado usando o modo pro de consulta por meio do SQL, é possível exibir os resultados tabelados de sua análise na interface do Experience Platform.

No painel personalizado, selecione as reticências (`...`) em qualquer widget para acessar as opções [!UICONTROL Exibir mais] e [!UICONTROL Exibir SQL].

![Um painel personalizado com um menu suspenso de reticências de insight e as opções Exibir mais e Exibir SQL destacadas.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Baixar CSV {#download-csv}

O recurso [!UICONTROL Exibir mais] exibe os pontos de dados específicos do gráfico em forma de tabela. Para simplificar o processo de compartilhamento e manipulação de dados, você pode baixar os dados processados no formato CSV nesta caixa de diálogo. Selecione **[!UICONTROL Baixar CSV]** para baixar seus dados.

>[!NOTE]
>
>O download do CSV é limitado aos primeiros 500 registros.

![Uma caixa de diálogo exibindo uma visualização do seu insight e dos resultados tabelados do SQL que gerou o insight.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

## Classificar por coluna {#sort-column}

Ao exibir resultados tabelados, você pode usar a funcionalidade de classificação para classificar por coluna em ordem crescente ou decrescente. No painel personalizado, selecione as reticências (`...`) em qualquer tabela para acessar a opção [!UICONTROL Exibir mais].

![Um painel personalizado com um menu suspenso de reticências das tabelas e a opção Exibir mais realçada.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Você pode classificar colunas selecionando o menu suspenso ao lado do nome da coluna e, em seguida, **[!UICONTROL Classificar em ordem crescente]** ou **[!UICONTROL Classificar em ordem decrescente]**.

>[!NOTE]
>
>As opções [!UICONTROL Classificar em Ordem Crescente] e [!UICONTROL Classificar em Ordem Decrescente] só aparecerão para colunas que tenham sido configuradas com a [funcionalidade de classificação](./overview.md#advanced-attributes).

![Uma lista suspensa de coluna da tabela mostrando as opções Classificar em Ordem Crescente e Classificar em Ordem Decrescente destacadas.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Redimensionar uma coluna {#resize-column}

É possível redimensionar colunas em resultados tabelados para melhorar a legibilidade dos dados. No painel personalizado, selecione as reticências (`...`) da tabela para acessar a opção [!UICONTROL Exibir mais]. Use o menu suspenso ao lado do nome da coluna para redimensioná-la e selecione **[!UICONTROL Redimensionar coluna]**.

![Uma lista suspensa de coluna da tabela mostrando a opção de coluna Redimensionar realçada.](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Selecione o controle deslizante e arraste para a esquerda ou direita para ajustar o tamanho da coluna conforme necessário.

![Uma tabela mostrando a barra de redimensionamento de coluna realçada.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Paginação de tabela {#table-pagination}

A paginação é aplicada automaticamente às tabelas no recurso [!UICONTROL Exibir mais], eliminando a necessidade de modificar manualmente as consultas SQL. Esse recurso garante que os dados sejam apresentados em um formato mais gerenciável, o que facilita o processo de navegação por grandes conjuntos de dados.

É possível ver até 500 registros por página. Para navegar pelos registros, use o **[!UICONTROL >]** localizado na parte inferior da página.

![Resultados em tabela com resultados e paginação realçados.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Próximas etapas

Depois de ler este documento, agora você sabe como visualizar os resultados tabulados da análise SQL do gráfico personalizado e baixar os dados como um arquivo CSV. Consulte o documento SQL de exibição para saber como [exibir o SQL por trás de seus insights personalizados](./view-sql.md).

Você também pode aprender a gerar gráficos a partir de modelos de dados existentes na interface do usuário do Adobe Experience Platform com o [guia de modo de design guiado](../standard-dashboards.md).
