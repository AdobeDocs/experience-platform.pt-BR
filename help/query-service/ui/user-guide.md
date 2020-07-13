---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do editor do Query do Query Service
topic: query editor
translation-type: tm+mt
source-git-commit: cc101b1a439408861961c6fcd0899ca7c48bfa04
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 1%

---


# Guia do usuário do Editor de Query

O Editor de Query é uma ferramenta interativa fornecida pelo Serviço de Query, que permite que você grave, valide e execute query para dados de experiência do cliente na interface do usuário do Experience Platform. O Editor de Query oferece suporte ao desenvolvimento de query para a exploração de análises e dados e permite que você execute query interativos para fins de desenvolvimento, bem como query não interativos para preencher conjuntos de dados no Experience Platform.

Para obter mais informações sobre os conceitos e recursos do Serviço de Query, consulte a visão geral [do Serviço de][query-service-overview]Query. Para saber mais sobre como navegar na interface do usuário do Serviço de Query no Platform, consulte a visão geral [da interface do usuário do Serviço de][query-service-ui]Query.

## Introdução

O Editor de Query fornece execução flexível de query ao conectar-se ao Serviço de Query, e os query só serão executados enquanto esta conexão estiver ativa.

### Conexão com o serviço de Query

O Editor de Query leva alguns segundos para inicializar e se conectar ao Serviço de Query quando ele é aberto. O console informa quando está conectado, como mostrado abaixo. Se você tentar executar um query antes de o editor se conectar, isso atrasará a execução até que a conexão seja concluída.

![Imagem](../images/queries/query-editor-overview/initializing-connection.png)

### Como os query são executados no Editor de Query

Query executados pelo Editor de Query são executados interativamente. Isso significa que, se você fechar o navegador ou sair, o query será cancelado. Isso também é válido para query criados para gerar conjuntos de dados de saídas de query.

## Criação de Query usando o Editor de Query

Usando o Editor de Query, você pode gravar, executar e salvar query para dados de experiência do cliente. Todos os query executados no Editor de Query, ou salvos, estão disponíveis para todos os usuários em sua organização com acesso ao Serviço de Query.

### Acessar o Editor de Query

Na interface do usuário do Experience Platform, clique em **Query** no menu de navegação esquerdo para abrir a área de trabalho do Query Service. Em seguida, clique em **Criar Query** na parte superior direita da tela para gravar query no start. Esse link está disponível em qualquer página da área de trabalho do Serviço de Query.

![Imagem](../images/queries/query-editor-overview/create-query.png)

### Gravando query

O Editor de Query é organizado para tornar os query de escrita o mais fáceis possível. A captura de tela abaixo mostra como o editor aparece na interface do usuário, com o botão **Reproduzir** e o campo de entrada SQL destacados.

![Imagem](../images/queries/query-editor-overview/editor.png)

Para minimizar o tempo de desenvolvimento, é recomendável desenvolver query com limites nas linhas retornadas. Por exemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Depois de verificar se o query produz a saída esperada, remova os limites e execute o query com `CREATE TABLE tablename AS SELECT` o para gerar um conjunto de dados com a saída.

### Ferramentas de gravação no Editor de Query

- **Realce automático da sintaxe:** Facilita a leitura e a organização do SQL.

![Imagem](../images/queries/query-editor-overview/syntax-highlight.png)

- **Preenchimento automático da palavra-chave SQL:** Start digitando seu query, use as teclas de seta para navegar até o termo desejado e pressione **Enter**.

![Imagem](../images/queries/query-editor-overview/syntax-auto.png)

- **Preenchimento automático de tabela e campo:** Start que digita o nome da tabela a `SELECT` partir da qual deseja inserir, use as teclas de seta para navegar até a tabela que está procurando e pressione **Enter**. Depois que uma tabela é selecionada, o preenchimento automático reconhecerá os campos nessa tabela.

![Imagem](../images/queries/query-editor-overview/tables-auto.png)

### Detecção de erros

O Editor de Query valida automaticamente um query à medida que você o escreve, fornecendo validação SQL genérica e validação de execução específica. Se um sublinhado vermelho aparecer abaixo do query (como mostrado na imagem abaixo), ele representa um erro dentro do query.

![Imagem](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando os erros são detectados, é possível visualização as mensagens de erro específicas passando o mouse sobre o código SQL.

![Imagem](../images/queries/query-editor-overview/linting-error.png)

### Detalhes do Query

Enquanto você exibe um query no Editor de Query, o painel Detalhes *do* Query fornece ferramentas para gerenciar o query selecionado.

![Imagem](../images/queries/query-editor-overview/query-details.png)

Esse painel permite gerar um conjunto de dados de saída diretamente da interface do usuário, excluir ou nomear o query exibido e visualização o código SQL em um formato fácil de copiar na guia Query ** SQL. Esse painel também mostra metadados úteis, como a última vez que o query foi modificado e quem o modificou, se aplicável. Para gerar um conjunto de dados, clique em Conjunto de Dados **de Saída**. A caixa de diálogo *Saída de Conjunto de Dados* é exibida. Digite um nome e uma descrição e clique em **Executar Query**. O novo conjunto de dados é exibido na guia *Conjuntos* de dados na interface do usuário do Serviço de Query no Platform.

### Salvando query

O Editor de Query fornece uma função de gravação que permite salvar um query e trabalhar nele posteriormente. Para salvar um query, clique em **Salvar** no canto superior direito do Editor de Query. Para que um query possa ser salvo, um nome deve ser fornecido para o query usando o painel Detalhes *do* Query.

### Como encontrar query anteriores

Todos os query executados no Editor de Query são capturados na tabela Log. Você pode usar a funcionalidade de pesquisa na guia *Log* para localizar execuções de query. query salvos são listados na guia *Procurar* .

Consulte a visão geral [da interface do usuário do serviço de][query-service-ui] Query para obter mais informações.

>[!NOTE]
>
>Query que não são executados não são salvos pelo Log. Para que o query esteja disponível no Serviço de Query, ele deve ser executado ou salvo no Editor de Query.

## Execução de query usando o Editor de Query

Para executar um query no Editor de Query, você pode inserir o SQL no editor ou carregar um query anterior na guia *Log* ou *Procurar* e clicar em **Reproduzir**. O status da execução do query é exibido na guia *Console* abaixo e os dados de saída são mostrados na guia *Resultados* .

### Console

O console fornece informações sobre o status e a operação do Query Service. O console exibe o status da conexão com o Serviço de Query, as operações de query que estão sendo executadas e quaisquer mensagens de erro que resultem desses query.

![Imagem](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>O console mostra somente erros que resultaram da execução de um query. Ele não mostra erros de validação de query antes da execução de um query.

### Resultados do Query

Depois que um query é concluído, os resultados são exibidos na guia *Resultados* , ao lado da guia *Console* . Esta visualização mostra a saída tabular do seu query, exibindo até 100 linhas. Essa visualização permite verificar se o query produz a saída esperada. Para gerar um conjunto de dados com seu query, remova os limites das linhas retornadas e execute o query com `CREATE TABLE tablename AS SELECT` o para gerar um conjunto de dados com a saída. Consulte o tutorial [de datasets de][query-service-create-datasets] geração para obter instruções sobre como gerar um conjunto de dados a partir dos resultados do query no Editor de Query.

![Imagem](../images/queries/query-editor-overview/query-results.png)

## Vídeo tutorial Executar query com o Query Service

O vídeo a seguir mostra como executar query na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, o uso de propriedades individuais em um objeto XDM, o uso de funções definidas pela Adobe e o uso de CREATE TABLE AS SELECT (CTAS) são demonstrados.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Próximas etapas

Agora que você sabe quais recursos estão disponíveis no Editor de Query e como navegar no aplicativo, é possível criar start diretamente no Platform. Para obter mais informações sobre como executar query SQL em relação a conjuntos de dados no Data Lake, consulte o guia sobre como [executar query][query-service-running-queries]. Para obter exemplos de query SQL para trabalhar com dados do Adobe Analytics e Adobe Target, consulte a referência [de][query-service-sample-queries]exemplo de query.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
