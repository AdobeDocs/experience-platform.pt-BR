---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia da interface do usuário do serviço de Query da Adobe Experience Platform
topic: guide
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Guia de serviço do Query

O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar query, visualizações executados anteriormente e query de acesso salvos por usuários na organização IMS. Para acessar a interface no [Adobe Experience Platform][platform-ui], selecione **Query** na navegação à esquerda.

## Editor de Query

O Editor de Query permite que você grave e execute query sem usar um cliente externo. Clique em **Criar Query** para abrir o Editor de Query e criar um novo query. Você também pode acessar o Editor de Query selecionando um query nas guias *Log* ou *Procurar* . Selecionar um query executado ou salvo anteriormente abrirá o Editor de Query e exibirá o SQL do query selecionado.

![Imagem](../images/queries/ui-overview/overview.png)

O Editor de Query fornece espaço de edição onde você pode começar a digitar um query. À medida que você digita, o editor preenche automaticamente palavras, tabelas e nomes de campos reservados do SQL dentro de tabelas. Quando terminar de gravar seu query, clique em **Reproduzir** para executar o query. A guia *Console* abaixo do editor mostra o que o Serviço de Query está fazendo no momento, indicando quando um query foi retornado. A guia *Resultado* , ao lado do Console, exibe os resultados do query. Consulte o guia [do Editor de][query-editor] Query para obter mais informações sobre como usar o editor de query.

![Imagem](../images/queries/ui-overview/query-editor.png)

## Procurar

A guia *Procurar* mostra query salvos pelos usuários em sua organização. É útil pensar neles como projetos de query, já que query salvos aqui podem ainda estar em construção. Query exibidos na guia *Procurar* também são exibidos como query executados na guia *Log* se tiverem sido executados anteriormente pelo Query Service.

![Imagem](../images/queries/ui-overview/browse.png)

| Coluna | Descrição |
| --- | --- |
| Nome | O nome do query criado pelo usuário. Você pode clicar no nome para abrir o query no Editor de Query. Você também pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas distinguem maiúsculas de minúsculas. |
| SQL | Os primeiros caracteres do query SQL. Passar o mouse sobre o código exibe o query completo. |
| Modificado por | O último usuário que modificou o query. Qualquer usuário em sua organização com acesso ao Serviço de Query pode modificar query. |
| Última modificação | A data e a hora da última modificação do query, no fuso horário do navegador. |

## Log

A guia *Log* fornece uma lista de query que foram executados anteriormente. Por padrão, o log lista os query em uma cronologia reversa.

![Imagem](../images/queries/ui-overview/log.png)

| Coluna | Descrição |
| --- | --- |
| Nome | O nome do query, que consiste nos primeiros vários caracteres do query SQL. Clicar no nome abre o Editor de Query, permitindo que você edite o query. Você pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas distinguem maiúsculas de minúsculas. |
| Criado por | O nome da pessoa que criou o query. |
| Cliente | O cliente usado para o query. |
| Conjunto de dados | O conjunto de dados de entrada usado pelo query. Clique no conjunto de dados para acessar a tela de detalhes do conjunto de dados de entrada. |
| Status | O status atual do query. |
| Última execução | Quando o query foi executado pela última vez. Você pode classificar a lista em ordem crescente ou decrescente clicando na seta sobre essa coluna. |
| Tempo de execução | A quantidade de tempo que levou para executar o query. |

## Credenciais

A guia *Credenciais* exibe suas credenciais de Postagres. Clique no ícone **Copiar** ao lado de qualquer campo para armazenar seu conteúdo no buffer do teclado. Para obter mais informações sobre como usar essas credenciais para se conectar com clientes externos, leia o guia [][connect-clients]Conectar-se com clientes.

![Imagem](../images/queries/ui-overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado com a interface do usuário do Query Service na Plataforma, você pode acessar o Editor de Query para criar seus próprios projetos de query para compartilhar com outros usuários na sua organização. Para obter mais informações sobre como criar e executar query no Editor de Query, consulte o guia [do usuário do Editor de][query-editor]Query.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
