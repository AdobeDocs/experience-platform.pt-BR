---
title: Monitorar consultas programadas
description: Saiba como monitorar consultas por meio da interface do usuário do Serviço de consulta.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: fa871529a4136263399bad3200ee3888049d06a5
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 1%

---

# Monitorar consultas programadas

O Adobe Experience Platform oferece maior visibilidade do status de todos os trabalhos de consulta por meio da interface. No [!UICONTROL Consultas programadas] Agora é possível encontrar informações importantes sobre as execuções de consulta, que incluem status, detalhes da programação e mensagens/códigos de erro caso falhem. Também é possível assinar alertas para consultas com base em seu status por meio da interface do para qualquer uma dessas consultas por meio do [!UICONTROL Consultas programadas] guia.

## [!UICONTROL Consultas programadas]

A variável [!UICONTROL Consultas programadas] A guia fornece uma visão geral de todas as consultas de CTAS e ITAS programadas. Os detalhes da execução podem ser encontrados para todas as consultas programadas, bem como códigos de erro e mensagens para quaisquer consultas com falha.

Para navegar até o [!UICONTROL Consultas programadas] selecione **[!UICONTROL Consultas]** na barra de navegação esquerda, seguida por **[!UICONTROL Consultas programadas]**

![A guia Consultas agendadas no espaço de trabalho Consultas com Consultas agendadas e Consultas destacadas.](../images/ui/monitor-queries/scheduled-queries.png)

A tabela abaixo descreve cada coluna disponível.

>[!NOTE]
>
>O ícone de assinaturas de alerta está contido em cada linha de uma coluna sem título. Consulte a [assinaturas de alerta](#alert-subscription) para obter mais informações.

| Coluna | Descrição |
|---|---|
| **[!UICONTROL Nome]** | O campo name é o nome do template ou os primeiros caracteres da query SQL. Qualquer consulta criada por meio da interface do usuário com o Editor de consultas é nomeada no início. Se a consulta foi criada por meio da API, seu nome se torna um trecho do SQL inicial usado para criar a consulta. Para ver uma lista de todas as execuções associadas à consulta, selecione um item na lista [!UICONTROL Nome] coluna. Para obter mais informações, consulte [detalhes da programação de execuções de consulta](#query-runs) seção. |
| **[!UICONTROL Modelo]** | O nome do modelo da consulta. Selecione um nome de modelo para navegar até o Editor de consultas. O modelo de consulta é exibido no Editor de consultas para conveniência. Se não houver nome do modelo, a linha será marcada com um hífen e não haverá capacidade de redirecionar para o Editor de consultas para exibir a consulta. |
| **[!UICONTROL SQL]** | Um trecho da consulta SQL. |
| **[!UICONTROL Frequência de execução]** | A cadência na qual sua consulta está definida para execução. Os valores disponíveis são `Run once` e `Scheduled`. As consultas podem ser filtradas de acordo com a frequência de execução. |
| **[!UICONTROL Criado por]** | O nome do usuário que criou a consulta. |
| **[!UICONTROL Criado]** | O carimbo de data e hora quando a consulta foi criada, em formato UTC. |
| **[!UICONTROL Carimbo de data/hora da última execução]** | O carimbo de data e hora mais recente quando a consulta foi executada. Esta coluna destaca se uma consulta foi executada de acordo com seu agendamento atual. |
| **[!UICONTROL Status da última execução]** | O status da execução de consulta mais recente. Os valores de status são: `Success`, `Failed`, `In progress`, e `No runs`. |
| **[!UICONTROL Status do Calendário]** | O status atual da consulta agendada. Há cinco valores em potencial, [!UICONTROL Registrando], [!UICONTROL Ativo], [!UICONTROL Inativo], [!UICONTROL Excluído]e um hífen. <ul><li>O hífen indica que a consulta agendada é uma consulta única e não recorrente.</li><li>A variável [!UICONTROL Registrando] status indica que o sistema ainda está processando a criação do novo agendamento para a consulta. Observe que você não pode desativar ou excluir uma consulta programada enquanto ela estiver se registrando.</li><li>A variável [!UICONTROL Ativo] status indica que a consulta programada foi **ainda não passado** data e hora de conclusão.</li><li>A variável [!UICONTROL Inativo] status indica que a consulta programada foi **aprovado** data e hora de conclusão.</li><li>A variável [!UICONTROL Excluído] status indica que a programação de consulta foi excluída.</li></ul> |

>[!TIP]
>
>Se você navegar até o Editor de consultas, poderá selecionar **[!UICONTROL Consultas]** para retornar ao [!UICONTROL Modelos] guia.

## Personalizar configurações de tabela para consultas programadas {#customize-table}

É possível ajustar as colunas nas [!UICONTROL Consultas programadas] para atender às suas necessidades. Para abrir o [!UICONTROL Personalizar tabela] caixa de diálogo de configurações e editar colunas disponíveis, selecione o ícone de configurações (![Um ícone de configurações.](../images/ui/monitor-queries/settings-icon.png)) na parte superior direita da tela.

>[!NOTE]
>
>A variável [!UICONTROL Criado em] A coluna que se refere à data em que o agendamento foi criado fica oculta por padrão.

![A guia Consultas agendadas com o ícone Personalizar configurações de tabela está realçada.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Alterne as caixas de seleção relevantes para remover ou adicionar uma coluna da tabela. Em seguida, selecione **[!UICONTROL Aplicar]** para confirmar suas escolhas.

>[!NOTE]
>
>Qualquer consulta criada por meio da interface do usuário se torna um modelo nomeado como parte do processo de criação. O nome do template é visto na coluna template. Se a query foi criada por meio da API, a coluna de modelo está em branco.

![O diálogo Personalizar configurações da tabela.](../images/ui/monitor-queries/customize-table-dialog.png)

## Gerenciar consultas programadas com ações integradas {#inline-actions}

A variável [!UICONTROL Consultas programadas] view oferece várias ações em linha para gerenciar todas as consultas programadas de um único local. As ações em linha são indicadas em cada linha com reticências. Selecione as reticências de uma consulta agendada que você deseja gerenciar para ver as opções disponíveis em um menu pop-up. As opções disponíveis incluem [[!UICONTROL Desativar programação]](#disable) ou [!UICONTROL Ativar programação], [[!UICONTROL Excluir programação]](#delete), e [[!UICONTROL Assinar]](#alert-subscription) para consultar alertas.

![A guia Consultas agendadas com as reticências da ação em linha e o menu pop-up realçado.](../images/ui/monitor-queries/disable-inline.png)

### Desativar ou ativar uma consulta programada {#disable}

Para desativar uma consulta programada, selecione as reticências de uma consulta programada que deseja gerenciar e selecione **[!UICONTROL Desativar programação]** nas opções do menu pop-up. Uma caixa de diálogo é exibida para confirmar a ação. Selecionar **[!UICONTROL Desativar]** para confirmar suas configurações.

Quando uma consulta programada é desativada, você pode ativar a programação por meio do mesmo processo. Selecione as reticências e selecione **[!UICONTROL Ativar programação]** nas opções disponíveis.

### Excluir uma consulta agendada {#delete}

Para excluir uma consulta agendada, selecione as reticências de uma consulta agendada que deseja gerenciar e selecione **[!UICONTROL Excluir programação]** nas opções do menu pop-up. Uma caixa de diálogo é exibida para confirmar a ação. Selecionar **[!UICONTROL Excluir]** para confirmar suas configurações.

Depois que uma consulta programada é excluída, ela é **não** removida da lista de consultas agendadas. As ações em linha fornecidas pelas reticências são removidas e substituídas pelo ícone de adição de alerta esmaecido. Não é possível assinar alertas para o agendamento excluído. A linha permanece na interface do usuário para fornecer informações sobre execuções realizadas como parte da consulta programada.

![A guia Consultas agendadas com uma consulta agendada excluída e o ícone de alerta esmaecido está realçado.](../images/ui/monitor-queries/post-delete.png)

Se quiser programar execuções para esse modelo de consulta, selecione o nome do modelo na linha apropriada para navegar até o Editor de consultas e, em seguida, siga as [instruções para adicionar um agendamento a uma consulta](./query-schedules.md#create-schedule) conforme descrito na documentação.

### Assinatura de alertas {#alert-subscription}

Para assinar alertas para execuções de consultas agendadas, selecione as reticências de uma consulta agendada que deseja gerenciar e selecione **[!UICONTROL Assinar]** nas opções do menu pop-up.

A variável [!UICONTROL Alertas] será aberta. A variável [!UICONTROL Alertas] A caixa de diálogo inscreve você em notificações da interface do usuário e alertas de email. Os alertas são baseados no status da consulta. Há três opções disponíveis: `start`, `success`, e `failure`. Marque as caixas apropriadas e selecione **[!UICONTROL Salvar]** para se inscrever. Você pode assinar alertas, desde que eles não tenham uma [!UICONTROL Carimbo de data/hora da última execução] valor.

![A caixa de diálogo de assinaturas do alerta.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Consulte a [documentação da API de assinaturas de alerta](../api/alert-subscriptions.md) para obter mais informações.

### Exibir os detalhes da consulta {#query-details}

Selecione o ícone de informações (![Um ícone de informações.](../images/ui/monitor-queries/information-icon.png)) para ver o painel de detalhes da consulta. O painel de detalhes contém todas as informações relevantes sobre a consulta além dos fatos incluídos na tabela de consultas programadas. As informações adicionais incluem a ID da consulta, a data da última modificação, o SQL da consulta, a ID da programação e a programação definida atual.

![A guia Consultas agendadas com o ícone de informações e o painel de detalhes destacados.](../images/ui/monitor-queries/details-panel.png)

## Filtrar consultas {#filter}

Você pode filtrar consultas com base na frequência de execução. No [!UICONTROL Consultas programadas] , selecione o ícone de filtro (![Um ícone de filtro](../images/ui/monitor-queries/filter-icon.png)) para abrir a barra lateral do filtro.

![A guia Scheduled queries com o ícone de filtro realçado.](../images/ui/monitor-queries/filter-queries.png)

Para filtrar a lista de consultas com base em sua frequência de execução, selecione **[!UICONTROL Agendado]** ou **[!UICONTROL Executar uma vez]** filtrar caixas de seleção.

>[!NOTE]
>
>Qualquer consulta executada, mas não agendada, é qualificada como [!UICONTROL Executar uma vez].

![A guia Scheduled queries com a barra lateral de filtro realçada.](../images/ui/monitor-queries/filter-sidebar.png)

Após ativar os critérios de filtro, selecione **[!UICONTROL Ocultar filtros]** para fechar o painel de filtro.

## Detalhes do agendamento de execuções de consulta {#query-runs}

Para abrir a página de detalhes da programação, selecione um nome de consulta na [!UICONTROL Consultas programadas] guia. Essa visualização fornece uma lista de todas as execuções executadas como parte dessa consulta programada. As informações fornecidas incluem a hora de início e término, o status e o conjunto de dados usado.

![A página de detalhes da programação.](../images/ui/monitor-queries/schedule-details.png)

Essas informações são fornecidas em uma tabela de cinco colunas. Cada linha denota uma execução de consulta.

| Nome da coluna | Descrição |
|---|---|
| **[!UICONTROL ID de execução da consulta]** | A ID de execução da consulta para a execução diária. Selecione o **[!UICONTROL ID de execução da consulta]** para navegar até o [!UICONTROL Visão geral da execução da consulta]. |
| **[!UICONTROL Início da execução da consulta]** | O carimbo de data e hora quando a consulta foi executada. O carimbo de data/hora está no formato UTC. |
| **[!UICONTROL Execução de consulta concluída]** | O carimbo de data e hora quando a consulta foi concluída. O carimbo de data/hora está no formato UTC. |
| **[!UICONTROL Status]** | O status da execução de consulta mais recente. Os três valores de status são: `successful` `failed` ou `in progress`. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados envolvido na execução. |

Detalhes da consulta que está sendo agendada podem ser vistos na [!UICONTROL Propriedades] painel. Esse painel inclui a ID de consulta inicial, o tipo de cliente, o nome do modelo, o SQL de consulta e a cadência do agendamento.

![A página de detalhes da programação com o painel de propriedades realçado.](../images/ui/monitor-queries/properties-panel.png)

Selecione uma ID de execução de consulta para navegar até a página de detalhes da execução e exibir informações da consulta.

![A tela de detalhes da programação com uma ID de execução realçada.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Visão geral da execução da consulta {#query-run-overview}

A variável [!UICONTROL Visão geral da execução da consulta] fornece informações sobre execuções individuais para esta consulta programada e um detalhamento mais detalhado do status de execução. Esta página também inclui as informações do cliente e detalhes de quaisquer erros que possam ter causado a falha da consulta.

![A tela de detalhes da execução com a seção de visão geral destacada.](../images/ui/monitor-queries/query-run-details.png)

A seção status da consulta fornece o código de erro e a mensagem de erro caso a consulta tenha falhado.

![A tela de detalhes da execução com a seção de erros realçada.](../images/ui/monitor-queries/failed-query.png)

Você pode copiar o SQL da consulta para a área de transferência nessa visualização. Para copiar a query, selecione o ícone copiar na parte superior direita do trecho SQL. Uma mensagem pop-up confirma que o código foi copiado.

![A tela de detalhes da execução com o ícone de cópia SQL realçado.](../images/ui/monitor-queries/copy-sql.png)

### Executar detalhes de consultas com bloqueio anônimo {#anonymous-block-queries}

As consultas que usam blocos anônimos para compreender suas instruções SQL são separadas em suas subconsultas individuais. A separação em subconsultas permite inspecionar os detalhes da execução de cada bloco de consulta individualmente.

>[!NOTE]
>
>Os detalhes de execução de um bloco anônimo que usa o comando DROP **não** ser relatada como uma subconsulta separada. Detalhes de execução separados estão disponíveis para consultas CTAS, consultas ITAS e instruções COPY usadas como subconsultas de bloco anônimas. Os detalhes de execução do comando DROP não são suportados no momento.

Blocos anônimos são indicados pelo uso de um `$$` prefixo antes da consulta. Para saber mais sobre blocos anônimos no serviço de query, consulte [documento de bloqueio anônimo](../essential-concepts/anonymous-block.md).

As subconsultas de blocos anônimos têm guias à esquerda do status de execução. Selecione uma guia para exibir os detalhes da execução.

![A visão geral da execução da consulta que exibe uma consulta de bloco anônimo. As várias guias de query são realçadas.](../images/ui/monitor-queries/anonymous-block-overview.png)

Se um query de bloco anônimo falhar, você poderá encontrar o código de erro para esse bloco específico por meio dessa interface.

![A visão geral da execução da consulta exibindo uma consulta de bloco anônimo com o código de erro de um único bloco realçado.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Selecionar **[!UICONTROL Query]** para retornar à tela de detalhes da programação ou **[!UICONTROL Consultas programadas]** para retornar ao [!UICONTROL Consultas programadas] guia.

![A tela de detalhes da execução com Consulta realçada.](../images/ui/monitor-queries/return-navigation.png)

<!-- Details required to complete this section below:
### Run details for queries with parameterized queries {#parameterized-queries}

Queries that use parameterized values to make up the SQL statement are ... 
-->
