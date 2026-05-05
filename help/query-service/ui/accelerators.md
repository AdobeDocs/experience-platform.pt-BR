---
keywords: Experience Platform;Serviço de consulta;Dados Distiller;aceleradores;consultas parametrizadas;modelos SQL
solution: Experience Platform
title: Aceleradores do Data Distiller
description: Use os aceleradores do Data Distiller para executar e agendar modelos SQL parametrizados aprovados pela Adobe na interface do usuário do Serviço de consulta. Os aceleradores são somente leitura e gerenciados pela Adobe; use **[!UICONTROL Create custom template]** para cloná-los e editá-los.
source-git-commit: 5ee579c15fc2d9954673062b08280d9060b5205a
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 0%

---

# Aceleradores do Data Distiller {#data-distiller-accelerators}

Os Data Distiller accelerators são modelos SQL parametrizados criados pela Adobe projetados para cenários analíticos comuns. Use aceleradores para executar análises comuns sem escrever SQL do zero. Os aceleradores são somente leitura e mantidos pela Adobe, garantindo a consistência em toda a organização. Se precisar modificar um, você pode cloná-lo como um modelo personalizado.

Leia este guia para saber como executar, agendar e clonar aceleradores no espaço de trabalho [!UICONTROL Queries].

>[!AVAILABILITY]
>
>Os Data Distiller Accelerators só estão disponíveis para organizações com uma SKU de Data Distiller. A guia [!UICONTROL Accelerators] e os fluxos de trabalho relacionados exigem o complemento Data Distiller. Consulte a [Visão geral do Data Distiller](../data-distiller/overview.md) ou entre em contato com seu representante da Adobe para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes de começar, verifique se você atende aos seguintes requisitos:

* Você tem acesso ao espaço de trabalho [!UICONTROL Queries] no Experience Platform.
* Você entende [como usar o Editor de consultas e executar consultas](./user-guide.md).
* Você está familiarizado com [consultas parametrizadas](./parameterized-queries.md) (espaços reservados no SQL substituídos no tempo de execução).

## Quando usar aceleradores {#when-to-use}

Use aceleradores quando precisar de SQL pré-construído para padrões analíticos comuns, como análise de funnel, médias móveis ou sobreposição de público-alvo. Se nenhum acelerador for adequado ao seu caso de uso, [escreva uma consulta personalizada no Editor de Consultas](./user-guide.md#query-authoring) ou solicite um novo acelerador (consulte [Solicitar um novo acelerador](#request-accelerator)).

Um pequeno conjunto de aceleradores abre como painéis para análise imediata, enquanto outros abrem no Editor de consultas, onde você pode executar, agendar ou adaptar a lógica. Consulte a seção [Aceleradores vinculados ao painel](#dashboard-accelerators) para descobrir como essas visualizações pré-configuradas fornecem insights sobre os dados do público-alvo.

Para começar a usar aceleradores, navegue até o espaço de trabalho **[!UICONTROL Queries]** e abra a guia **[!UICONTROL Accelerators]** ou a guia **[!UICONTROL Overview]**.

## Caminhos de descoberta do acelerador {#discovery-paths}

Você pode acessar aceleradores do espaço de trabalho Consultas de duas maneiras, dependendo se deseja o catálogo completo ou os modelos recomendados.

### Use a guia Aceleradores

Use este caminho quando quiser navegar por todos os aceleradores disponíveis. Para abrir o catálogo do acelerador completo, selecione **[!UICONTROL Queries]** na navegação à esquerda e, em seguida, selecione a guia **[!UICONTROL Accelerators]**.

O espaço de trabalho exibe uma tabela de aceleradores com nomes, visualizações SQL e carimbos de data e hora. Selecione um nome de acelerador para abri-lo no Editor de consultas.

>[!NOTE]
>
>Todos os aceleradores selecionados na guia **[!UICONTROL Accelerators]** são abertos no Editor de Consulta.

![O espaço de trabalho Queries com a guia Accelerators selecionada mostra a tabela de aceleradores.](../images/ui/accelerators/accelerators-tab-table.png)

### Use a guia Visão geral

Use este caminho quando quiser acesso rápido a aceleradores altamente recomendados. Navegue até **[!UICONTROL Queries]** e selecione a guia **[!UICONTROL Overview]**. Em seguida, selecione um cartão na seção **[!UICONTROL Recommended Data Distiller accelerators]**.

A maioria dos aceleradores é aberta no Editor de consultas. Um pequeno conjunto de aceleradores abre como painéis com visualizações pré-construídas. Se o cartão abrir um painel em vez do Editor de consultas, consulte [Aceleradores vinculados a painéis](#dashboard-accelerators).

![O espaço de trabalho Consultas com a guia Visão Geral selecionada mostra uma lista de aceleradores recomendados do Data Distiller.](../images/ui/accelerators/queries-overview-accelerators.png)

## Abrir um acelerador no Editor de consultas {#open-accelerator}

Esta seção explica o que acontece quando você abre um acelerador no Editor de consultas e as ações que você pode realizar em seguida, incluindo executar o acelerador, agendá-lo ou criar um modelo personalizado.

Depois de abrir um acelerador, você pode **executar** o acelerador para ver os resultados, **agendar** o acelerador para execução automática ou **criar um modelo personalizado** para modificar o SQL.

>[!NOTE]
>
>Quando você abre um acelerador no Editor de Consultas, o SQL é pré-carregado em um estado somente leitura e as ações da barra de ferramentas como [!UICONTROL Show results], [!UICONTROL Undo text], [!UICONTROL Format text] são desabilitadas.

O painel direito exibe metadados como **[!UICONTROL Accelerator ID]**, **[!UICONTROL Name]** e detalhes de modificação, e fornece acesso ao agendamento até **[!UICONTROL Add schedule]**.

![O Editor de Consultas com um acelerador aberto, mostrando a área SQL, a guia Parâmetros de consulta e o painel direito.](../images/ui/accelerators/accelerator-query-editor.png)

### Fornecer parâmetros e executar um acelerador {#provide-parameters-execute}

Para executar o acelerador, primeiro você deve fornecer valores para todos os parâmetros necessários. Os parâmetros usam a sintaxe `${PARAMETER_NAME}` e são exibidos na guia **[!UICONTROL Query parameters]** abaixo do editor. Por exemplo, `${START_DATE}` requer um valor de data no formato `YYYY-MM-DD` (por exemplo, `2024-01-01`), e `${AUDIENCE_ID}` requer um identificador de público-alvo específico.

Para executar um acelerador:

1. Selecione **[!UICONTROL Query parameters]** e insira um valor para cada parâmetro.
2. Selecione o ícone de reprodução (![O ícone de reprodução.](../../images/icons/play.png)) na barra de ferramentas.

O acelerador é executado e exibe resultados na guia **[!UICONTROL Results]**. Estes resultados não são mantidos para um conjunto de dados, a menos que você use **[!UICONTROL Run as CTAS]** ou agende o acelerador.

Para obter mais informações sobre consultas parametrizadas, consulte [Consultas parametrizadas no Editor de Consultas](./parameterized-queries.md).

## Resultados persistentes de um acelerador {#persist-results}

Depois de executar um acelerador e confirmar os resultados, é possível manter a saída em um conjunto de dados.

Para criar um conjunto de dados a partir dos resultados, selecione **[!UICONTROL Save]** para salvar o acelerador como modelo e, em seguida, selecione **[!UICONTROL Run as CTAS]**. A caixa de diálogo **[!UICONTROL Enter output dataset details]** é exibida. Insira um nome de conjunto de dados e uma descrição opcional, depois confirme para criar o conjunto de dados. Essa ação cria um novo conjunto de dados e grava os resultados nele.

![A caixa de diálogo [!UICONTROL Enter output dataset details] com um nome de conjunto de dados e uma descrição preenchida.](../images/ui/accelerators/output-dataset-details-dialog.png)

## Agendar um acelerador {#schedule-accelerator}

Para agendar um acelerador para execução automática com valores de parâmetro fixos, selecione **[!UICONTROL Add schedule]** no painel direito.

>[!TIP]
>
>Antes de programar, compreenda os valores de parâmetro obrigatórios. Execute o acelerador primeiro para validar os resultados.

A caixa de diálogo de configuração de programação é exibida.

![A caixa de diálogo de configuração de agendamento mostrando a frequência, o intervalo de datas, o conjunto de dados de saída e os campos de parâmetro.](../images/ui/accelerators/schedule-details.png)

Na caixa de diálogo de configuração do agendamento, você deve fornecer uma frequência, um período, um conjunto de dados de saída e valores de parâmetro novamente. Os valores de parâmetro inseridos no Editor de consultas não são transportados para a configuração de programação. Na seção **[!UICONTROL Dataset details]**, você pode optar por **[!UICONTROL Append into existing dataset]** ou **[!UICONTROL Create and append into new dataset]**. Após configurar o agendamento, o acelerador é executado automaticamente com base nas configurações e grava os resultados no conjunto de dados selecionado.

Para obter instruções detalhadas, consulte o guia [Criar um agendamento de consulta](./query-schedules.md#create-schedule).

## Criar um modelo personalizado de um acelerador {#create-custom-template}

Se você precisar modificar o SQL ou reutilizar a lógica em sua própria configuração, crie um modelo personalizado a partir de um acelerador. Primeiro, abra um acelerador no Editor de Consultas e selecione **[!UICONTROL Create custom template]**. Modifique o SQL e os detalhes conforme necessário e selecione **[!UICONTROL Save]** ou **[!UICONTROL Save and close]** para armazenar o modelo.

Depois de salvo, o template é editável e pode ser executado, programado ou usado com CTAS. O modelo é salvo na guia **[!UICONTROL Templates]**, onde é possível gerenciá-lo como qualquer outro modelo. Para obter mais informações, consulte [Modelos de consulta](./query-templates.md).

### O que muda quando você cria um modelo personalizado {#custom-template-differences}

O modelo clonado difere do acelerador original porque o SQL é editável, você pode salvar as alterações, excluir o modelo e agendá-lo. O campo **[!UICONTROL Modified by]** mostra seu nome. O modelo foi encontrado na guia **[!UICONTROL Templates]** em vez de **[!UICONTROL Accelerators]**.

## Aceleradores vinculados a painéis {#dashboard-accelerators}

Alguns aceleradores na guia **[!UICONTROL Overview]** são abertos como painéis em vez de consultas SQL. Esses aceleradores fornecem visualizações pré-criadas para analisar dados de público-alvo e não exigem entrada de parâmetros ou execução manual.

Os seguintes aceleradores abrem no espaço de trabalho **[!UICONTROL Dashboards]**:

O **[!UICONTROL Advanced Audience Overlaps]** analisa as interseções entre os públicos selecionados ou entre todo o seu conjunto de públicos para identificar padrões de sobreposição. Use esses insights para refinar a segmentação e reduzir o direcionamento redundante.

**[!UICONTROL Audience Comparison]** compara as métricas principais entre dois públicos-alvo lado a lado, incluindo tamanho, composição de identidade e alterações ao longo do tempo. Use esta exibição para avaliar as diferenças de desempenho e informar as decisões de direcionamento.

**[!UICONTROL Audience Trends]** acompanha como as métricas de público mudam ao longo do tempo, incluindo o tamanho do público e a contagem de identidades. Use essas tendências para monitorar o crescimento e avaliar o impacto das estratégias de segmentação.

**[!UICONTROL Audience Identity Overlaps]** examina como os tipos de identidade se sobrepõem dentro dos públicos selecionados para entender as relações de identidade. Use essa análise para melhorar a correção de identidade e a precisão da segmentação.

![Modo de exibição de Painel mostrando visualizações de análise de público-alvo com gráficos e filtros.](../images/ui/accelerators/dashboard-accelerator-template-example.png)

Depois que o painel for aberto, use os controles e filtros disponíveis para explorar e comparar os dados do público-alvo. Para obter mais detalhes, consulte [modelos de painel](../../dashboards/sql-insights-query-pro-mode/templates/overview.md).

## Solicitar um novo acelerador {#request-accelerator}

Se você tiver um caso de uso recorrente que não esteja coberto pelos aceleradores existentes, envie uma solicitação por meio do canal de suporte da Adobe. O Adobe avalia as solicitações com base em padrões de uso comuns e na aplicabilidade do setor.

## Próximas etapas {#next-steps}

Agora você pode usar aceleradores para executar e automatizar consultas analíticas comuns.

Para estender seus fluxos de trabalho, crie e procure [modelos de consulta](./query-templates.md#browse), crie [consultas parametrizadas](./parameterized-queries.md), agende [consultas](./query-schedules.md) ou explore [fluxos de trabalho de Serviço de Consulta](./user-guide.md).
