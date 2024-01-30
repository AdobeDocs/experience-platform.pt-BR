---
title: Agendamentos de consulta
description: Saiba como automatizar execuções de consultas programadas, excluir ou desativar um agendamento de consultas e utilizar as opções de agendamento disponíveis por meio da interface do usuário do Adobe Experience Platform.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 7d2027bf315ae6e354c906e4aabf6371a92e4148
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Agendamentos de consulta

Você pode automatizar as execuções de consulta criando programações de consulta. As consultas programadas são executadas em uma cadência personalizada para gerenciar seus dados com base na frequência, data e hora. Você também pode escolher um conjunto de dados de saída para seus resultados, se necessário. As consultas que foram salvas como um modelo podem ser agendadas no Editor de consultas.

>[!IMPORTANT]
>
>Você só pode adicionar um agendamento a uma consulta que já tenha sido criada, salva e executada.

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

O espaço de trabalho de agendamentos é exibido. Selecionar **[!UICONTROL Adicionar programação]** para criar um agendamento.

![O espaço de trabalho Agendamento do Editor de Consultas com Adicionar agendamento realçado.](../images/ui/query-schedules/add-schedule.png)

### Editar os detalhes da programação {#schedule-details}

A página de detalhes da programação é exibida. Nesta página, você pode escolher a frequência da consulta programada, as datas de início e término, o dia da semana em que a consulta programada será executada, bem como para qual conjunto de dados exportar a consulta.

![O painel Schedule details está destacado.](../images/ui/query-schedules/schedule-details.png)

Você pode escolher as seguintes opções para **[!UICONTROL Frequência]**:

- **[!UICONTROL Por hora]**: A consulta agendada será executada a cada hora para o período de data selecionado.
- **[!UICONTROL Diariamente]**: A consulta agendada será executada a cada X dias na hora e no período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Semanalmente]**: A consulta selecionada será executada nos dias da semana, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Mensal]**: A consulta selecionada será executada mensalmente no dia, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Anual]**: A consulta selecionada será executada todos os anos no dia, mês, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.

Para o conjunto de dados de saída, você tem a opção de usar a opção de anexar em um conjunto de dados existente ou criar e anexar em um novo conjunto de dados. A segunda opção significa que, se você executar um query pela primeira vez e criar um conjunto de dados, qualquer execução subsequente continuará inserindo dados nesse conjunto de dados.

>[!IMPORTANT]
>
> Como você está usando um conjunto de dados existente ou criando um novo, **não** é necessário incluir `INSERT INTO` ou `CREATE TABLE AS SELECT` como parte da query, já que os conjuntos de dados já estão definidos. Incluindo `INSERT INTO` ou `CREATE TABLE AS SELECT` como parte das consultas programadas resultará em um erro.

Se você não tiver acesso a consultas parametrizadas, continue na [excluir ou desativar um agendamento](#delete-schedule) seção.

### Definir parâmetros para uma consulta parametrizada programada {#set-parameters}

>[!IMPORTANT]
>
>O recurso de interface de consulta parametrizada está disponível atualmente em um **somente versão limitada** e não está disponível para todos os clientes.

Se você estiver criando uma consulta programada para uma consulta parametrizada, deverá definir os valores de parâmetro para essas execuções de consulta.

![A seção Schedule details do workflow de criação do agendamento com a seção Query parameters destacada.](../images/ui/query-schedules/scheduled-query-parameter.png)

Após confirmar todos esses detalhes, selecione **[!UICONTROL Salvar]** para criar um agendamento. Você retorna ao espaço de trabalho de agendamentos que exibe detalhes do agendamento recém-criado, incluindo a ID do agendamento, o próprio agendamento e o conjunto de dados de saída do agendamento. Você pode usar a ID de agendamento para pesquisar mais informações sobre as execuções da própria consulta agendada. Para saber mais, leia o [guia de endpoints de execução de consulta agendada](../api/runs-scheduled-queries.md).

![O espaço de trabalho de agendamentos com o agendamento recém-criado destacado.](../images/ui/query-schedules/schedules-workspace.png)

## Exibir execuções de consulta programada {#scheduled-query-runs}

Para exibir uma lista de execuções programadas de um modelo de consulta, navegue até a [!UICONTROL Consultas programadas] e selecione um nome de template na lista disponível.

![A guia Scheduled queries com um modelo nomeado realçado.](../images/ui/query-schedules/view-scheduled-runs.png)

A lista de execuções de consulta para a consulta programada é exibida.

![A seção de detalhes do espaço de trabalho Consultas agendadas com uma lista de execuções de consulta é destacada para uma consulta agendada.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Consulte a [guia consultado agendado do monitor](./monitor-queries.md#inline-actions) para obter informações completas sobre como monitorar o status de todos os trabalhos de consulta por meio da interface.

## Excluir ou desabilitar um agendamento {#delete-schedule}

Você pode excluir ou desativar um agendamento no espaço de trabalho de agendamentos de uma consulta específica ou no [!UICONTROL Consultas programadas] espaço de trabalho que lista todas as consultas programadas.

Para acessar o [!UICONTROL Agendamentos] da consulta escolhida, você deve selecionar o nome de um modelo de consulta no campo [!UICONTROL Modelos] ou na guia [!UICONTROL Consultas programadas] guia. Isso navega até o Editor de consultas para essa consulta. No Editor de consultas, selecione **[!UICONTROL Agendamentos]** para acessar o espaço de trabalho de agendamentos.

Selecione um agendamento nas linhas de agendamentos disponíveis. Você pode usar o botão para desativar ou ativar a consulta programada.

>[!IMPORTANT]
>
>Você deve desativar o agendamento antes de excluir um agendamento de uma consulta.

Selecionar **[!UICONTROL Excluir um agendamento]** para excluir a programação desativada.

![O espaço de trabalho de agendamentos com Desativar agendamento e Excluir agendamento realçado.](../images/ui/query-schedules/delete-schedule.png)

Em alternativa, a [!UICONTROL Consultas programadas] A guia oferece uma coleção de ações integradas para cada consulta programada. As ações em linha disponíveis incluem [!UICONTROL Desativar programação] ou [!UICONTROL Ativar programação], [!UICONTROL Excluir programação], e [!UICONTROL Assinar] para alertas para a consulta agendada. Para obter instruções completas sobre como excluir ou desativar uma consulta agendada por meio da guia Consultas agendadas, consulte a [guia consultado agendado do monitor](./monitor-queries.md#inline-actions).
