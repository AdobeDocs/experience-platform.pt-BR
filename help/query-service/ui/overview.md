---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guia da interface do usuário do serviço de Query Adobe Experience Platform
topic: guide
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar query, visualização query executados anteriormente e acessar query salvos por usuários na Organização IMS.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 3%

---


# [!DNL Query Service] guia

A Adobe Experience Platform [!DNL Query Service] fornece uma interface de usuário que pode ser usada para gravar e executar query, visualização query executados anteriormente e acessar query salvos pelos usuários na Organização IMS. Para acessar a interface do usuário no [Adobe Experience Platform][platform-ui], selecione **[!UICONTROL Query]** na navegação à esquerda.

## [!DNL Query Editor]

O [!DNL Query Editor] permite que você grave e execute query sem usar um cliente externo. Clique em **[!UICONTROL Criar Query]** para abrir [!DNL Query Editor] e criar um novo query. Você também pode acessar o query selecionando-o nas guias [!DNL Query Editor] Log *[!UICONTROL ou]* Procurar ** . Selecionar um query executado ou salvo anteriormente abrirá o  [!DNL Query Editor] e exibirá o SQL do query selecionado.

![Imagem](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] fornece espaço de edição onde você pode começar a digitar um query. À medida que você digita, o editor preenche automaticamente palavras, tabelas e nomes de campos reservados do SQL dentro de tabelas. Quando terminar de gravar seu query, clique no botão **Reproduzir** para executar o query. A guia *[!UICONTROL Console]* abaixo do editor mostra o que [!DNL Query Service] está fazendo no momento, indicando quando um query foi retornado. A guia *[!UICONTROL Resultado]* , ao lado do Console, exibe os resultados do query. Consulte o guia [do Editor de][query-editor] Query para obter mais informações sobre como usar o [!DNL Query Editor].

![Imagem](../images/queries/ui-overview/query-editor.png)

## Procurar

A guia *[!UICONTROL Procurar]* mostra query salvos pelos usuários em sua organização. É útil pensar neles como projetos de query, já que query salvos aqui podem ainda estar em construção. Query exibidos na guia *[!UICONTROL Procurar]* também são exibidos como query executados na guia *[!UICONTROL Log]* se tiverem sido executados anteriormente por [!DNL Query Service].

![Imagem](../images/queries/ui-overview/browse.png)

| Coluna | Descrição |
| --- | --- |
| Nome | O nome do query criado pelo usuário. Você pode clicar no nome para abrir o query no [!DNL Query Editor]. Você também pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas distinguem maiúsculas de minúsculas. |
| SQL | Os primeiros caracteres do query SQL. Passar o mouse sobre o código exibe o query completo. |
| Modificado por | O último usuário que modificou o query. Qualquer usuário em sua organização com acesso a [!DNL Query Service] pode modificar query. |
| Última modificação | A data e a hora da última modificação do query, no fuso horário do navegador. |

## Log

A guia *[!UICONTROL Log]* fornece uma lista de query que foram executados anteriormente. Por padrão, o log lista os query em uma cronologia reversa.

![Imagem](../images/queries/ui-overview/log.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O nome do query, que consiste nos primeiros vários caracteres do query SQL. Clicar no nome abre o query, permitindo que você edite o . [!DNL Query Editor] Você pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas distinguem maiúsculas de minúsculas. |
| **[!UICONTROL Criado por]** | O nome da pessoa que criou o query. |
| **[!UICONTROL Cliente]** | O cliente usado para o query. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados de entrada usado pelo query. Clique no conjunto de dados para acessar a tela de detalhes do conjunto de dados de entrada. |
| **[!UICONTROL Status]** | O status atual do query. |
| **[!UICONTROL Última execução]** | Quando o query foi executado pela última vez. Você pode classificar a lista em ordem crescente ou decrescente clicando na seta sobre essa coluna. |
| **[!UICONTROL Tempo de execução]** | A quantidade de tempo que levou para executar o query. |

## Credenciais

A guia *[!UICONTROL Credenciais]* exibe suas [!DNL Postgres] credenciais. Clique no ícone **[!UICONTROL Copiar]** ao lado de qualquer campo para armazenar seu conteúdo no buffer do teclado. Para obter mais informações sobre como usar essas credenciais para se conectar com clientes externos, leia o guia [][connect-clients]Conectar-se com clientes.

![Imagem](../images/queries/ui-overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado com a interface do [!DNL Query Service] usuário ativada, [!DNL Platform]você pode acessar [!DNL Query Editor] o start criando seus próprios projetos de query para compartilhar com outros usuários em sua organização. Para obter mais informações sobre como criar e executar query em [!DNL Query Editor], consulte o guia [do usuário do Editor de][query-editor]Query.

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
