---
keywords: Experience Platform;home;popular topics;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Guia do usuário do Editor de query
topic: query editor
description: O Editor de query é uma ferramenta interativa fornecida pelo Adobe Experience Platform Query Service, que permite que você grave, valide e execute query para dados de experiência do cliente na interface do usuário do Experience Platform. O Editor de query oferece suporte ao desenvolvimento de query para a exploração de análises e dados e permite que você execute query interativos para fins de desenvolvimento, bem como query não interativos para preencher conjuntos de dados no Experience Platform.
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# [!DNL Query Editor] guia do usuário

[!DNL Query Editor] é uma ferramenta interativa fornecida pela Adobe Experience Platform [!DNL Query Service], que permite gravar, validar e executar query para dados de experiência do cliente na interface do [!DNL Experience Platform] usuário. [!DNL Query Editor] O oferece suporte ao desenvolvimento de query para a exploração de análises e dados e permite que você execute query interativos para fins de desenvolvimento, bem como query não interativos para preencher conjuntos de dados em [!DNL Experience Platform].

Para obter mais informações sobre os conceitos e recursos do [!DNL Query Service], consulte a visão geral [do Serviço de][query-service-overview]Query. Para saber mais sobre como navegar na interface do usuário do Serviço de Query em [!DNL Platform], consulte a visão geral [da interface do usuário do Serviço de][query-service-ui]Query.

## Introdução

[!DNL Query Editor] fornece execução flexível de query conectando-se a [!DNL Query Service]e os query só serão executados enquanto essa conexão estiver ativa.

### Conexão com [!DNL Query Service]

[!DNL Query Editor] leva alguns segundos para inicializar e se conectar [!DNL Query Service] quando ele é aberto. O console informa quando está conectado, como mostrado abaixo. Se você tentar executar um query antes de o editor se conectar, isso atrasará a execução até que a conexão seja concluída.

![Imagem](../images/queries/query-editor-overview/initializing-connection.png)

### Como os query são executados de [!DNL Query Editor]

Query executados de [!DNL Query Editor] forma interativa. Isso significa que, se você fechar o navegador ou sair, o query será cancelado. Isso também é válido para query criados para gerar conjuntos de dados de saídas de query.

## Criação de query usando [!DNL Query Editor]

Usando [!DNL Query Editor], você pode gravar, executar e salvar query para dados de experiência do cliente. Todos os query executados em [!DNL Query Editor]ou salvos estão disponíveis para todos os usuários em sua organização com acesso ao [!DNL Query Service].

### Acesso ao [!DNL Query Editor]

Na [!DNL Experience Platform] interface do usuário, clique em **[!UICONTROL Query]** no menu de navegação esquerdo para abrir a [!DNL Query Service] área de trabalho. Em seguida, clique em **[!UICONTROL Criar Query]** na parte superior direita da tela para gravar query no start. Esse link está disponível em qualquer página da área de [!DNL Query Service] trabalho.

![Imagem](../images/queries/query-editor-overview/create-query.png)

### Gravando query

[!UICONTROL O Editor] de query é organizado para facilitar o mais possível os query de escrita. A captura de tela abaixo mostra como o editor aparece na interface do usuário, com o botão **Reproduzir** e o campo de entrada SQL destacados.

![Imagem](../images/queries/query-editor-overview/editor.png)

Para minimizar o tempo de desenvolvimento, é recomendável desenvolver query com limites nas linhas retornadas. Por exemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Depois de verificar se o query produz a saída esperada, remova os limites e execute o query com `CREATE TABLE tablename AS SELECT` o para gerar um conjunto de dados com a saída.

### Ferramentas de gravação em [!DNL Query Editor]

- **Realce automático da sintaxe:** Facilita a leitura e a organização do SQL.

![Imagem](../images/queries/query-editor-overview/syntax-highlight.png)

- **Preenchimento automático da palavra-chave SQL:** Start digitando seu query, use as teclas de seta para navegar até o termo desejado e pressione **Enter**.

![Imagem](../images/queries/query-editor-overview/syntax-auto.png)

- **Preenchimento automático de tabela e campo:** Start que digita o nome da tabela a `SELECT` partir da qual deseja inserir, use as teclas de seta para navegar até a tabela que está procurando e pressione **Enter**. Depois que uma tabela é selecionada, o preenchimento automático reconhecerá os campos nessa tabela.

![Imagem](../images/queries/query-editor-overview/tables-auto.png)

### Detecção de erros

[!DNL Query Editor] valida automaticamente um query à medida que você o escreve, fornecendo validação SQL genérica e validação de execução específica. Se um sublinhado vermelho aparecer abaixo do query (como mostrado na imagem abaixo), ele representa um erro dentro do query.

![Imagem](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando os erros são detectados, é possível visualização as mensagens de erro específicas passando o mouse sobre o código SQL.

![Imagem](../images/queries/query-editor-overview/linting-error.png)

### Detalhes do query

Enquanto você estiver visualizando um query no [!DNL Query Editor], o painel Detalhes **[!UICONTROL do]** Query fornece ferramentas para gerenciar o query selecionado.

![Imagem](../images/queries/query-editor-overview/query-details.png)

Esse painel permite gerar um conjunto de dados de saída diretamente da interface do usuário, excluir ou nomear o query exibido e visualização o código SQL em um formato fácil de copiar na guia Query **** SQL. Esse painel também mostra metadados úteis, como a última vez que o query foi modificado e quem o modificou, se aplicável. Para gerar um conjunto de dados, clique em Conjunto de Dados **[!UICONTROL de Saída]**. A caixa de diálogo **[!UICONTROL Saída de Conjunto de Dados]** é exibida. Digite um nome e uma descrição e clique em **[!UICONTROL Executar Query]**. O novo conjunto de dados é exibido na guia **[!UICONTROL Conjuntos]** de dados na interface do [!DNL Query Service] usuário em [!DNL Platform].

### Salvando query

[!DNL Query Editor] fornece uma função de gravação que permite salvar um query e trabalhar nele posteriormente. Para salvar um query, clique em **[!UICONTROL Salvar]** no canto superior direito de [!DNL Query Editor]. Para que um query possa ser salvo, um nome deve ser fornecido para o query usando o painel Detalhes **[!UICONTROL do]** Query.

### Como encontrar query anteriores

Todos os query executados de [!DNL Query Editor] são capturados na tabela Log. Você pode usar a funcionalidade de pesquisa na guia **[!UICONTROL Log]** para localizar execuções de query. Query salvos são listados na guia **[!UICONTROL Procurar]** .

Consulte a visão geral [da interface do usuário do serviço de][query-service-ui] Query para obter mais informações.

>[!NOTE]
>
>Query que não são executados não são salvos pelo Log. Para que o query esteja disponível em [!DNL Query Service], ele deve ser executado ou salvo em [!DNL Query Editor].

## Execução de query usando o Editor de Query

Para executar um query no, insira o SQL no editor ou carregue um query anterior na guia [!DNL Query Editor]Log *ou* Procurar **[!UICONTROL e clique em]** Reproduzir ****. O status da execução do query é exibido na guia **[!UICONTROL Console]** abaixo e os dados de saída são mostrados na guia **[!UICONTROL Resultados]** .

### Console

O console fornece informações sobre o status e a operação do [!DNL Query Service]. O console exibe o status da conexão com [!DNL Query Service], as operações de query que estão sendo executadas e quaisquer mensagens de erro que resultem desses query.

![Imagem](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>O console mostra somente erros que resultaram da execução de um query. Ele não mostra erros de validação de query antes da execução de um query.

### Resultados do query

Depois que um query é concluído, os resultados são exibidos na guia **[!UICONTROL Resultados]** , ao lado da guia **[!UICONTROL Console]** . Esta visualização mostra a saída tabular do seu query, exibindo até 100 linhas. Essa visualização permite verificar se o query produz a saída esperada. Para gerar um conjunto de dados com seu query, remova os limites das linhas retornadas e execute o query com `CREATE TABLE tablename AS SELECT` o para gerar um conjunto de dados com a saída. Consulte o tutorial [de datasets de][query-service-create-datasets] geração para obter instruções sobre como gerar um conjunto de dados a partir dos resultados do query [!DNL Query Editor].

![Imagem](../images/queries/query-editor-overview/query-results.png)

## Executar query com vídeo [!DNL Query Service] tutorial

O vídeo a seguir mostra como executar query na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, o uso de propriedades individuais em um objeto XDM, o uso de funções definidas pelo Adobe e o uso de CREATE TABLE AS SELECT (CTAS) são demonstrados.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Próximas etapas

Agora que você sabe em quais recursos estão disponíveis [!DNL Query Editor] e como navegar no aplicativo, é possível criar seus próprios query diretamente no aplicativo, como start [!DNL Platform]. Para obter mais informações sobre como executar query SQL em relação a conjuntos de dados em [!DNL Data Lake], consulte o guia sobre como [executar query][query-service-running-queries]. Para obter exemplos de query SQL para trabalhar com dados do Adobe Analytics e do Adobe Target, consulte a referência [de][query-service-sample-queries]exemplo de query.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
