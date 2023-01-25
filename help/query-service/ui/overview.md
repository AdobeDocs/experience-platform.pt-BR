---
keywords: Experience Platform, home, tópicos populares, serviço de consultas, serviço de consultas, consulta, editor de consultas, Editor de consultas, Editor de consultas, Editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do serviço de query
description: O Adobe Experience Platform Query Service fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 5a027200efc22051cca6d4c041e857b2abc7d96f
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# [!DNL Query Service] Guia da interface do usuário

A Adobe Experience Platform [!DNL Query Service] O fornece uma interface de usuário que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas pelos usuários em sua Organização IMS. Para acessar a interface do usuário no [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Queries]** no painel de navegação esquerdo.

## [!DNL Query Editor]

O [!DNL Query Editor] permite gravar e executar consultas sem usar um cliente externo. Selecionar **[!UICONTROL Criar Consulta]** para abrir o [!DNL Query Editor] e criar uma nova query. Você também pode acessar a variável [!DNL Query Editor] selecionando um query no **[!UICONTROL Log]** ou **[!UICONTROL Modelos]** guias. A seleção de uma consulta executada ou salva anteriormente abrirá o [!DNL Query Editor] e exibir o SQL para a query selecionada.

![O painel Consultas com a opção Criar consulta foi realçado.](../images/ui/overview/overview.png)

[!DNL Query Editor] O fornece espaço de edição, onde você pode começar a digitar uma consulta. À medida que você digita, o editor conclui automaticamente palavras, tabelas e nomes de campos reservados do SQL nas tabelas. Quando terminar de gravar seu query, selecione a variável **Reproduzir** para executar o query. O **[!UICONTROL Console]** guia abaixo do editor mostra o que [!DNL Query Service] O está fazendo no momento, indicando quando um query foi retornado. O **[!UICONTROL Resultado]** , ao lado do Console, exibe os resultados da consulta. Consulte a [Guia do Editor de consultas](./user-guide.md) para obter mais informações sobre como usar o [!DNL Query Editor].

![Um zoom na exibição da variável [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Consultas agendadas {#scheduled-queries}

Consultas que já foram salvas como um modelo podem ser agendadas para execução em uma cadência regular. Ao agendar um query, você pode escolher a frequência de execuções, a data de início e de término, o dia da semana em que o query agendada é executado, bem como o conjunto de dados para o qual exportar o query. As programações de query são definidas por meio do Editor de consultas.

Para saber como agendar um query por meio da interface do usuário, consulte o [guia de consultas agendadas](./user-guide.md#scheduled-queries). Para saber como adicionar agendamentos usando a API, leia o [guia do endpoint de consultas agendadas](../api/scheduled-queries.md).

Depois que um query é agendado, ele aparece na lista de consultas agendadas na [!UICONTROL Consultas agendadas] guia . Detalhes completos sobre a consulta, as execuções, o criador e os tempos podem ser encontrados ao selecionar uma consulta agendada na lista.

![O espaço de trabalho Queries com a guia Consultas agendadas foi realçado e exibiu linhas de agendamentos de consulta.](../images/ui/overview/scheduled-queries.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O campo de nome é o nome do modelo ou os primeiros caracteres da consulta SQL. Qualquer query criada por meio da interface do usuário com o Editor de consultas é nomeada no início. Se a consulta foi criada por meio da API, o nome da consulta é um trecho do SQL inicial usado para criar a consulta. |
| **[!UICONTROL Modelo]** | O nome do modelo da consulta. Selecione um nome de modelo para navegar até o Editor de consultas. O modelo de consulta é exibido no Editor de consultas para conveniência. Se não houver um nome de modelo, a linha será marcada com um hífen e não será possível redirecionar para o Editor de consultas para exibir a consulta. |
| **[!UICONTROL SQL]** | Um trecho da consulta SQL. |
| **[!UICONTROL Executar frequência]** | Essa é a cadência na qual seu query está definido para ser executado. Os valores disponíveis são `Run once` e `Scheduled`. As consultas podem ser filtradas de acordo com sua frequência de execução. |
| **[!UICONTROL Criado por]** | O nome do usuário que criou o query. |
| **[!UICONTROL Criado]** | O carimbo de data e hora quando a consulta foi criada, no formato UTC. |
| **[!UICONTROL Carimbo de data e hora da última execução]** | O carimbo de data e hora mais recente quando a consulta foi executada. Essa coluna destaca se uma consulta foi executada de acordo com seu agendamento atual. |
| **[!UICONTROL Status da última execução]** | O status da execução mais recente da consulta. Os três valores de status são: `successful` `failed` ou `in progress`. |

Consulte a documentação para obter mais informações sobre como [monitorar consultas por meio da interface do usuário do serviço de query](./monitor-queries.md).

## Modelos {#browse}

O **[!UICONTROL Modelos]** mostra queries salvas pelos usuários em sua organização. É útil considerar esses projetos como projetos de query, já que as consultas salvas aqui podem ainda estar em construção. Queries exibidos no **[!UICONTROL Modelos]** A guia também é exibida como consultas de execução no **[!UICONTROL Log]** se tiverem sido executados anteriormente por [!DNL Query Service].

![Uma visualização ampliada da guia Modelos do painel de Consultas exibindo várias consultas salvas.](../images/ui/overview/templates.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O campo name é o nome da consulta criado pelo usuário ou os primeiros caracteres da consulta SQL. Qualquer query criada por meio da interface do usuário com o Editor de consultas é nomeada no início. Se a consulta foi criada por meio da API, o nome da consulta é um trecho do SQL inicial usado para criar a consulta. Você pode selecionar o nome da consulta para abri-la no [!DNL Query Editor]. Também é possível usar a barra de pesquisa para pesquisar a variável [!UICONTROL Nome] de um query. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL SQL]** | Os primeiros caracteres da consulta SQL. Passar o mouse sobre o código exibe a consulta completa. |
| **[!UICONTROL Modificado por]** | O último usuário que modificou a query. Qualquer usuário da organização com acesso a [!DNL Query Service] O pode modificar queries. |
| **[!UICONTROL Última modificação]** | A data e a hora da última modificação do query, no fuso horário do navegador. |

Consulte a [templates de query](./query-templates.md) documentação para obter mais informações sobre modelos na interface do usuário da plataforma.

## Log {#log}

O **[!UICONTROL Log]** A guia fornece uma lista de consultas que foram executadas anteriormente. Por padrão, o log lista os queries na cronologia inversa.

![Uma visualização ampliada da guia Log do painel de Consultas exibindo uma lista de consultas em ordem cronológica inversa.](../images/ui/overview/log.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O nome da consulta, que consiste nos primeiros caracteres da consulta SQL. Selecione o nome do modelo para abrir o [!UICONTROL Detalhes do log de consultas] exibir para essa execução. Você pode usar a barra de pesquisa para pesquisar o nome de um query. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL Hora de início]** | A hora em que o query foi executado. |
| **[!UICONTROL Hora de conclusão]** | A hora em que a execução da consulta foi concluída. |
| **[!UICONTROL Status]** | O status atual da query. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados de entrada usado pelo query. Selecione o conjunto de dados a ser acessado na tela de detalhes do conjunto de dados de entrada. |
| **[!UICONTROL Cliente]** | O cliente usado para o query. |
| **[!UICONTROL Criado por]** | O nome da pessoa que criou o query. |

>!![Note]
Selecione o ícone de lápis (![Um ícone de lápis.](../images/ui/overview/edit-icon.png)) de qualquer linha do log de query para navegar até a [!DNL Query Editor]. O query é preenchido previamente para uma edição conveniente.

Consulte a [documentação dos logs de consulta](./query-logs.md) para obter mais informações sobre os arquivos de log gerados automaticamente por um evento de query.

## Credenciais

O **[!UICONTROL Credenciais]** exibe suas credenciais que expiram e não expiram. Para obter mais informações sobre como usar essas credenciais para se conectar a clientes externos, leia o [guia de credenciais](../clients/overview.md).

![O painel Queries com a guia Credenciais foi realçado.](../images/ui/overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado com [!DNL Query Service] interface do usuário em [!DNL Platform], você pode acessar [!DNL Query Editor] para começar a criar seus próprios projetos de query para compartilhar com outros usuários em sua organização. Para obter mais informações sobre criação e execução de consultas em [!DNL Query Editor], consulte o [[!DNL Query Editor] guia do usuário](./user-guide.md).
