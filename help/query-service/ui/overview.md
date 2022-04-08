---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do serviço de query
topic-legacy: guide
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 2%

---

# [!DNL Query Service] Guia da interface do usuário

A Adobe Experience Platform [!DNL Query Service] O fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS. Para acessar a interface do usuário no [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Queries]** no painel de navegação esquerdo.

## [!DNL Query Editor]

O [!DNL Query Editor] permite gravar e executar consultas sem usar um cliente externo. Selecionar **[!UICONTROL Criar Consulta]** para abrir o [!DNL Query Editor] e criar uma nova query. Você também pode acessar a variável [!DNL Query Editor] selecionando um query no **[!UICONTROL Log]** ou **[!UICONTROL Procurar]** guias. A seleção de uma consulta executada ou salva anteriormente abrirá o [!DNL Query Editor] e exibir o SQL para a query selecionada.

![O painel Consultas com a opção Criar consulta foi realçado.](../images/ui/overview/overview.png)

[!DNL Query Editor] O fornece espaço de edição, onde você pode começar a digitar uma consulta. À medida que você digita, o editor conclui automaticamente palavras, tabelas e nomes de campos reservados do SQL nas tabelas. Quando terminar de gravar seu query, selecione a variável **Reproduzir** para executar o query. O **[!UICONTROL Console]** guia abaixo do editor mostra o que [!DNL Query Service] O está fazendo no momento, indicando quando um query foi retornado. O **[!UICONTROL Resultado]** , ao lado do Console, exibe os resultados da consulta. Consulte a [Guia do Editor de consultas](./user-guide.md) para obter mais informações sobre como usar o [!DNL Query Editor].

![Um zoom na exibição da variável [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Navegar {#browse}

O **[!UICONTROL Procurar]** mostra queries salvas pelos usuários em sua organização. É útil considerar esses projetos como projetos de query, já que as consultas salvas aqui podem ainda estar em construção. Queries exibidos no **[!UICONTROL Procurar]** A guia também é exibida como consultas de execução no **[!UICONTROL Log]** se tiverem sido executados anteriormente por [!DNL Query Service].

![Uma visualização ampliada da guia Procurar do painel de Consultas exibindo várias consultas salvas.](../images/ui/overview/browse.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O nome da consulta criado pelo usuário. Você pode selecionar no nome para abrir o query no [!DNL Query Editor]. Também é possível usar a barra de pesquisa para pesquisar o Nome de uma consulta. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL SQL]** | Os primeiros caracteres da consulta SQL. Passar o mouse sobre o código exibe a consulta completa. |
| **[!UICONTROL Modificado por]** | O último usuário que modificou a query. Qualquer usuário da organização com acesso a [!DNL Query Service] O pode modificar queries. |
| **[!UICONTROL Última modificação]** | A data e a hora da última modificação do query, no fuso horário do navegador. |

## Log

O **[!UICONTROL Log]** A guia fornece uma lista de consultas que foram executadas anteriormente. Por padrão, o log lista os queries na cronologia inversa.

![Uma visualização ampliada da guia Log do painel de Consultas exibindo uma lista de consultas em ordem cronológica inversa.](../images/ui/overview/log.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O nome da consulta, que consiste nos primeiros caracteres da consulta SQL. Selecionar o nome abre a janela [!DNL Query Editor], permitindo editar o query. Você pode usar a barra de pesquisa para pesquisar o Nome de um query. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL Criado por]** | O nome da pessoa que criou o query. |
| **[!UICONTROL Cliente]** | O cliente usado para o query. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados de entrada usado pelo query. Selecione o conjunto de dados a ser acessado na tela de detalhes do conjunto de dados de entrada. |
| **[!UICONTROL Status]** | O status atual da query. |
| **[!UICONTROL Última execução]** | Quando a consulta foi executada por último. Você pode classificar a lista em ordem crescente ou decrescente selecionando a seta sobre essa coluna. |
| **[!UICONTROL Tempo de execução]** | O tempo necessário para executar o query. |

## Credenciais

O **[!UICONTROL Credenciais]** exibe suas credenciais que expiram e não expiram. Para obter mais informações sobre como usar essas credenciais para se conectar a clientes externos, leia o [guia de credenciais](../clients/overview.md).

![O painel Queries com a guia Credenciais foi realçado.](../images/ui/overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado com [!DNL Query Service] interface do usuário em [!DNL Platform], você pode acessar [!DNL Query Editor] para começar a criar seus próprios projetos de query para compartilhar com outros usuários em sua organização. Para obter mais informações sobre criação e execução de consultas em [!DNL Query Editor], consulte o [[!DNL Query Editor] guia do usuário](./user-guide.md).