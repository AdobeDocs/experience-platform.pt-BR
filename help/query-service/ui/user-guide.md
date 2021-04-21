---
keywords: Experience Platform; home; tópicos populares; Editor de consultas; editor de consultas; serviço de consultas;
solution: Experience Platform
title: Guia da interface do usuário do Editor de consultas
topic-legacy: query editor
description: O Editor de consultas é uma ferramenta interativa fornecida pelo Serviço de consultas da Adobe Experience Platform, que permite gravar, validar e executar consultas de dados de experiência do cliente na interface do usuário do Experience Platform. O Editor de consultas oferece suporte ao desenvolvimento de consultas para análise e exploração de dados e permite executar consultas interativas para fins de desenvolvimento, bem como consultas não interativas para preencher conjuntos de dados no Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# [!DNL Query Editor] Guia da interface do usuário

[!DNL Query Editor] é uma ferramenta interativa fornecida pela Adobe Experience Platform  [!DNL Query Service], que permite gravar, validar e executar consultas para dados de experiência do cliente na interface do  [!DNL Experience Platform] usuário. [!DNL Query Editor] O suporta o desenvolvimento de consultas para análise e exploração de dados e permite executar consultas interativas para fins de desenvolvimento, bem como consultas não interativas para preencher conjuntos de dados no  [!DNL Experience Platform].

Para obter mais informações sobre os conceitos e os recursos de [!DNL Query Service], consulte a [Visão geral do serviço de consulta][query-service-overview]. Para saber mais sobre como navegar na interface do usuário do Serviço de query em [!DNL Platform], consulte a [Visão geral da interface do usuário do Serviço de query][query-service-ui].

## Introdução

[!DNL Query Editor] O fornece execução flexível de consultas ao conectar-se a  [!DNL Query Service], e as consultas só serão executadas enquanto essa conexão estiver ativa.

### Conectando a [!DNL Query Service]

[!DNL Query Editor] leva alguns segundos para inicializar e se conectar  [!DNL Query Service] quando é aberto. O Console informa quando ele está conectado, como mostrado abaixo. Se você tentar executar uma query antes que o editor esteja conectado, a execução será adiada até que a conexão seja concluída.

![Imagem](../images/queries/query-editor-overview/initializing-connection.png)

### Como as consultas são executadas a partir de [!DNL Query Editor]

Consultas executadas a partir de [!DNL Query Editor] são executadas interativamente. Isso significa que se você fechar o navegador ou sair, a consulta será cancelada. Isso também é verdadeiro para queries feitos para gerar conjuntos de dados de saídas de query.

## Criação de query usando [!DNL Query Editor]

Usando [!DNL Query Editor], você pode gravar, executar e salvar consultas para dados de experiência do cliente. Todas as consultas executadas em [!DNL Query Editor], ou salvas, estão disponíveis para todos os usuários em sua organização com acesso a [!DNL Query Service].

### Acesso ao [!DNL Query Editor]

Na interface [!DNL Experience Platform], clique em **[!UICONTROL Queries]** no menu de navegação esquerdo para abrir o espaço de trabalho [!DNL Query Service]. Em seguida, clique em **[!UICONTROL Create Query]** na parte superior direita da tela para começar a gravar queries. Esse link está disponível em qualquer página no espaço de trabalho [!DNL Query Service].

![Imagem](../images/queries/query-editor-overview/create-query.png)

### Gravação de queries

[!UICONTROL Query Editor] O é organizado para facilitar ao máximo a gravação de consultas. A captura de tela abaixo mostra como o editor aparece na interface do usuário, com o botão **Play** e o campo de entrada SQL realçado.

![Imagem](../images/queries/query-editor-overview/editor.png)

Para minimizar o tempo de desenvolvimento, é recomendável desenvolver as consultas com limites nas linhas retornadas. Por exemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Depois de verificar se a consulta produz a saída esperada, remova os limites e execute a consulta com `CREATE TABLE tablename AS SELECT` para gerar um conjunto de dados com a saída.

### A escrever ferramentas em [!DNL Query Editor]

- **Realce automático da sintaxe:** facilita a leitura e a organização do SQL.

![Imagem](../images/queries/query-editor-overview/syntax-highlight.png)

- **Preenchimento automático da palavra-chave SQL:** Comece a digitar sua consulta, use as teclas de seta para navegar até o termo desejado e pressione  **Enter**.

![Imagem](../images/queries/query-editor-overview/syntax-auto.png)

- **Preenchimento automático de tabela e campo:** Comece a digitar o nome  `SELECT` da tabela de onde deseja criar, use as teclas de seta para navegar até a tabela que está procurando e pressione  **Enter**. Depois que uma tabela é selecionada, o preenchimento automático reconhecerá os campos nessa tabela.

![Imagem](../images/queries/query-editor-overview/tables-auto.png)

### Detecção de erros

[!DNL Query Editor] O valida automaticamente uma query à medida que você a escreve, fornecendo validação genérica de SQL e validação de execução específica. Se um sublinhado vermelho aparecer abaixo da query (como mostrado na imagem abaixo), ele representará um erro no query.

![Imagem](../images/queries/query-editor-overview/syntax-error-highlight.png)

Quando os erros são detectados, é possível exibir as mensagens de erro específicas passando o mouse sobre o código SQL.

![Imagem](../images/queries/query-editor-overview/linting-error.png)

### Detalhes da consulta

Enquanto você está visualizando uma consulta em [!DNL Query Editor], o painel **[!UICONTROL Query Details]** fornece ferramentas para gerenciar a consulta selecionada.

![Imagem](../images/queries/query-editor-overview/query-details.png)

Esse painel permite gerar um conjunto de dados de saída diretamente da interface do usuário, excluir ou nomear a consulta exibida e exibir o código SQL em um formato fácil de copiar na guia **[!UICONTROL SQL Query]**. Esse painel também mostra metadados úteis, como a última vez que a query foi modificada e quem a modificou, se aplicável. Para gerar um conjunto de dados, clique em **[!UICONTROL Output Dataset]**. A caixa de diálogo **[!UICONTROL Output Dataset]** é exibida. Insira um nome e uma descrição, depois clique em **[!UICONTROL Run Query]**. O novo conjunto de dados é exibido na guia **[!UICONTROL Datasets]** na interface do usuário [!DNL Query Service] em [!DNL Platform].

### Salvar consultas

[!DNL Query Editor] O fornece uma função save que permite salvar um query e trabalhar nele posteriormente. Para salvar um query, clique em **[!UICONTROL Save]** no canto superior direito de [!DNL Query Editor]. Antes que uma consulta possa ser salva, um nome deve ser fornecido para a consulta usando o painel **[!UICONTROL Query Details]**.

### Como encontrar consultas anteriores

Todas as consultas executadas de [!DNL Query Editor] são capturadas na tabela Log. Você pode usar a funcionalidade de pesquisa na guia **[!UICONTROL Log]** para localizar execuções de consulta. As consultas salvas são listadas na guia **[!UICONTROL Browse]** .

Consulte a [Visão geral da interface do usuário do serviço de consulta][query-service-ui] para obter mais informações.

>[!NOTE]
>
>As consultas que não são executadas não são salvas pelo Log. Para que a consulta esteja disponível em [!DNL Query Service], ela deve ser executada ou salva em [!DNL Query Editor].

## Execução de consultas usando o Editor de consultas

Para executar uma consulta em [!DNL Query Editor], você pode inserir SQL no editor ou carregar uma consulta anterior da guia **[!UICONTROL Log]** ou **[!UICONTROL Browse]** e clicar em **Reproduzir**. O status da execução da consulta é exibido na guia **[!UICONTROL Console]** abaixo, e os dados de saída são mostrados na guia **[!UICONTROL Results]** .

### Console

O console fornece informações sobre o status e a operação de [!DNL Query Service]. O console exibe o status da conexão com [!DNL Query Service], as operações de consulta que estão sendo executadas e quaisquer mensagens de erro que resultem dessas consultas.

![Imagem](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>O console mostra apenas erros que resultaram da execução de um query. Ele não mostra erros de validação de consulta antes da execução de um query.

### Resultados da consulta

Após a conclusão de um query, os resultados são exibidos na guia **[!UICONTROL Results]**, ao lado da guia **[!UICONTROL Console]**. Esta exibição mostra a saída em tabela de seu query, exibindo até 100 linhas. Essa visualização permite verificar se o query produz a saída esperada. Para gerar um conjunto de dados com sua consulta, remova os limites nas linhas retornadas e execute a consulta com `CREATE TABLE tablename AS SELECT` para gerar um conjunto de dados com a saída. Consulte o [tutorial de geração de conjuntos de dados][query-service-create-datasets] para obter instruções sobre como gerar um conjunto de dados a partir de resultados de query em [!DNL Query Editor].

![Imagem](../images/queries/query-editor-overview/query-results.png)

## Executar consultas com vídeo tutorial [!DNL Query Service]

O vídeo a seguir mostra como executar consultas na interface do Adobe Experience Platform e em um cliente PSQL. Além disso, é demonstrado o uso de propriedades individuais em um objeto XDM, usando funções definidas pelo Adobe e usando CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Próximas etapas

Agora que você sabe quais recursos estão disponíveis em [!DNL Query Editor] e como navegar no aplicativo, é possível começar a criar suas próprias consultas diretamente em [!DNL Platform]. Para obter mais informações sobre como executar consultas SQL em relação a conjuntos de dados em [!DNL Data Lake], consulte o guia em [executar consultas][query-service-running-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
