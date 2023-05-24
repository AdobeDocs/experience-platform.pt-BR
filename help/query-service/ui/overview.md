---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;consulta;editor de consultas;Editor de consultas;editor de consultas;
solution: Experience Platform
title: Guia da interface do usuário do Serviço de consulta
description: O Serviço de consulta da Adobe Experience Platform fornece uma interface que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por usuários em sua organização.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---

# [!DNL Query Service] Guia da interface do usuário

O ADOBE EXPERIENCE PLATFORM [!DNL Query Service] O fornece uma interface que pode ser usada para gravar e executar consultas, exibir consultas executadas anteriormente e acessar consultas salvas por usuários em sua organização. Para acessar a interface do usuário no [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Consultas]** no painel de navegação esquerdo.

## [!DNL Query Editor]

A variável [!DNL Query Editor] permite gravar e executar consultas sem usar um cliente externo. Selecionar **[!UICONTROL Criar consulta]** para abrir o [!DNL Query Editor] e crie uma nova query. Você também pode acessar a variável [!DNL Query Editor] selecionando uma consulta no campo **[!UICONTROL Log]** ou **[!UICONTROL Modelos]** guias. Selecionar uma consulta executada ou salva anteriormente abrirá a variável [!DNL Query Editor] e exibir o SQL para a consulta selecionada.

![O painel Consultas com Criar consulta realçado.](../images/ui/overview/overview.png)

[!DNL Query Editor] O fornece um espaço de edição onde você pode começar a digitar uma query. À medida que você digita, o editor preenche automaticamente as palavras reservadas SQL, as tabelas e os nomes de campo dentro das tabelas. Quando terminar de escrever o query, selecione o **Reproduzir** botão para executar a consulta. A variável **[!UICONTROL Console]** abaixo do editor mostra o que [!DNL Query Service] está fazendo no momento, indicando quando uma consulta foi retornada. A variável **[!UICONTROL Resultado]** , ao lado do Console, exibe os resultados da consulta. Consulte a [Guia do Editor de consultas](./user-guide.md) para obter mais informações sobre como usar o [!DNL Query Editor].

![Uma ampliação tendo em conta a [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Consultas programadas {#scheduled-queries}

As consultas que já foram salvas como um modelo podem ser agendadas para execução em uma cadência regular. Ao agendar uma consulta, você pode escolher a frequência de execuções, as datas de início e término, o dia da semana em que a consulta agendada é executada, bem como o conjunto de dados para o qual exportar a consulta. Os agendamentos de consulta são definidos com o Editor de consultas.

Para saber como agendar um query por meio da interface, consulte [guia de consultas programadas](./user-guide.md#scheduled-queries). Para saber como adicionar agendas usando a API, leia o [guia de endpoint de consultas programadas](../api/scheduled-queries.md).

Depois que um query for agendado, ele aparecerá na lista de consultas agendadas no [!UICONTROL Consultas programadas] guia. Detalhes completos sobre a consulta, execuções, criador e horários podem ser encontrados selecionando uma consulta agendada na lista.

![O espaço de trabalho Consultas com a guia Consultas agendadas destacada e exibindo linhas de agendamentos de consulta.](../images/ui/overview/scheduled-queries.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O campo name é o nome do template ou os primeiros caracteres da query SQL. Qualquer consulta criada por meio da interface do usuário com o Editor de consultas é nomeada no início. Se a consulta foi criada por meio da API, o nome da consulta é um trecho do SQL inicial usado para criar a consulta. |
| **[!UICONTROL Modelo]** | O nome do modelo da consulta. Selecione um nome de modelo para navegar até o Editor de consultas. O modelo de consulta é exibido no Editor de consultas para conveniência. Se não houver nome do modelo, a linha será marcada com um hífen e não haverá capacidade de redirecionar para o Editor de consultas para exibir a consulta. |
| **[!UICONTROL SQL]** | Um trecho da consulta SQL. |
| **[!UICONTROL Frequência de execução]** | Esta é a cadência na qual sua consulta está definida para execução. Os valores disponíveis são `Run once` e `Scheduled`. As consultas podem ser filtradas de acordo com a frequência de execução. |
| **[!UICONTROL Criado por]** | O nome do usuário que criou a consulta. |
| **[!UICONTROL Criado]** | O carimbo de data e hora quando a consulta foi criada, em formato UTC. |
| **[!UICONTROL Carimbo de data/hora da última execução]** | O carimbo de data e hora mais recente quando a consulta foi executada. Esta coluna destaca se uma consulta foi executada de acordo com seu agendamento atual. |
| **[!UICONTROL Status da última execução]** | O status da execução de consulta mais recente. Os três valores de status são: `successful` `failed` ou `in progress`. |

Consulte a documentação para obter mais informações sobre como [monitorar consultas por meio da interface do Serviço de consulta](./monitor-queries.md).

## Modelos {#browse}

A variável **[!UICONTROL Modelos]** A guia mostra consultas salvas por usuários em sua organização. É útil imaginá-los como projetos de consulta, já que as consultas salvas aqui ainda podem estar em construção. Consultas exibidas na **[!UICONTROL Modelos]** também são exibidas como consultas de execução na **[!UICONTROL Log]** se tiverem sido executados anteriormente por [!DNL Query Service].

![Uma exibição ampliada da guia Modelos do painel de consultas exibindo várias consultas salvas.](../images/ui/overview/templates.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O campo name é o nome da consulta criada pelo usuário ou os primeiros caracteres da consulta SQL. Qualquer consulta criada por meio da interface do usuário com o Editor de consultas é nomeada no início. Se a consulta foi criada por meio da API, o nome da consulta é um trecho do SQL inicial usado para criar a consulta. Você pode selecionar o nome da consulta para abrir a consulta na [!DNL Query Editor]. Também é possível usar a barra de pesquisa para pesquisar a variável [!UICONTROL Nome] de uma consulta. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL SQL]** | Os primeiros caracteres da consulta SQL. Passar o mouse sobre o código exibe a consulta completa. |
| **[!UICONTROL Modificado por]** | O último usuário que modificou a consulta. Qualquer usuário da organização com acesso ao [!DNL Query Service] é possível modificar consultas. |
| **[!UICONTROL Última modificação]** | A data e a hora da última modificação no query, no fuso horário do navegador. |

Consulte a [modelos de consulta](./query-templates.md) para obter mais informações sobre modelos na interface do usuário da Platform.

## Log {#log}

A variável **[!UICONTROL Log]** A guia fornece uma lista de consultas que foram executadas anteriormente. Por padrão, o log lista as consultas na cronologia reversa.

![Uma exibição ampliada da guia Log do painel Consultas exibindo uma lista de consultas em ordem cronológica inversa.](../images/ui/overview/log.png)

| Coluna | Descrição |
| --- | --- |
| **[!UICONTROL Nome]** | O nome da consulta, que consiste nos primeiros caracteres da consulta SQL. Selecione o nome do modelo para abrir a [!UICONTROL Detalhes do log de consulta] para essa execução. Você pode usar a barra de pesquisa para pesquisar pelo nome de uma consulta. As pesquisas diferenciam maiúsculas de minúsculas. |
| **[!UICONTROL Hora de início]** | A hora em que a consulta foi executada. |
| **[!UICONTROL Tempo de conclusão]** | A hora em que a execução da consulta foi concluída. |
| **[!UICONTROL Status]** | O status atual da consulta. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados de entrada usado pela consulta. Selecione o conjunto de dados para acessar a tela de detalhes do conjunto de dados de entrada. |
| **[!UICONTROL Cliente]** | O cliente usado para a consulta. |
| **[!UICONTROL Criado por]** | O nome da pessoa que criou a consulta. |

>!![Note]
Selecione o ícone de lápis (![Um lápis.](../images/ui/overview/edit-icon.png)) de qualquer linha do log de consulta para navegar até a [!DNL Query Editor]. A consulta é pré-preenchida para edição conveniente.

Consulte a [documentação dos logs de consulta](./query-logs.md) para obter mais informações sobre os arquivos de log gerados automaticamente por um evento de consulta.

## Credenciais

A variável **[!UICONTROL Credenciais]** exibe suas credenciais que expiram e que não expiram. Para obter mais informações sobre como usar essas credenciais para conexão com clientes externos, leia a [guia de credenciais](../clients/overview.md).

![O painel Queries com a guia Credenciais é realçado.](../images/ui/overview/credentials.png)

## Próximas etapas

Agora que você está familiarizado [!DNL Query Service] interface de usuário ativada [!DNL Platform], você pode acessar [!DNL Query Editor] para começar a criar seus próprios projetos de consulta para compartilhar com outros usuários em sua organização. Para obter mais informações sobre criação e execução de consultas no [!DNL Query Editor], consulte o [[!DNL Query Editor] guia do usuário](./user-guide.md).
