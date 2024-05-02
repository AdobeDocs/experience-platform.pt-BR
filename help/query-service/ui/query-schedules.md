---
title: Agendamentos de consulta
description: Saiba como automatizar execuções de consultas programadas, excluir ou desativar um agendamento de consultas e utilizar as opções de agendamento disponíveis por meio da interface do usuário do Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 0%

---

# Agendamentos de consulta

Você pode automatizar as execuções de consulta criando programações de consulta. As consultas programadas são executadas em uma cadência personalizada para gerenciar seus dados com base na frequência, data e hora. Você também pode escolher um conjunto de dados de saída para seus resultados, se necessário. As consultas que foram salvas como um modelo podem ser agendadas no Editor de consultas.

>[!IMPORTANT]
>
>Você só pode adicionar um agendamento a uma consulta que já foi criada e salva.

Quaisquer consultas programadas são adicionadas à lista no [!UICONTROL Consultas programadas] guia. Nesse espaço de trabalho, é possível monitorar o status de todos os trabalhos de consulta agendados por meio da interface do usuário. No [!UICONTROL Consultas programadas] guia, você pode encontrar informações importantes sobre as execuções de consulta e assinar alertas. As informações disponíveis incluem o status, os detalhes da programação e as mensagens/códigos de erro em caso de falha na execução. Consulte a [Monitorar documento de consultas programadas](./monitor-queries.md) para obter mais informações.

Esse fluxo de trabalho abrange o processo de agendamento na interface do usuário do serviço de consulta. Para saber como adicionar agendas usando a API, leia o [guia de endpoint de consultas programadas](../api/scheduled-queries.md).

## Criar um agendamento de consulta {#create-schedule}

Para agendar uma consulta, selecione um modelo de consulta no [!UICONTROL Modelos] ou na guia [!UICONTROL Modelo] coluna da [!UICONTROL Consultas programadas] guia. A seleção do nome do modelo leva você ao Editor de consultas.

Se você acessar uma consulta salva no Editor de consultas, poderá criar uma programação para a consulta ou exibir a programação da consulta no painel de detalhes.

>[!TIP]
>
>Selecionar **[!UICONTROL Exibir programação]** para navegar até o espaço de trabalho agendamentos e ver as execuções de consultas agendadas rapidamente.

![O Editor de consultas com [!UICONTROL Exibir programação] e [!UICONTROL Adicionar programação] destacado.](../images/ui/query-schedules/view-add-schedule.png)

Selecionar **[!UICONTROL Adicionar programação]** para navegar até o [página de detalhes da programação](#schedule-details).

Como alternativa, selecione o **[!UICONTROL Agendamentos]** abaixo do nome do query.

![O Editor de consultas com a guia Agendamentos realçada.](../images/ui/query-schedules/schedules-tab.png)

O espaço de trabalho de agendamentos é exibido. A interface do usuário exibe uma lista de todas as execuções agendadas às quais o modelo está associado. Selecionar **[!UICONTROL Adicionar programação]** para criar um agendamento.

![O espaço de trabalho Agendamento do Editor de Consultas com Adicionar agendamento realçado.](../images/ui/query-schedules/add-schedule.png)

### Adicionar detalhes da programação {#schedule-details}

A página de detalhes da programação é exibida. Nesta página, você pode editar diversos detalhes da consulta programada. Os detalhes incluem o [frequência e dia da semana da consulta agendada](#scheduled-query-frequency) executar, as datas de início e término, o conjunto de dados para o qual exportar os resultados e [alertas de status de consulta](#alerts-for-query-status).

![O painel Schedule details está destacado.](../images/ui/query-schedules/schedule-details.png)

#### Frequência de consulta agendada {#scheduled-query-frequency}

Você pode escolher as seguintes opções para **[!UICONTROL Frequência]**:

- **[!UICONTROL Por hora]**: A consulta agendada será executada a cada hora para o período de data selecionado.
- **[!UICONTROL Diariamente]**: A consulta agendada será executada a cada X dias na hora e no período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Semanalmente]**: A consulta selecionada será executada nos dias da semana, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Mensal]**: A consulta selecionada será executada mensalmente no dia, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Anual]**: A consulta selecionada será executada todos os anos no dia, mês, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.

### Fornecer detalhes do conjunto de dados {#dataset-details}

Gerencie os resultados da consulta anexando os dados a um conjunto de dados existente ou criando um novo conjunto de dados e anexando os dados a ele.

Selecionar **[!UICONTROL Criar e anexar em um novo conjunto de dados]** para criar um conjunto de dados ao executar um query pela primeira vez. As execuções subsequentes continuam a inserir dados nesse conjunto de dados. Por fim, forneça um nome e uma descrição para o conjunto de dados.

>[!IMPORTANT]
>
> Como você está usando um conjunto de dados existente ou criando um novo, **não** é necessário incluir `INSERT INTO` ou `CREATE TABLE AS SELECT` como parte da query, já que os conjuntos de dados já estão definidos. Incluindo `INSERT INTO` ou `CREATE TABLE AS SELECT` como parte das consultas programadas resultará em um erro.

![O painel Detalhes do agendamento com detalhes do conjunto de dados e a variável [!UICONTROL Criar e anexar em um novo conjunto de dados] opções realçadas.](../images/ui/query-schedules/dataset-details-create-and-append.png)

Como alternativa, selecione **[!UICONTROL Anexar ao conjunto de dados existente]** seguido pelo ícone do conjunto de dados (![O ícone do conjunto de dados.](../images/ui/query-schedules/dataset-icon.png)).

![O painel Detalhes do agendamento com detalhes do conjunto de dados e Anexar ao conjunto de dados existente realçado.](../images/ui/query-schedules/dataset-details-existing.png)

A variável **[!UICONTROL Selecionar conjunto de dados de saída]** será exibida.

Em seguida, navegue pelos conjuntos de dados existentes ou use o campo de pesquisa para filtrar as opções. Selecione a linha do conjunto de dados que deseja usar. Os detalhes do conjunto de dados são exibidos no painel à direita. Selecionar **[!UICONTROL Concluído]** para confirmar sua escolha.

![A caixa de diálogo Selecionar conjunto de dados de saída com o campo de pesquisa, uma linha de conjunto de dados, e Concluído realçado.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Colocar consultas em quarentena se elas falharem continuamente {#quarantine}

Ao criar um agendamento, você pode inscrever seu query no recurso de quarentena para proteger recursos do sistema e evitar possíveis interrupções. O recurso de quarentena identifica e isola automaticamente as consultas que falham repetidamente colocando-as em um [!UICONTROL Em quarentena] estado. Colocando consultas em quarentena após dez falhas consecutivas, é possível intervir, revisar e corrigir problemas antes de permitir mais execuções. Isso ajuda a manter a eficiência operacional e a integridade dos dados.

![O espaço de trabalho Calendários de Consultas com [!UICONTROL Quarentena de consulta] realçado e Sim selecionado.](../images/ui/query-schedules/quarantine-enroll.png)

Depois que uma consulta é inscrita no recurso de quarentena, você pode assinar alertas para essa alteração de status de consulta. Se uma consulta programada não estiver inscrita na quarentena, ela não aparecerá como uma opção em [a janela de Alertas](./monitor-queries.md#alert-subscription).

Você também pode inscrever uma consulta agendada no recurso de quarentena a partir das ações em linha do [!UICONTROL Consultas programadas] guia. Consulte a [documentação de consultas do monitor](./monitor-queries.md#alert-subscription) para obter mais detalhes.

### Definir alertas para um status de consulta agendada {#alerts-for-query-status}

Você também pode assinar alertas de consulta como parte das configurações de consulta programada. Isso significa que você receberá notificações sobre uma alteração no status do query. Os alertas podem ser recebidos como notificações pop-up ou emails. As opções de alerta de estado de consulta disponíveis incluem início, sucesso e falha. Marque a caixa de seleção para assinar alertas para esse status de consulta agendada.

![O painel Schedule details com as opções de Alerta é realçado.](../images/ui/query-editor/alerts.png)

Para obter uma visão geral dos alertas no Adobe Experience Platform, incluindo a estrutura de como as regras de alerta são definidas, consulte [visão geral dos alertas](../../observability/alerts/overview.md). Para obter orientação sobre como gerenciar alertas e regras de alerta na interface do Adobe Experience Platform, consulte [Guia da interface de alertas](../../observability/alerts/ui.md).

### Definir parâmetros para uma consulta parametrizada programada {#set-parameters}

>[!IMPORTANT]
>
>O recurso de interface de consulta parametrizada está disponível atualmente em um **somente versão limitada** e não está disponível para todos os clientes. Se você não tiver acesso a consultas parametrizadas, continue na [excluir ou desativar um agendamento](#delete-schedule) seção.

Se você estiver criando uma consulta programada para uma consulta parametrizada, deverá definir os valores de parâmetro para essas execuções de consulta.

![A seção Schedule details do workflow de criação do agendamento com a seção Query parameters destacada.](../images/ui/query-schedules/scheduled-query-parameter.png)

Depois de confirmar os detalhes da programação, selecione **[!UICONTROL Salvar]** para criar um agendamento. Você retornará à guia Agendamentos do modelo. Este espaço de trabalho exibe detalhes do agendamento recém-criado, incluindo a ID do agendamento, o próprio agendamento e o conjunto de dados de saída do agendamento.

## Exibir execuções de consulta programada {#scheduled-query-runs}

Do modelo [!UICONTROL Agendamentos] selecione a ID de programação para navegar até a lista de execuções de consulta para a sua consulta recém-programada.

![O espaço de trabalho de agendamentos com o agendamento recém-criado destacado.](../images/ui/query-schedules/schedules-workspace.png)

Como alternativa, para exibir uma lista de execuções programadas de um modelo de consulta, navegue até a **[!UICONTROL Consultas programadas]** e selecione um nome de template na lista disponível.

![A guia Scheduled queries com um modelo nomeado realçado.](../images/ui/query-schedules/view-scheduled-runs.png)

A lista de execuções de consulta para a consulta programada é exibida.

![A seção de detalhes do espaço de trabalho Consultas agendadas com uma lista de execuções de consulta é destacada para uma consulta agendada.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Consulte a [guia consultado agendado do monitor](./monitor-queries.md#inline-actions) para obter informações completas sobre como monitorar o status de todos os trabalhos de consulta por meio da interface.

Selecione um **[!UICONTROL ID de execução da consulta]** na lista para navegar até a visão geral da execução da consulta. Para uma discriminação completa da informação disponível sobre a [visão geral da execução da consulta](./monitor-queries.md#query-run-overview), consulte a documentação de consultas agendadas do monitor.

Para monitorar consultas programadas usando a API do Serviço de consulta, consulte a [guia de endpoints de execução de consulta agendada](../api/runs-scheduled-queries.md).

## Ativar, desativar ou excluir um agendamento {#delete-schedule}

Você pode ativar, desativar ou deletar um agendamento do espaço de trabalho de agendamentos de uma determinada consulta ou do [!UICONTROL Consultas programadas] espaço de trabalho que lista todas as consultas programadas.

Para acessar o [!UICONTROL Agendamentos] da consulta escolhida, você deve selecionar o nome de um modelo de consulta no campo [!UICONTROL Modelos] ou na guia [!UICONTROL Consultas programadas] guia. Isso navega até o Editor de consultas para essa consulta. No Editor de consultas, selecione **[!UICONTROL Agendamentos]** para acessar o espaço de trabalho de agendamentos.

Selecione um agendamento nas linhas de agendamentos disponíveis para preencher o painel de detalhes. Use o botão para desativar (ou ativar) a consulta programada.

### Excluir consultas desabilitadas

>[!IMPORTANT]
>
>Você deve desativar o agendamento antes de excluir um agendamento de uma consulta.

![A lista de agendamentos de um modelo com o painel de detalhes realçado.](../images/ui/query-schedules/schedule-details-panel.png)

Uma caixa de diálogo de confirmação é exibida. Selecionar **[!UICONTROL Desativar]** para confirmar a ação

![A janela de confirmação Desativar a programação.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Selecionar **[!UICONTROL Excluir um agendamento]** para excluir a programação desativada.

![O espaço de trabalho de agendamentos com Excluir agendamento realçado.](../images/ui/query-schedules/delete-schedule.png)

Em alternativa, a [!UICONTROL Consultas programadas] A guia oferece uma coleção de ações integradas para cada consulta programada. As ações em linha disponíveis incluem [!UICONTROL Desativar programação] ou [!UICONTROL Ativar programação], [!UICONTROL Excluir programação], e [!UICONTROL Assinar] para alertas para a consulta agendada. Para obter instruções completas sobre como excluir ou desativar uma consulta agendada por meio da guia Consultas agendadas, consulte a [guia consultado agendado do monitor](./monitor-queries.md#inline-actions).
