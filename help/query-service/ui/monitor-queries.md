---
title: Monitorar consultas programadas
description: Saiba como monitorar consultas por meio da interface do usuário do serviço de query.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 26765c7f8daadabe325d2d519543c0fcd92c7717
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---

# Monitorar consultas agendadas

O Adobe Experience Platform fornece visibilidade aprimorada para o status de todas as tarefas de consulta por meio da interface do usuário. De [!UICONTROL Consultas agendadas] agora é possível encontrar informações importantes sobre as execuções de query que incluem o status, detalhes de programação e mensagens/códigos de erro caso falhem. Também é possível assinar alertas para consultas com base em seu status por meio da interface do usuário para qualquer uma dessas consultas por meio de [!UICONTROL Consultas agendadas] guia .

## [!UICONTROL Consultas agendadas]

O [!UICONTROL Consultas agendadas] A guia fornece uma visão geral de todas as consultas programadas do CTAS e do ITAS. É possível encontrar detalhes de execução para todas as consultas programadas, bem como códigos de erro e mensagens para quaisquer consultas com falha.

Para navegar até o [!UICONTROL Consultas agendadas] guia , selecione **[!UICONTROL Queries]** na barra de navegação esquerda, seguida por **[!UICONTROL Consultas agendadas]**

![A guia Consultas agendadas no espaço de trabalho Consultas .](../images/ui/monitor-queries/scheduled-queries.png)

A tabela abaixo descreve cada coluna disponível.

>[!NOTE]
>
>O ícone de assinaturas de alerta está contido em cada linha em uma coluna sem título. Consulte a [assinaturas de alertas](#alert-subscription) para obter mais informações.

| Coluna | Descrição |
|---|---|
| **[!UICONTROL Nome]** | O campo de nome é o nome do modelo ou os primeiros caracteres da consulta SQL. Qualquer query criada por meio da interface do usuário com o Editor de consultas é nomeada no início. Se a consulta foi criada por meio da API, seu nome se torna um trecho do SQL inicial usado para criar a consulta. Selecione qualquer item no [!UICONTROL Nome] para ver uma lista de todas as execuções associadas à query. Para obter mais informações, consulte [a consulta executa detalhes da programação](#query-runs) seção. |
| **[!UICONTROL Modelo]** | O nome do modelo da consulta. Selecione um nome de modelo para navegar até o Editor de consultas. O modelo de consulta é exibido no Editor de consultas para conveniência. Se não houver um nome de modelo, a linha será marcada com um hífen e não será possível redirecionar para o Editor de consultas para exibir a consulta. |
| **[!UICONTROL SQL]** | Um trecho da consulta SQL. |
| **[!UICONTROL Executar frequência]** | Essa é a cadência na qual seu query está definido para ser executado. Os valores disponíveis são `Run once` e `Scheduled`. As consultas podem ser filtradas de acordo com sua frequência de execução. |
| **[!UICONTROL Criado por]** | O nome do usuário que criou o query. |
| **[!UICONTROL Criado]** | O carimbo de data e hora quando a consulta foi criada, no formato UTC. |
| **[!UICONTROL Carimbo de data e hora da última execução]** | O carimbo de data e hora mais recente quando a consulta foi executada. Essa coluna destaca se uma consulta foi executada de acordo com seu agendamento atual. |
| **[!UICONTROL Status da última execução]** | O status da execução mais recente da consulta. Os valores de status são: `Success`, `Failed`, `In progress`e `No runs`. |

>[!TIP]
>
>Se você navegar até o Editor de consultas, é possível selecionar **[!UICONTROL Queries]** para retornar ao [!UICONTROL Modelos] guia .

### Personalizar configurações da tabela para consultas agendadas

É possível ajustar as colunas na variável [!UICONTROL Consultas agendadas] conforme suas necessidades. Selecione o ícone de configurações (![Um ícone de configurações.](../images/ui/monitor-queries/settings-icon.png)) para abrir o [!UICONTROL Personalizar tabela] e edite as colunas disponíveis.

![O ícone Personalizar configurações da tabela.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Alterne as caixas de seleção relevantes para remover ou adicionar uma coluna da tabela. Em seguida, selecione **[!UICONTROL Aplicar]** para confirmar suas opções.

>[!NOTE]
>
>Qualquer query criada por meio da interface do usuário se torna um template nomeado como parte do processo de criação. O nome do modelo é visto na coluna de modelo. Se a consulta foi criada por meio da API, a coluna de modelo fica em branco.

![A caixa de diálogo Personalizar configurações da tabela.](../images/ui/monitor-queries/customize-table-dialog.png)

### Inscrever-se em alertas {#alert-subscription}

É possível assinar alertas da [!UICONTROL Consultas agendadas] guia . Selecione o ícone de notificação de alerta (![Um ícone de alerta.](../images/ui/monitor-queries/alerts-icon.png)) ao lado de um nome de query para abrir o [!UICONTROL Alertas] caixa de diálogo. O [!UICONTROL Alertas] inscreve-se em notificações da interface do usuário e alertas de email. Os alertas são baseados no status da query. Há três opções disponíveis: `start`, `success`e `failure`. Marque as caixas apropriadas e selecione **[!UICONTROL Salvar]** para assinar.

![A caixa de diálogo de assinaturas de alerta.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Consulte a [documentação da API de assinaturas de alertas](../api/alert-subscriptions.md) para obter mais informações.

### Filtrar consultas {#filter}

Você pode filtrar consultas com base na frequência de execução. No [!UICONTROL Consultas agendadas] selecione o ícone de filtro (![Um ícone de filtro](../images/ui/monitor-queries/filter-icon.png)) para abrir a barra lateral do filtro.

![A guia agendadas queries com o ícone de filtro realçado.](../images/ui/monitor-queries/filter-queries.png)

Selecione uma das opções **[!UICONTROL Programado]** ou **[!UICONTROL Executar uma vez]** execute caixas de seleção de filtro de frequência para filtrar a lista de consultas.

>[!NOTE]
>
>Qualquer consulta que tenha sido executada, mas não tenha sido agendada, é qualificada como [!UICONTROL Executar uma vez].

![A guia de consultas agendadas com a barra lateral de filtro realçada.](../images/ui/monitor-queries/filter-sidebar.png)

Após ativar os critérios de filtro, selecione **[!UICONTROL Ocultar filtros]** para fechar o painel de filtro.

## O query executa detalhes da programação {#query-runs}

Selecione um nome de consulta para navegar até a página de detalhes da programação. Esta exibição fornece uma lista de todas as execuções executadas como parte dessa consulta agendada. As informações fornecidas incluem a hora inicial e final, o status e o conjunto de dados usados.

![A página de detalhes do agendamento.](../images/ui/monitor-queries/schedule-details.png)

Essas informações são fornecidas em uma tabela de cinco colunas. Cada linha indica uma execução de query.

| Nome da coluna | Descrição |
|---|---|
| **[!UICONTROL ID de execução da consulta]** | A ID de execução da consulta para a execução diária. Selecione o **[!UICONTROL ID de execução da consulta]** para navegar até o [!UICONTROL Visão geral da execução de query]. |
| **[!UICONTROL Início da execução da consulta]** | O carimbo de data e hora quando o query foi executado. Está no formato UTC. |
| **[!UICONTROL Execução da consulta concluída]** | O carimbo de data e hora quando o query foi concluído. Está no formato UTC. |
| **[!UICONTROL Status]** | O status da execução mais recente da consulta. Os três valores de status são: `successful` `failed` ou `in progress`. |
| **[!UICONTROL Conjunto de dados]** | O conjunto de dados envolvido na execução. |

Os detalhes da consulta que está sendo agendada podem ser vistos no [!UICONTROL Propriedades] painel. Esse painel inclui a ID da consulta inicial, o tipo de cliente, o nome do modelo, o SQL da consulta e a cadência do agendamento.

![A página de detalhes do agendamento com o painel de propriedades realçado.](../images/ui/monitor-queries/properties-panel.png)

Selecione uma ID de execução de consulta para navegar até a página de detalhes da execução e exibir informações da consulta.

![A tela de detalhes do agendamento com uma ID de execução realçada.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Visão geral da execução de query {#query-run-overview}

O [!UICONTROL Visão geral da execução de query] O fornece informações sobre execuções individuais para esta consulta agendada e um detalhamento mais detalhado do status de execução. Esta página também inclui as informações do cliente e os detalhes de qualquer erro que possa ter causado falha na consulta.

![A tela de detalhes da execução com a seção de visão geral realçada.](../images/ui/monitor-queries/query-run-details.png)

A seção Status da consulta fornece o código de erro e a mensagem de erro caso a consulta tenha falhado.

![A tela de detalhes da execução com a seção de erros realçada.](../images/ui/monitor-queries/failed-query.png)

É possível copiar o SQL da consulta para a área de transferência nessa visualização. Selecione o ícone de cópia na parte superior direita do trecho SQL para copiar a consulta. Uma mensagem pop-up confirma que o código foi copiado.

![A tela de detalhes da execução com o ícone de cópia SQL destacado.](../images/ui/monitor-queries/copy-sql.png)

### (Versão limitada) Execute detalhes para consultas com bloco anônimo {#anonymous-block-queries}

>[!IMPORTANT]
>
>O recurso de monitoramento de query que exibe detalhes de execução de consultas de bloco anônimas está atualmente em uma versão limitada e não está disponível para todos os clientes.

Queries que usam blocos anônimos para compor suas instruções SQL são separados em suas consultas individuais. Isso permite inspecionar os detalhes de execução de cada bloco de query individualmente.

Blocos anônimos são indicados por meio de um `$$` antes da consulta. Consulte a [documento de bloco anônimo](../essential-concepts/anonymous-block.md) para saber mais sobre blocos anônimos no serviço de query.

As consultas de bloco anônimo têm guias à esquerda do status de execução. Selecione uma guia para exibir os detalhes da execução.

![A visão geral da execução de Query exibe uma consulta de bloco anônima. As várias guias do query são destacadas.](../images/ui/monitor-queries/anonymous-block-overview.png)

Caso uma consulta de bloco anônimo falhe, você pode encontrar o código de erro para esse bloco específico por meio dessa interface.

![A visão geral da execução de Query exibe uma consulta de bloco anônima com o código de erro para um único bloco destacado.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Selecionar **[!UICONTROL Query]** para retornar à tela de detalhes da programação, ou **[!UICONTROL Consultas agendadas]** para retornar ao [!UICONTROL Consultas agendadas] guia .

![A tela de detalhes da execução com Query realçada.](../images/ui/monitor-queries/return-navigation.png)
