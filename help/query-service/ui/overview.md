---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do serviço de query
topic-legacy: guide
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 2%

---

# [!DNL Query Service] guia

O Adobe Experience Platform [!DNL Query Service] fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS. Para acessar a interface do usuário em [Adobe Experience Platform][platform-ui], selecione **[!UICONTROL Queries]** na navegação à esquerda.

## [!DNL Query Editor]

O [!DNL Query Editor] permite que você grave e execute consultas sem usar um cliente externo. Clique em **[!UICONTROL Create Query]** para abrir o [!DNL Query Editor] e criar uma nova consulta. Você também pode acessar o [!DNL Query Editor] selecionando um query nas guias **[!UICONTROL Log]** ou **[!UICONTROL Browse]**. Selecionar uma consulta executada ou salva anteriormente abrirá [!DNL Query Editor] e exibirá o SQL da consulta selecionada.

![Imagem](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] O fornece espaço de edição, onde você pode começar a digitar uma consulta. À medida que você digita, o editor preenche automaticamente as palavras, as tabelas e os nomes de campo reservados do SQL nas tabelas. Quando terminar de gravar sua consulta, clique no botão **Play** para executar a consulta. A guia **[!UICONTROL Console]** abaixo do editor mostra o que [!DNL Query Service] está fazendo no momento, indicando quando uma consulta foi retornada. A guia **[!UICONTROL Result]**, ao lado do Console, exibe os resultados da consulta. Consulte o [Guia do Editor de Consultas][query-editor] para obter mais informações sobre como usar o [!DNL Query Editor].

![Imagem](../images/queries/ui-overview/query-editor.png)

## Procurar

A guia **[!UICONTROL Browse]** mostra as consultas salvas pelos usuários em sua organização. É útil considerar esses projetos como projetos de query, já que as consultas salvas aqui podem ainda estar em construção. As consultas exibidas na guia **[!UICONTROL Browse]** também são exibidas como consultas de execução na guia **[!UICONTROL Log]** se tiverem sido executadas anteriormente por [!DNL Query Service].

![Imagem](../images/queries/ui-overview/browse.png)

| Coluna | Descrição |
| --- | --- |
| Nome | O nome da consulta criado pelo usuário. Você pode clicar no nome para abrir o query no [!DNL Query Editor]. Também é possível usar a barra de pesquisa para pesquisar o Nome de uma consulta. As pesquisas diferenciam maiúsculas de minúsculas. |
| SQL | Os primeiros caracteres da consulta SQL. Passar o mouse sobre o código exibe a consulta completa. |
| Modificado por | O último usuário que modificou a query. Qualquer usuário em sua organização com acesso a [!DNL Query Service] pode modificar consultas. |
| Última modificação | A data e a hora da última modificação do query, no fuso horário do navegador. |

## Log

A guia **[!UICONTROL Log]** fornece uma lista de consultas que foram executadas anteriormente. Por padrão, o log lista os queries na cronologia inversa.

![Imagem](../images/queries/ui-overview/log.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Name]** | O nome da consulta, que consiste nos primeiros caracteres da consulta SQL. Clicar no nome abre o [!DNL Query Editor], permitindo que você edite a query. Você pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL Created By]** | O nome da pessoa que criou o query. |
| **[!UICONTROL Client]** | O cliente usado para o query. |
| **[!UICONTROL Dataset]** | O conjunto de dados de entrada usado pelo query. Clique no conjunto de dados para ir até a tela de detalhes do conjunto de dados de entrada. |
| **[!UICONTROL Status]** | O status atual da query. |
| **[!UICONTROL Last Run]** | Quando a consulta foi executada por último. Você pode classificar a lista em ordem crescente ou decrescente clicando na seta sobre essa coluna. |
| **[!UICONTROL Run Time]** | O tempo necessário para executar o query. |

## Credenciais

A guia **[!UICONTROL Credentials]** exibe suas credenciais [!DNL Postgres]. Clique no ícone **[!UICONTROL Copy]** ao lado de qualquer campo para armazenar seu conteúdo no buffer de teclado. Para obter mais informações sobre como usar essas credenciais para se conectar com clientes externos, leia o [guia de conexão com clientes][connect-clients].

![Imagem](../images/queries/ui-overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado com a [!DNL Query Service] interface do usuário em [!DNL Platform], é possível acessar [!DNL Query Editor] para começar a criar seus próprios projetos de query para compartilhar com outros usuários em sua organização. Para obter mais informações sobre criação e execução de consultas em [!DNL Query Editor], consulte o [Guia do usuário do Editor de consultas][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
