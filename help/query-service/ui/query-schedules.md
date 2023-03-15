---
title: Agendamentos de consulta
description: Saiba como automatizar execuções de consultas programadas, excluir ou desativar um agendamento de consultas e utilizar as opções de agendamento disponíveis por meio da interface do usuário do Adobe Experience Platform.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Agendamentos de consulta

Você pode automatizar as execuções de consulta criando programações de consulta. As consultas programadas são executadas em uma cadência personalizada para gerenciar seus dados com base na frequência, data e hora. Você também pode escolher um conjunto de dados de saída para seus resultados, se necessário. As consultas que foram salvas como um modelo podem ser agendadas no Editor de consultas.

>[!IMPORTANT]
>
>Veja a seguir uma lista de limitações para consultas programadas ao usar o Editor de consultas. Não se aplicam à [!DNL Query Service] API:<br/>Você só pode adicionar um agendamento a uma consulta que já tenha sido criada, salva e executada.<br/>Você **não é possível** adicione uma programação a uma consulta com parâmetros.<br/>Consultas programadas **não é possível** contém um bloco anônimo.

Quaisquer consultas programadas são adicionadas à lista no [!UICONTROL Consultas programadas] guia. Nesse espaço de trabalho, é possível monitorar o status de todos os trabalhos de consulta agendados por meio da interface do usuário. No [!UICONTROL Consultas programadas] guia, você pode encontrar informações importantes sobre as execuções de consulta e assinar alertas. As informações disponíveis incluem o status, os detalhes da programação e as mensagens/códigos de erro em caso de falha na execução. Consulte a [Monitorar documento de consultas programadas](./monitor-queries.md) para obter mais informações.

## Criar agendamentos de consulta {#create-schedule}

Para adicionar um agendamento a uma consulta, selecione um modelo de consulta no [!UICONTROL Modelos] ou na guia [!UICONTROL Consultas programadas] para navegar até o Editor de consultas.

Para saber como adicionar agendas usando a API, leia o [guia de endpoint de consultas programadas](../api/scheduled-queries.md).

Quando uma consulta salva é acessada pelo Editor de consultas, a variável [!UICONTROL Agendamentos] é exibida abaixo do nome da consulta. Selecionar **[!UICONTROL Agendamentos]**.

![O Editor de consultas com a guia Agendamentos realçada.](../images/ui/query-schedules/schedules-tab.png)

O espaço de trabalho de agendamentos é exibido. Selecionar **[!UICONTROL Adicionar programação]** para criar um agendamento.

![O espaço de trabalho Agendamento do Editor de Consultas com Adicionar agendamento realçado.](../images/ui/query-schedules/add-schedule.png)

A página de detalhes da programação é exibida. Nesta página, você pode escolher a frequência da consulta programada, as datas de início e término, o dia da semana em que a consulta programada será executada, bem como para qual conjunto de dados exportar a consulta.

![O painel Schedule details está destacado.](../images/ui/query-schedules/schedule-details.png)

Você pode escolher as seguintes opções para **[!UICONTROL Frequência]**:

- **[!UICONTROL Por hora]**: A consulta agendada será executada a cada hora para o período de data selecionado.
- **[!UICONTROL Diariamente]**: A consulta agendada será executada a cada X dias na hora e no período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Semanalmente]**: A consulta selecionada será executada nos dias da semana, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Mensal]**: A consulta selecionada será executada mensalmente no dia, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.
- **[!UICONTROL Anual]**: A consulta selecionada será executada todos os anos no dia, mês, hora e período de data selecionados. Observe que o horário selecionado está em **UTC**, e não o fuso horário local.

Para o conjunto de dados de saída, você tem a opção de usar um conjunto de dados existente ou criar um novo.

>[!IMPORTANT]
>
> Como você está usando um conjunto de dados existente ou criando um novo, **não** é necessário incluir `INSERT INTO` ou `CREATE TABLE AS SELECT` como parte da query, já que os conjuntos de dados já estão definidos. Incluindo `INSERT INTO` ou `CREATE TABLE AS SELECT` como parte das consultas programadas resultará em um erro.

Após confirmar todos esses detalhes, selecione **[!UICONTROL Salvar]** para criar um agendamento. Você retorna ao espaço de trabalho de agendamentos que exibe detalhes do agendamento recém-criado, incluindo a ID do agendamento, o próprio agendamento e o conjunto de dados de saída do agendamento. Você pode usar a ID de agendamento para pesquisar mais informações sobre as execuções da própria consulta agendada. Para saber mais, leia o [guia de endpoints de execução de consulta agendada](../api/runs-scheduled-queries.md).

![O espaço de trabalho de agendamentos com o agendamento recém-criado destacado.](../images/ui/query-schedules/schedules-workspace.png)

## Excluir ou desabilitar um agendamento {#delete-schedule}

Você pode excluir ou desativar um agendamento no espaço de trabalho de agendamentos. Você deve selecionar um modelo de consulta entre as opções [!UICONTROL Modelos] ou na guia [!UICONTROL Consultas programadas] para navegar até o Editor de consultas e selecionar **[!UICONTROL Agendar]** para acessar o espaço de trabalho de agendamentos.

Selecione um agendamento nas linhas de agendamentos disponíveis. Você pode usar o botão para desativar ou ativar a consulta programada.

>[!IMPORTANT]
>
>Você deve desativar o agendamento antes de excluir um agendamento de uma consulta.

Selecionar **[!UICONTROL Excluir um agendamento]** para excluir a programação desativada.

![O espaço de trabalho de agendamentos com Desativar agendamento e Excluir agendamento realçado.](../images/ui/query-schedules/delete-schedule.png)


