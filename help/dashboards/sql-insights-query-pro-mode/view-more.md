---
title: Ver mais
description: Saiba mais sobre as diferentes opções de exibição para seus dados analisados por SQL. No painel personalizado, é possível visualizar os resultados tabulados da análise ou baixar os dados processados no formato CSV.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 87675263b817a2026741d6bdd094010831d6ea28
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# Visualizar mais {#view-more}

Depois de criar uma [insight personalizada](./overview.md) usando o [modo profissional de consulta](./overview.md#query-pro-mode), você pode exibir os dados do gráfico em vários formatos. É possível exibir um formulário tabelado dos resultados ou exportar os dados no formato CSV ou por email.

## Resultados em tabela {#tabulated-results}

Para cada gráfico criado usando o modo profissional de consulta por meio do SQL, é possível exibir os resultados tabelados de sua análise na interface do Experience Platform.

No painel personalizado, selecione as reticências (`...`) em qualquer widget para acessar as opções [!UICONTROL Exibir mais] e [!UICONTROL Exibir SQL].

![Um painel personalizado com um menu suspenso de reticências do insight e as opções Exibir mais e Exibir SQL realçadas.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Exportar {#export}

Na caixa de diálogo **[!UICONTROL Exibir mais]**, exporte os dados da tabela baixando um arquivo CSV diretamente ou enviando um link para seu email para download seguro mais tarde.

>[!IMPORTANT]
>
>Para acessar as opções de exportação, seu administrador deve conceder a permissão **[!UICONTROL Exportar Dados do Painel]**. Se o botão [!UICONTROL Exportar] estiver esmaecido, contate o administrador. Consulte a [Visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre permissões de painel.

>[!NOTE]
>
>Exportações somente para visualização não exigem a permissão [!UICONTROL Exportar Dados do Painel]. Por exemplo, exportar dados processados de seus [insights de painel personalizados no formato PDF](./export-pdf.md), ou de [insights de painel da interface do usuário da plataforma](../download.md).

### Baixar CSV {#download-csv}

Na caixa de diálogo [!UICONTROL Exibir mais], selecione **[!UICONTROL Exportar]** e escolha **[!UICONTROL Baixar CSV]** para baixar os dados do gráfico no formato CSV.

>[!NOTE]
>
>O download do CSV é limitado aos primeiros 500 registros.

![Uma caixa de diálogo exibindo uma visualização da sua insight e os resultados tabulados do seu SQL que gerou a insight.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

### Enviar como email {#send-as-email}

Para exportar mais de 500 registros, selecione **[!UICONTROL Exportar]** e escolha **[!UICONTROL Enviar como email]** na caixa de diálogo [!UICONTROL Exportar arquivo]. Essa opção envia com segurança um link de download para seu endereço de email associado à Adobe. O nome do destinatário e o endereço de email registrado do Adobe aparecem na seção [!UICONTROL Destinatários] da caixa de diálogo.

![A opção Exibir mais dados do gráfico com as opções Exportar e Enviar como email foi realçada.](../images/sql-insights-query-pro-mode/send-as-email.png)

Depois de selecionar [!UICONTROL Enviar como email], o Adobe gera um relatório e envia um email para o endereço registrado do Adobe. O email inclui um link de download seguro que requer autenticação por meio do Experience Platform.

>[!NOTE]
>
>Você deve baixar o relatório dentro de 24 horas após a geração do link; depois disso, o arquivo expira.

![A interface do usuário do Experience Platform com a caixa de diálogo de êxito Geração de arquivo exibida contendo a opção Baixar relatório.](../images/sql-insights-query-pro-mode/download-report.png)

Para proteger seus dados, o Adobe hospeda com segurança os arquivos exportados em vez de enviá-los como anexos. O Access exige autenticação por meio da interface do usuário do Experience Platform, e o Adobe verifica se o arquivo foi baixado somente pelo recipient pretendido.

Este método permite exportar **até 10.000 registros** e garante o acesso seguro a dados confidenciais.

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

Depois de ler este documento, agora você sabe como visualizar os resultados tabulados da análise SQL do gráfico personalizado e como exportar esses dados com segurança. Consulte o documento SQL de exibição para saber como [exibir o SQL por trás de seus insights personalizados](./view-sql.md).

Você também pode aprender a gerar gráficos a partir de modelos de dados existentes na interface do usuário do Adobe Experience Platform com o [guia de modo de design guiado](../standard-dashboards.md).
