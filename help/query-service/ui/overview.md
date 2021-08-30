---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do serviço de query
topic-legacy: guide
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# [!DNL Query Service] guia

O Adobe Experience Platform [!DNL Query Service] fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS. Para acessar a interface do usuário em [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Queries]** na navegação à esquerda.

## [!DNL Query Editor]

O [!DNL Query Editor] permite que você grave e execute consultas sem usar um cliente externo. Selecione **[!UICONTROL Criar Consulta]** para abrir o [!DNL Query Editor] e criar uma nova consulta. Você também pode acessar o [!DNL Query Editor] selecionando um query nas guias **[!UICONTROL Log]** ou **[!UICONTROL Browse]**. Selecionar uma consulta executada ou salva anteriormente abrirá [!DNL Query Editor] e exibirá o SQL da consulta selecionada.

![Imagem](../images/ui/overview/overview.png)

[!DNL Query Editor] O fornece espaço de edição, onde você pode começar a digitar uma consulta. À medida que você digita, o editor conclui automaticamente palavras, tabelas e nomes de campos reservados do SQL nas tabelas. Quando terminar de gravar seu query, selecione o botão **Play** para executar o query. A guia **[!UICONTROL Console]** abaixo do editor mostra o que [!DNL Query Service] está fazendo no momento, indicando quando uma consulta foi retornada. A guia **[!UICONTROL Result]**, ao lado do Console, exibe os resultados da consulta. Consulte o [Guia do Editor de Consultas](./user-guide.md) para obter mais informações sobre como usar o [!DNL Query Editor].

![Imagem](../images/ui/overview/query-editor.png)

## Procurar

A guia **[!UICONTROL Procurar]** mostra as consultas salvas pelos usuários em sua organização. É útil considerar esses projetos como projetos de query, já que as consultas salvas aqui podem ainda estar em construção. As consultas exibidas na guia **[!UICONTROL Browse]** também são exibidas como consultas de execução na guia **[!UICONTROL Log]** se tiverem sido executadas anteriormente por [!DNL Query Service].

![Imagem](../images/ui/overview/browse.png)

| Coluna | Descrição |
| --- | --- |
| Nome | O nome da consulta criado pelo usuário. Você pode selecionar no nome para abrir o query no [!DNL Query Editor]. Também é possível usar a barra de pesquisa para pesquisar o Nome de uma consulta. As pesquisas diferenciam maiúsculas de minúsculas. |
| SQL | Os primeiros caracteres da consulta SQL. Passar o mouse sobre o código exibe a consulta completa. |
| Modificado por | O último usuário que modificou a query. Qualquer usuário em sua organização com acesso a [!DNL Query Service] pode modificar consultas. |
| Última modificação | A data e a hora da última modificação do query, no fuso horário do navegador. |

## Log

A guia **[!UICONTROL Log]** fornece uma lista de consultas que foram executadas anteriormente. Por padrão, o log lista os queries na cronologia inversa.

![Imagem](../images/ui/overview/log.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O nome da consulta, que consiste nos primeiros caracteres da consulta SQL. Selecionar o nome abre o [!DNL Query Editor], permitindo que você edite a query. Você pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL Criado por]** | O nome da pessoa que criou o query. |
| **[!UICONTROL Cliente]** | O cliente usado para o query. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados de entrada usado pelo query. Selecione o conjunto de dados a ser acessado na tela de detalhes do conjunto de dados de entrada. |
| **[!UICONTROL Status]** | O status atual da query. |
| **[!UICONTROL Última execução]** | Quando a consulta foi executada por último. Você pode classificar a lista em ordem crescente ou decrescente selecionando a seta sobre essa coluna. |
| **[!UICONTROL Tempo de execução]** | O tempo necessário para executar o query. |

## Credenciais

A guia **[!UICONTROL Credentials]** exibe suas credenciais que estão expirando e que não estão expirando. Para obter mais informações sobre como usar essas credenciais para se conectar a clientes externos, leia o [guia de credenciais](../clients/overview.md).

![Imagem](../images/ui/overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado com a [!DNL Query Service] interface do usuário em [!DNL Platform], é possível acessar [!DNL Query Editor] para começar a criar seus próprios projetos de query para compartilhar com outros usuários em sua organização. Para obter mais informações sobre criação e execução de consultas em [!DNL Query Editor], consulte o [Guia do usuário do Editor de consultas](./user-guide.md).