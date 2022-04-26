---
keywords: Experience Platform, home, tópicos populares, monitorar contas, monitorar fluxos de dados, fluxos de dados, destinos
description: Os destinos permitem ativar seus dados do Adobe Experience Platform para inúmeros parceiros externos. Este tutorial fornece instruções sobre como você pode monitorar os fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.
solution: Experience Platform
title: Monitorar fluxos de dados para destinos na interface do usuário
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 1bb3db196ed603a5a9ba0dcf9d54419d36a6ed51
workflow-type: tm+mt
source-wordcount: '3190'
ht-degree: 0%

---

# Monitorar fluxos de dados para destinos na interface do usuário

Os destinos permitem ativar seus dados do Adobe Experience Platform para inúmeros parceiros externos. A plataforma facilita o processo de rastreamento do fluxo de dados para seus destinos, fornecendo transparência com fluxos de dados.

O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados, incluindo o destino para o qual os dados são ativados. Este tutorial fornece instruções sobre como monitorar os fluxos de dados diretamente no espaço de trabalho de destinos ou usar o painel de monitoramento para monitorar os fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.

## Introdução {#getting-started}

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fluxos de dados](../home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile]e para [!DNL Destinations].
   - [Execuções do fluxo de dados](../../sources/notifications.md): As execuções de fluxo de dados são trabalhos agendados recorrentes com base na configuração de frequência de fluxos de dados selecionados.
- [Destinos](../../destinations/home.md): Os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação simplificada de dados da Platform para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Monitorar fluxos de dados no espaço de trabalho Destinos {#monitor-dataflows-in-the-destinations-workspace}

No **[!UICONTROL Destinos]** na interface do usuário da plataforma, navegue até o **[!UICONTROL Procurar]** e selecione o nome de um destino que deseja visualizar.

![Selecionar exibição de destino](../assets/ui/monitor-destinations/select-destination.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página, há uma lista de fluxos de dados visualizáveis, incluindo informações sobre seu destino, nome de usuário, número de fluxos de dados e status.

Consulte a tabela a seguir para obter mais informações sobre status:

| Status | Descrição |
| ------ | ----------- |
| Ativado | O `Enabled` status indica que um fluxo de dados está ativo e exporta dados de acordo com o agendamento fornecido. |
| Desativado | O `Disabled` status indica que um fluxo de dados está inativo e não está exportando dados. |
| Processamento | O `Processing` status indica que um fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados. |
| Erro | O `Error` status indica que o processo de ativação de um fluxo de dados foi interrompido. |

### O fluxo de dados é executado para destinos de transmissão {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Detalhes da execução do fluxo de dados"
>abstract="Os detalhes de execução do fluxo de dados de destino contêm informações sobre o status de ativação do segmento e as métricas obtidas do Perfil do cliente em tempo real para gerar identidades exclusivas. Para saber mais, consulte o guia de definições de métricas."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Perfis recebidos"
>abstract="O número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identidades ativadas"
>abstract="A contagem de identidades de perfil individuais ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de segmentos exportados."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identidades excluídas"
>abstract="A contagem de registros de perfil individuais excluídos da ativação do destino selecionado com base em atributos ausentes e violação de consentimento."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Falha de identidades"
>abstract="A contagem de identidades de perfil individuais que falharam no destino selecionado. Verifique o diagnóstico de erro para obter detalhes."

Para destinos de transmissão, a variável [!UICONTROL Execuções do fluxo de dados] A guia fornece uma atualização por hora para dados de métrica em suas execuções de fluxo de dados. As estatísticas mais proeminentes rotuladas são para identidades.

As identidades representam as diferentes facetas de um perfil. Por exemplo, se um perfil contiver um número de telefone e um endereço de email, esse perfil terá duas identidades.

Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para identidades:

- **[!UICONTROL Identidades ativadas]**: O número total de identidades de perfil ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de segmentos exportados.
- **[!UICONTROL Identidades excluídas]**: O número total de identidades de perfil que são ignoradas para ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Falha de identidades]**: O número total de identidades de perfil que não estão ativadas para o destino devido a erros.

![O fluxo de dados executa detalhes para destinos de fluxo](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

- **[!UICONTROL Início da execução do fluxo de dados]**: A hora em que a execução do fluxo de dados começou. Para execuções de fluxo de dados, o Experience Platform captura métricas com base no início da execução do fluxo de dados, na forma de métricas por hora. Para execução de fluxo de dados, se um fluxo de dados for iniciado, por exemplo, às 10:30 PM, a métrica mostrará a hora de início como 10:00 PM na interface do usuário.
- **[!UICONTROL Tempo de processamento]**: O tempo que levou para a execução do fluxo de dados ser processada.
   - Para **[!UICONTROL concluído]** for executada, a métrica de tempo de processamento sempre mostrará uma hora.
   - Para execuções de fluxo de dados que ainda estão em um **[!UICONTROL processamento]** , a janela para capturar todas as métricas permanece aberta por mais de uma hora, para processar todas as métricas que correspondem à execução do fluxo de dados. Por exemplo, uma execução de fluxo de dados iniciada às 9h30 pode permanecer em um estado de processamento por uma hora e trinta minutos para capturar e processar todas as métricas. Em seguida, quando a janela de processamento for fechada e o status da execução do fluxo de dados for atualizado para **concluído**, o tempo de processamento exibido é alterado para uma hora.
- **[!UICONTROL Perfis recebidos]**: O número total de perfis recebidos no fluxo de dados.
- **[!UICONTROL Identidades ativadas]**: O número total de identidades de perfil que foram ativadas com êxito para o destino selecionado como parte da execução do fluxo de dados. Essa métrica inclui identidades que são criadas, atualizadas e removidas de segmentos exportados.
- **[!UICONTROL Identidades excluídas]**: O número total de identidades de perfil que são excluídas da ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Falha de identidades]** O número total de identidades de perfil que não estão ativadas para o destino devido a erros.
- **[!UICONTROL Taxa de ativação]**: A porcentagem de identidades recebidas que foram ativadas ou ignoradas com êxito. A fórmula a seguir demonstra como esse valor é calculado:
   ![Fórmula da taxa de ativação](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Representa o estado em que o fluxo de dados está: ou [!UICONTROL Concluído] ou [!UICONTROL Processamento]. [!UICONTROL Concluído] significa que todas as identidades para a execução do fluxo de dados correspondente foram exportadas dentro do período de uma hora. [!UICONTROL Processamento] significa que a execução do fluxo de dados ainda não foi concluída.

Para exibir os detalhes de uma execução específica do fluxo de dados, selecione a hora de início da execução na lista.

A página de detalhes de uma execução do fluxo de dados contém informações adicionais, como o número de perfis recebidos, o número de identidades ativadas, o número de identidades falhadas e o número de identidades excluídas.

![Detalhes do fluxo de dados para destinos de transmissão](../assets/ui/monitor-destinations/dataflow-details-stream.png)

A página de detalhes também exibe uma lista de identidades que falharam e identidades que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo código de erro, contagem de identidades e descrição. Por padrão, a lista exibe as identidades com falha. Para mostrar identidades ignoradas, selecione o **[!UICONTROL Identidades excluídas]** alternar.

![Registros de fluxo de dados para destinos de fluxo](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### O fluxo de dados é executado para destinos em lote {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Detalhes da execução do fluxo de dados"
>abstract="Os detalhes de execução do fluxo de dados de destino contêm informações sobre o status de ativação do segmento e as métricas obtidas do Perfil do cliente em tempo real para gerar identidades exclusivas. Para saber mais, consulte o guia de definições de métricas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="O fluxo de dados é executado para destinos de transmissão"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Perfis recebidos"
>abstract="O número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identidades ativadas"
>abstract="A contagem de identidades de perfil individuais ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de segmentos exportados."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identidades excluídas"
>abstract="A contagem de registros de perfil individuais excluídos da ativação do destino selecionado com base em atributos ausentes e violação de consentimento."

Para destinos de lote, a variável [!UICONTROL Execuções do fluxo de dados] A guia fornece dados de métrica em suas execuções de fluxo de dados. Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para identidades:

- **[!UICONTROL Identidades ativadas]**: O número total de identidades de perfil ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de segmentos exportados.
- **[!UICONTROL Identidades excluídas]**: A contagem de identidades de perfil individuais excluídas da ativação para o destino selecionado, com base nos atributos ausentes e na violação de consentimento.

![O fluxo de dados executa a exibição para destinos em lote](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

- **[!UICONTROL Início da execução do fluxo de dados]**: A hora em que a execução do fluxo de dados começou.
- **[!UICONTROL Tempo de processamento]**: O tempo que levou para a execução do fluxo de dados ser processada.
- **[!UICONTROL Perfis recebidos]**: O número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos.
- **[!UICONTROL Identidades ativadas]**: O número total de identidades de perfil que foram ativadas com êxito para o destino selecionado como parte da execução do fluxo de dados. Essa métrica inclui identidades que são criadas, atualizadas e removidas de segmentos exportados.
- **[!UICONTROL Identidades excluídas]**: O número total de identidades de perfil que são excluídas da ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Status]**: Representa o estado em que o fluxo de dados está. Pode ser um dos três estados: [!UICONTROL Sucesso], [!UICONTROL Falha]e [!UICONTROL Processamento]. [!UICONTROL Sucesso] significa que o fluxo de dados está ativo e exporta dados de acordo com o agendamento fornecido. [!UICONTROL Falha] significa que a ativação dos dados foi suspensa devido a erros. [!UICONTROL Processamento] significa que o fluxo de dados ainda não está ativo e geralmente é encontrado quando um novo fluxo de dados é criado.

Para exibir detalhes de uma execução específica do fluxo de dados, selecione a hora de início da execução na lista.

>[!NOTE]
>
>As execuções de fluxo de dados são geradas com base na frequência de agendamento do fluxo de dados de destino. É feita uma execução separada do fluxo de dados para cada [política de mesclagem](../../profile/merge-policies/overview.md) aplicada a um segmento.

A página de detalhes de um fluxo de dados, além dos detalhes mostrados na lista de fluxos de dados, exibe informações mais específicas sobre o fluxo de dados:

- **[!UICONTROL Tamanho dos dados]**: O tamanho do fluxo de dados que está sendo exportado.
- **[!UICONTROL Total de arquivos]**: O número total de arquivos exportados no fluxo de dados.
- **[!UICONTROL Última atualização]**: A hora em que a execução do fluxo de dados foi atualizada pela última vez.

![Detalhes de execução do fluxo de dados para destinos em lote](../assets/ui/monitor-destinations/dataflow-batch.png)

A página de detalhes também exibe uma lista de identidades que falharam e identidades que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo o código de erro e a descrição. Por padrão, a lista exibe as identidades com falha. Para mostrar identidades excluídas, selecione a variável **[!UICONTROL Identidades excluídas]** alternar.

![Registros de fluxo de dados para destinos em lote](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Painel de monitoramento de destinos {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="A exibição de ativação de destino contém informações sobre o status de ativação do segmento e as métricas obtidas do Perfil do cliente em tempo real para gerar identidades exclusivas."

Para acessar o [!UICONTROL Monitoramento] painel, selecione **[!UICONTROL Monitoramento]** (![ícone de monitoramento](../assets/ui/monitor-destinations/monitoring-icon.png)) no painel de navegação esquerdo. Uma vez no [!UICONTROL Monitoramento] página, selecione [!UICONTROL Destinos]. O [!UICONTROL Monitoramento] o painel contém métricas e informações sobre as tarefas de execução de destino.

>[!NOTE]
>
>A funcionalidade de monitoramento de destinos é atualmente compatível com todos os destinos no Experience Platform *Except* o [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Hubs de Eventos do Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [API HTTP](/help/destinations/catalog/streaming/http-destination.md), [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)e [Personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md) destinos.

Use o [!UICONTROL Destinos] painel para obter uma ideia geral da integridade dos fluxos de ativação. Comece obtendo insights em um nível agregado para todos os destinos de lote e fluxo e detalhe as exibições detalhadas para fluxos de dados, execuções de fluxo de dados e segmentos ativados para obter uma análise detalhada dos dados de ativação. As telas no [!UICONTROL Monitoramento] O painel fornece insights acionáveis por meio de métricas e descrições de erros para ajudar você a solucionar problemas que possam surgir em seus cenários de ativação.

No centro do painel há [!UICONTROL Ativation] , que contém métricas e gráficos que exibem dados sobre a taxa de ativação dos dados exportados para destinos de fluxo, bem como sobre falhas na execução do fluxo de dados em lote para destinos em lote.

![Gráficos de transmissão e ativação em lote](../assets/ui/monitor-destinations/dashboard-graph.png)


Por padrão, os dados exibidos contêm as informações de ativação das últimas 24 horas. Selecionar **[!UICONTROL Últimas 24 horas]** para ajustar o período de tempo dos registros exibidos. As opções disponíveis incluem **[!UICONTROL Últimas 24 horas]**, **[!UICONTROL Últimos 7 dias]** e **[!UICONTROL Últimos 30 dias]**. Como alternativa, você pode selecionar as datas na janela pop-up do calendário que aparece. Depois de selecionar as datas, selecione **[!UICONTROL Aplicar]** para ajustar o período de tempo das informações apresentadas.

>[!NOTE]
>
>A captura de tela a seguir mostra a taxa de ativação e o fluxo de dados em lote são executados nos últimos 30 dias em vez das últimas 24 horas. Pode ajustar o período de tempo selecionando **[!UICONTROL Últimos 30 dias]**.

![Alterar intervalo de datas de retrospectiva para destinos ativados](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Use o ícone de seta (![ícone de seta](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) para expandir ou descartar os cartões na parte superior da tela, que mostram informações instantâneas sobre os detalhes de ativação, com base no tipo de destino - streaming ou lote:

- **[!UICONTROL Taxa de ativação de transmissão]**: Representa a porcentagem de identidades recebidas que foram ativadas ou ignoradas com êxito. A fórmula usada para calcular essa porcentagem é descrita mais acima nesta página, na variável [O fluxo de dados é executado para destinos de transmissão](#dataflow-runs-for-streaming-destinations) seção.
- **[!UICONTROL O fluxo de dados com falha em lote é executado]**: Representa o número de execuções de fluxo de dados com falha no intervalo de tempo selecionado.

![Mostrar ou descartar cartões na parte superior da página](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

O **[!UICONTROL Ativation]** O gráfico é exibido por padrão e você pode desativá-lo para expandir a lista de destinos abaixo. Selecione o **[!UICONTROL Métricas e gráficos]** para desativar os gráficos.

O **[!UICONTROL Ativation]** O painel exibe uma lista de destinos que contêm pelo menos uma conta existente. Esta lista também inclui informações sobre perfis recebidos, identidades ativadas, falha de identidades, identidades excluídas, taxa de ativação, total de fluxos de dados com falha e a última data atualizada para esses destinos. Nem todas as métricas estão disponíveis para todos os tipos de destino. A tabela abaixo descreve quais métricas estão disponíveis por tipo de destino, transmissão ou lote.

| Métrica | Tipo de destino |
---------|----------|
| **[!UICONTROL Perfis recebidos]** | Streaming e lote |
| **[!UICONTROL Identidades ativadas]** | Streaming e lote |
| **[!UICONTROL Falha de identidades]** | Streaming |
| **[!UICONTROL Identidades excluídas]** | Streaming e lote |
| **[!UICONTROL Taxa de ativação]** | Streaming |
| **[!UICONTROL Total de fluxos de dados com falha]** | Em lote |
| **[!UICONTROL Última atualização]** | Streaming e lote |

![Dashboard de todos os destinos ativados](../assets/ui/monitor-destinations/dashboard-destinations.png)

Também é possível filtrar a lista de destinos para exibir apenas a categoria de destinos selecionada. Selecione o **[!UICONTROL Meus destinos]** e selecione o [categoria de destino](/help/destinations/destination-types.md#categories) para o qual deseja filtrar.

![Filtrar destinos usando o seletor suspenso](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Além disso, você pode inserir um destino na barra de pesquisa para isolá-lo em um único destino. Se quiser ver os fluxos de dados do destino, selecione o filtro ![filter](../assets/ui/monitor-destinations/filter-add.png) ao lado dele para ver uma lista de seus fluxos de dados ativos.

![Filtrar destinos usando a barra de pesquisa](../assets/ui/monitor-destinations/filtered-destinations.png)

Se quiser exibir todos os fluxos de dados existentes em todos os destinos, selecione **[!UICONTROL Fluxos de dados]**.

Uma lista de fluxos de dados é exibida, classificada pela última execução do fluxo de dados. Você pode ver detalhes adicionais de um fluxo de dados específico localizando o destino que deseja monitorar, selecionando o filtro ![filter](../assets/ui/monitor-destinations/filter-add.png) ao seu lado e, em seguida, selecionando o filtro ![filter](../assets/ui/monitor-destinations/filter-add.png) ao lado do fluxo de dados, você deseja obter mais informações.

![Todos os fluxos de dados destacados no painel de monitoramento](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Depois de selecionar um fluxo de dados para inspeção adicional, a página de detalhes do fluxo de dados contém um botão que permite visualizar os dados ativados no fluxo de dados, detalhados por execuções ou segmentos de fluxo de dados.

### Exibição de execuções do fluxo de dados {#dataflow-runs-view}

When **[!UICONTROL Execuções do fluxo de dados]** for selecionado, você poderá ver uma lista de execuções de fluxo de dados para o fluxo de dados selecionado e mais informações sobre cada execução.

>[!INFO]
>
>Para fluxos de dados para destinos de transmissão, uma execução de fluxo de dados é dividida em janelas por hora. Cada janela por hora gera uma ID de execução de fluxo de dados correspondente.
>
>Para fluxos de dados para destinos em lote, cada segmento tem uma execução de fluxo de dados correspondente gerada, com base na frequência agendada de ativação de segmento. Por exemplo, se você configurar uma ativação agendada diária para cinco segmentos no mesmo fluxo de dados de destino, haverá cinco execuções separadas de fluxo de dados geradas todos os dias.

![Painel de execução de fluxo](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Use o **[!UICONTROL Mostrar somente falhas]** alternar para exibir somente as execuções com falha de um fluxo de dados.

![O fluxo de dados é executado - mostrar apenas falhas é alternado](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Visualização no nível do segmento {#segment-level-view}

When **[!UICONTROL Segmentos]** for selecionado, você verá uma lista dos segmentos que foram ativados para o fluxo de dados selecionado, dentro do intervalo de tempo selecionado. Essa tela inclui informações a nível de segmento sobre as identidades ativadas, as identidades excluídas, bem como o status e a hora da última execução do fluxo de dados. Ao revisar as métricas de identidades excluídas e ativadas, é possível verificar se um segmento foi ativado ou não com êxito.

Por exemplo, você está ativando um segmento chamado &quot;Membros de fidelidade na Califórnia&quot; para um destino do Amazon S3 &quot;Membros de fidelidade da Califórnia em dezembro&quot;. Vamos supor que haja 100 perfis no segmento selecionado, mas apenas 80 em 100 perfis contêm atributos de ID de fidelidade e você definiu as regras de mapeamento de exportação como `loyalty.id` é obrigatório. Nesse caso, em um nível de segmento, você verá 80 identidades ativadas e 20 identidades excluídas.

>[!IMPORTANT]
>
>Observe as limitações atuais relacionadas às métricas no nível do segmento:
>- A visualização no nível do segmento está disponível atualmente apenas para destinos em lote.
>- As métricas no nível do segmento são registradas atualmente apenas para execuções bem-sucedidas do fluxo de dados. Eles não são registrados para execuções de fluxo de dados com falha e registros excluídos.


![Segmentos no painel de fluxo de dados](../assets/ui/monitor-destinations/dashboard-segments-view.png)

Na visualização no nível do segmento, as métricas são agregadas em várias execuções de fluxo de dados dentro do intervalo de tempo selecionado. Se houver várias execuções de fluxo de dados, você poderá fazer drill-down a partir do nível de segmento para ver o detalhamento de cada execução de fluxo de dados, filtrado pelo segmento selecionado.
Usar o botão de filtro ![filter](../assets/ui/monitor-destinations/filter-add.png) para detalhar o fluxo de dados, execute a exibição para cada segmento no fluxo de dados.

### Página de execução do fluxo de dados {#dataflow-runs-page}

A página de execução do fluxo de dados exibe informações sobre as execuções do fluxo de dados, incluindo a hora de início da execução do fluxo de dados, o tempo de processamento, os perfis recebidos, as identidades ativadas, as identidades excluídas, as identidades falharam, a taxa de ativação e o status.

Ao fazer o detalhamento, o fluxo de dados executa a página a partir do [exibição em nível de segmento](#segment-level-view), você tem a opção de filtrar o fluxo de dados executado pelas seguintes opções:

- **[!UICONTROL O fluxo de dados é executado com identidades com falha]**: Para o segmento selecionado, essa opção lista todas as execuções de fluxo de dados que falharam na ativação. Para verificar por que as identidades em uma determinada execução do fluxo de dados falharam, consulte o [página de detalhes da execução do fluxo de dados](#dataflow-run-details-page) para essa execução do fluxo de dados.
- **[!UICONTROL O fluxo de dados é executado com identidades ignoradas]**: Para o segmento selecionado, essa opção lista todas as execuções de fluxo de dados em que algumas identidades não foram totalmente ativadas e alguns perfis foram ignorados. Para verificar por que as identidades em uma determinada execução do fluxo de dados foram ignoradas, consulte o [página de detalhes da execução do fluxo de dados](#dataflow-run-details-page) para essa execução do fluxo de dados.
- **[!UICONTROL O fluxo de dados é executado com identidades ativadas]**: Para o segmento selecionado, essa opção lista todas as execuções de fluxo de dados que têm identidades que foram ativadas com êxito.

![Filtrar execuções de fluxo de dados para segmentos](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Para ver mais detalhes sobre uma execução específica do fluxo de dados, selecione o filtro ![filter](../assets/ui/monitor-destinations/filter-add.png) ao lado do tempo de início da execução do fluxo de dados para ver a página de detalhes da execução do fluxo de dados.

![O fluxo de dados executa o filtro no painel de monitoramento](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Página Detalhes da execução do fluxo de dados {#dataflow-run-details-page}

A página de detalhes de execução do fluxo de dados, além dos detalhes mostrados na lista de execuções do fluxo de dados, exibe informações mais específicas sobre o fluxo de dados:

- **[!UICONTROL ID de execução do fluxo de dados]**: A ID do fluxo de dados.
- **[!UICONTROL ID da organização IMS]**: A organização IMS à qual o fluxo de dados pertence.
- **[!UICONTROL Última atualização]**: A hora em que a execução do fluxo de dados foi atualizada pela última vez.

A página de detalhes também tem um botão para alternar entre erros e segmentos de execução de fluxo de dados. Essa opção só está disponível para execuções de fluxo de dados em destinos em lote.

A visualização de erros de execução do fluxo de dados exibe uma lista de identidades que falharam e identidades que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo código de erro, contagem de identidades e descrição. Por padrão, a lista exibe as identidades com falha. Para mostrar identidades ignoradas, selecione o **[!UICONTROL Identidades excluídas]** alternar.

![Alternância de identidades excluídas](../assets/ui/monitor-destinations/identities-excluded.png)

When **[!UICONTROL Segmentos]** for selecionado, você verá uma lista dos segmentos que foram ativados na execução do fluxo de dados selecionado. Essa tela inclui informações a nível de segmento sobre as identidades ativadas, as identidades excluídas, bem como o status e a hora da última execução do fluxo de dados.

![Execução do fluxo de dados - exibição de segmentos](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Próximas etapas {#next-steps}

Seguindo este guia, agora você sabe como monitorar os fluxos de dados para destinos de lote e streaming, incluindo todas as informações relevantes, como tempo de processamento, taxa de ativação e status. Para saber mais sobre os fluxos de dados na Platform, leia o [visão geral dos fluxos de dados](../home.md). Para saber mais sobre destinos, leia a seção [visão geral dos destinos](../../destinations/home.md).