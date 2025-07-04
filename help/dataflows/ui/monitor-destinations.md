---
description: Saiba como monitorar fluxos de dados para seus destinos usando a interface do Experience Platform.
solution: Experience Platform
title: Monitorar fluxos de dados para destinos na interface do
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: fa7cfea74c5b76dd5643aaa2e9dd7447e9b9ef42
workflow-type: tm+mt
source-wordcount: '3621'
ht-degree: 9%

---

# Monitorar fluxos de dados para destinos na interface do

Use os vários destinos no catálogo do Experience Platform para ativar seus dados do Experience Platform para inúmeros parceiros externos. O Experience Platform facilita o processo de rastreamento do fluxo de dados para seus destinos ao fornecer transparência aos fluxos de dados.

O painel de monitoramento fornece uma representação visual da jornada de um fluxo de dados, incluindo o destino em que os dados estão sendo ativados, o tipo de dados que você está visualizando, dados exportados por execução de fluxo de dados e muito mais.

Este tutorial fornece instruções sobre como monitorar fluxos de dados diretamente no espaço de trabalho de destinos ou usar o painel de monitoramento para monitorar fluxos de dados para seus destinos usando a interface do usuário do Experience Platform.

## Introdução {#getting-started}

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [Fluxos de dados](../home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Experience Platform. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
   - [Execuções de fluxo de dados](../../sources/notifications.md): as execuções de fluxo de dados são os trabalhos agendados recorrentes com base na configuração de frequência dos fluxos de dados selecionados.
- [Destinos](../../destinations/home.md): os destinos são integrações pré-criadas com aplicativos usados com frequência que permitem a ativação contínua de dados do Experience Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Monitorar fluxos de dados no espaço de trabalho de Destinos {#monitor-dataflows-in-the-destinations-workspace}

No espaço de trabalho **[!UICONTROL Destinos]** da interface do usuário do Experience Platform, navegue até a guia **[!UICONTROL Procurar]** e selecione o nome de um destino que deseja exibir.

![Selecione a exibição de destino com uma conexão de destino realçada](../assets/ui/monitor-destinations/select-destination.png)

Uma lista de fluxos de dados existentes é exibida. Nesta página há uma lista de fluxos de dados visualizáveis, incluindo informações sobre seu destino, nome de usuário, número de fluxos de dados e status.

Consulte a tabela a seguir para obter mais informações sobre status:

| Status | Descrição |
| ------ | ----------- |
| Ativado | O status `Enabled` indica que um fluxo de dados está ativo e está exportando dados de acordo com o agendamento fornecido. |
| Desabilitado | O status `Disabled` indica que um fluxo de dados está inativo e não está exportando dados. |
| Processamento | O status `Processing` indica que um fluxo de dados ainda não está ativo. Esse status geralmente é encontrado imediatamente após a criação de um novo fluxo de dados. |
| Erro | O status `Error` indica que o processo de ativação de um fluxo de dados foi interrompido. |

### O fluxo de dados é executado para destinos de transmissão {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Detalhes de execução do fluxo de dados"
>abstract="Os detalhes de execução do fluxo de dados de destino contêm informações sobre o status de ativação de um público-alvo e métricas obtidas do Perfil do cliente em tempo real para gerar identidades exclusivas. Para saber mais, revise o guia de definições de métricas."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Perfis recebidos"
>abstract="O número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Identidades ativadas"
>abstract="A contagem de identidades de perfil individuais ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de públicos-alvo exportados."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Identidades excluídas"
>abstract="A contagem de registros de perfil individuais excluídos da ativação do destino selecionado com base em atributos ausentes e violação de consentimento."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Falha de identidades"
>abstract="A contagem de identidades de perfil individuais que falharam no destino selecionado. Verifique o diagnóstico de erro para obter detalhes."

Para destinos de transmissão, a guia [!UICONTROL Execuções de fluxo de dados] fornece uma atualização por hora para os dados de métrica em suas execuções de fluxo de dados. As estatísticas mais proeminentes rotuladas são para identidades.

As identidades representam as diferentes facetas de um perfil. Por exemplo, se um perfil contiver um número de telefone e um endereço de email, esse perfil terá duas identidades.

Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais de identidades:

- **[!UICONTROL Identidades ativadas]**: o número total de identidades de perfil ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de públicos-alvo exportados.
- **[!UICONTROL Identidades excluídas]**: o número total de identidades de perfil que são ignoradas para ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Falha nas identidades]**: o número total de identidades de perfil que não estão ativadas para o destino devido a erros.

![O fluxo de dados executa detalhes para destinos de streaming.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

- **[!UICONTROL Início da execução do fluxo de dados]**: a hora em que a execução do fluxo de dados começou. Para execuções de fluxo de dados de transmissão, o Experience Platform captura as métricas com base no início da execução do fluxo de dados, na forma de métricas por hora. Isso significa que, para execuções de fluxo de dados de transmissão, se uma execução de fluxo de dados tiver começado, por exemplo, às 22h30, a métrica mostrará a hora de início como 22h na interface do usuário.
- **[!UICONTROL Tempo de processamento]**: o tempo necessário para a execução do fluxo de dados ser processada.
   - Para execuções de **[!UICONTROL concluídas]**, a métrica de tempo de processamento sempre mostra uma hora.
   - Para execuções de fluxo de dados que ainda estão em um estado **[!UICONTROL processando]**, a janela para capturar todas as métricas permanece aberta por mais de uma hora, para processar todas as métricas que correspondem à execução do fluxo de dados. Por exemplo, uma execução de fluxo de dados iniciada às 9h30 pode permanecer em um estado de processamento por uma hora e trinta minutos para capturar e processar todas as métricas. Em seguida, quando a janela de processamento fechar e o status da execução do fluxo de dados atualizar para **concluído**, o tempo de processamento exibido será alterado para uma hora.
- **[!UICONTROL Perfis recebidos]**: o número total de perfis recebidos no fluxo de dados.
- **[!UICONTROL Identidades ativadas]**: o número total de identidades de perfil ativadas com êxito para o destino selecionado como parte da execução do fluxo de dados. Essa métrica inclui identidades que são criadas, atualizadas e removidas de públicos-alvo exportados.
- **[!UICONTROL Identidades excluídas]**: o número total de identidades de perfil excluídas da ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Falha nas identidades]** O número total de identidades de perfil que não estão ativadas para o destino devido a erros.

  >[!IMPORTANT]
  >
  > A partir de março de 2025, a Adobe está lançando uma atualização para aumentar a precisão dos relatórios para destinos de transmissão. Esse aprimoramento garante um melhor alinhamento entre os relatórios no Experience Platform e as plataformas de destino.
  >
  > Antes desta atualização, **[!UICONTROL Falha nas identidades]** incluiu todas as tentativas de ativação. Após essa atualização, somente a última tentativa de ativação será incluída na contagem total.
  > 
  > Esse aprimoramento se aplica a todos os destinos de streaming.
  > Após esse aprimoramento, os usuários de destinos de streaming podem observar uma queda esperada em sua contagem de **[!UICONTROL Falha de identidades]**.


- **[!UICONTROL Taxa de ativação]**: a porcentagem de identidades recebidas que foram ativadas com êxito. A fórmula a seguir demonstra como esse valor é calculado:
  ![Fórmula da taxa de ativação.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: representa o estado em que o fluxo de dados está: [!UICONTROL Concluído] ou [!UICONTROL Processando]. [!UICONTROL Concluído] significa que todas as identidades para a execução do fluxo de dados correspondente foram exportadas dentro do período de uma hora. [!UICONTROL Processando] significa que a execução do fluxo de dados ainda não foi concluída.

Para exibir os detalhes de uma execução de fluxo de dados específica, selecione a hora de início da execução na lista.

A página de detalhes de uma execução de fluxo de dados contém informações adicionais, como o número de perfis recebidos, o número de identidades ativadas, o número de identidades que falharam e o número de identidades excluídas.

![Detalhes do fluxo de dados para destinos de streaming.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

A página de detalhes também exibe uma lista de identidades que falharam e as que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo o código de erro, a contagem de identidades e a descrição. Por padrão, a lista exibe as identidades com falha. Para mostrar as identidades ignoradas, selecione a opção **[!UICONTROL Identidades excluídas]**.

![Registros de fluxo de dados para destinos de streaming com uma mensagem de erro realçada.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### Monitoramento de execução de fluxo de dados de nível de público do [!BADGE Beta]{type=Informative} para destinos de streaming {#audience-level-dataflow-runs-for-streaming-destinations}

Você pode exibir informações sobre as identidades ativadas, excluídas ou com falha em um nível de público-alvo, para cada público que faz parte do fluxo de dados.

O monitoramento no nível do público-alvo para destinos de streaming está disponível atualmente apenas para os seguintes destinos:

- [[!DNL (API) Oracle Eloqua] conexão](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)
- [[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)
- [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)
- [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)
- [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)
- [[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)
- [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)
- [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)
- [[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)
- [[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)
- [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)
- [[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)
- [[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)
- [[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)
- [[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)
- [[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)
- [[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)
- [[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)
- [[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)
- [[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)
- [[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)

![Monitoramento no nível do público-alvo para destinos de streaming.](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>O número **[!UICONTROL Perfis recebidos]** na guia **[!UICONTROL Públicos-alvo]** nem sempre corresponde ao número de perfis recebidos para a execução do fluxo de dados. Isso ocorre porque um determinado perfil pode fazer parte de mais de um público-alvo sendo ativado na execução do fluxo de dados.

### Execuções de fluxo de dados para destinos em lote {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Detalhes de execução do fluxo de dados"
>abstract="Os detalhes de execução do fluxo de dados de destino contêm informações sobre o status de ativação de um público-alvo e métricas obtidas do Perfil do cliente em tempo real para gerar identidades exclusivas. Para saber mais, revise o guia de definições de métricas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html?lang=pt-BR#dataflow-runs-for-streaming-destinations" text="O fluxo de dados é executado para destinos de transmissão"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Perfis recebidos"
>abstract="O número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Identidades ativadas"
>abstract="A contagem de identidades de perfil individuais ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de públicos-alvo exportados."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Identidades excluídas"
>abstract="A contagem de registros de perfil individuais excluídos da ativação do destino selecionado com base em atributos ausentes e violação de consentimento."

Para destinos em lote, a guia [!UICONTROL Execuções de fluxo de dados] fornece dados de métrica sobre suas execuções de fluxo de dados. Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais de identidades:

- **[!UICONTROL Identidades ativadas]**: o número total de identidades de perfil ativadas com êxito para o destino selecionado. Essa métrica inclui identidades que são criadas, atualizadas e removidas de públicos-alvo exportados.
- **[!UICONTROL Identidades excluídas]**: a contagem de identidades de perfil individuais excluídas da ativação para o destino selecionado, com base nos atributos ausentes e na violação de consentimento.

![O fluxo de dados executa a exibição para destinos em lote.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Cada execução de fluxo de dados individual mostra os seguintes detalhes:

- **[!UICONTROL Início da execução do fluxo de dados]**: a hora em que a execução do fluxo de dados começou.
- **[!UICONTROL Público-alvo]**: o nome do público associado a cada execução de fluxo de dados.
- **[!UICONTROL Tempo de processamento]**: o tempo necessário para a execução do fluxo de dados ser processada.
- **[!UICONTROL Perfis recebidos]**: o número total de perfis recebidos no fluxo de dados. Esse valor é atualizado a cada 60 minutos.
- **[!UICONTROL Identidades ativadas]**: o número total de identidades de perfil ativadas com êxito para o destino selecionado como parte da execução do fluxo de dados. Essa métrica inclui identidades que são criadas, atualizadas e removidas de públicos-alvo exportados.
- **[!UICONTROL Identidades excluídas]**: o número total de identidades de perfil excluídas da ativação com base em atributos ausentes e violação de consentimento.
- **[!UICONTROL Status]**: representa o estado em que o fluxo de dados está. Pode ser um destes três estados: [!UICONTROL Sucesso], [!UICONTROL Falha] e [!UICONTROL Processamento]. [!UICONTROL Sucesso] significa que o fluxo de dados está ativo e exportando dados de acordo com o agendamento fornecido. [!UICONTROL Falha] significa que a ativação de dados foi suspensa devido a erros. [!UICONTROL Processando] significa que o fluxo de dados ainda não está ativo e geralmente é encontrado quando um novo fluxo de dados é criado.

Para exibir detalhes de uma execução de fluxo de dados específica, selecione a hora de início da execução na lista.

>[!NOTE]
>
>As execuções de fluxo de dados são geradas com base na frequência de programação do fluxo de dados de destino. Uma execução de fluxo de dados separada é feita para cada [política de mesclagem](../../profile/merge-policies/overview.md) aplicada a um público.

A página de detalhes de um fluxo de dados, além dos detalhes mostrados na lista de fluxos de dados, exibe informações mais específicas sobre o fluxo de dados:

- **[!UICONTROL Tamanho dos dados]**: o tamanho do fluxo de dados que está sendo exportado.
- **[!UICONTROL Total de arquivos]**: o número total de arquivos exportados no fluxo de dados.
- **[!UICONTROL Última atualização]**: a hora em que a execução do fluxo de dados foi atualizada pela última vez.

![Detalhes da execução do fluxo de dados para destinos em lote.](../assets/ui/monitor-destinations/dataflow-batch.png)

A página de detalhes também exibe uma lista de identidades que falharam e as que foram excluídas. As informações das identidades com falha e excluída são exibidas, incluindo o código e a descrição do erro. Por padrão, a lista exibe as identidades com falha. Para mostrar identidades excluídas, selecione a opção **[!UICONTROL Identidades excluídas]**.

![Registros de fluxo de dados para destinos em lote com uma mensagem de erro realçada.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### Exibir no monitoramento {#view-in-monitoring}

Você também pode optar por exibir informações avançadas sobre um determinado fluxo de dados, que é executado no painel de monitoramento. Para exibir informações sobre um fluxo de dados no painel de monitoramento:

1. Navegue até **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** guia
2. Navegue até o fluxo de dados que deseja inspecionar.
3. Selecione o símbolo de reticências e o ![ícone de monitoramento](/help/images/icons/monitoring.png) **[!UICONTROL Exibir no monitoramento]**.

![Selecione Exibir no monitoramento do fluxo de trabalho de destinos para obter mais informações sobre um fluxo de dados.](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>Agora é possível exibir informações sobre o fluxo de dados e seu fluxo de dados associado no painel de monitoramento. Leia a seção abaixo para obter mais informações.

## Painel de monitoramento de destinos {#monitoring-destinations-dashboard}

>[!NOTE]
>
>Atualmente, a funcionalidade de monitoramento de destinos tem suporte para todos os destinos no Experience Platform *except* the [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) and [Custom Personalization](/help/destinations/catalog/personalization/custom-personalization.md) destinations.

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Activation"
>abstract="A visualização da ativação de destino contém informações sobre o status de ativação de um público-alvo e as métricas obtidas do Perfil do cliente em tempo real para gerar identidades exclusivas."

Para acessar o painel de [!UICONTROL Monitoramento], selecione **[!UICONTROL Monitoramento]** (![ícone de monitoramento](/help/images/icons/monitoring.png)) na navegação à esquerda. Uma vez na página [!UICONTROL Monitoramento], selecione [!UICONTROL Destinos]. O painel [!UICONTROL Monitoramento] contém métricas e informações sobre os trabalhos de execução de destino.

Use o painel [!UICONTROL Destinos] para ter uma ideia geral da integridade dos fluxos de ativação. Comece obtendo insights em um nível agregado para todos os destinos de lote e transmissão e depois analise detalhadamente as exibições de fluxos de dados, execuções de fluxo de dados e públicos ativados para obter uma análise detalhada dos dados de ativação. As telas no painel [!UICONTROL Monitoramento] fornecem insights acionáveis por meio de métricas e descrições de erros para ajudá-lo a solucionar problemas que possam surgir em seus cenários de ativação.

É possível filtrar as informações exibidas por tipo de dados - clientes, contas (somente para o Adobe Real-Time CDP B2B edition), clientes potenciais e enriquecimento da conta. Leia mais sobre essas opções no [guia do painel de monitoramento](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![Filtro de tipo de dados realçado na exibição do painel de monitoramento.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

No centro do painel está o painel [!UICONTROL Ativação], que contém métricas e gráficos que exibem dados sobre a taxa de ativação dos dados exportados para destinos de streaming, bem como sobre as execuções de fluxo de dados em lote com falha para destinos em lote.

![Gráficos de ativação em lote e streaming destacados na exibição de monitoramento.](../assets/ui/monitor-destinations/dashboard-graph.png)


Por padrão, os dados exibidos contêm as informações de ativação das últimas 24 horas. Selecione **[!UICONTROL Últimas 24 horas]** para ajustar o intervalo de tempo dos registros exibidos. As opções disponíveis incluem **[!UICONTROL Últimas 24 horas]**, **[!UICONTROL Últimos 7 dias]** e **[!UICONTROL Últimos 30 dias]**. Como alternativa, você pode selecionar as datas na janela pop-up do calendário exibida. Depois de selecionar as datas, selecione **[!UICONTROL Aplicar]** para ajustar o intervalo de tempo das informações exibidas.

>[!NOTE]
>
>A captura de tela a seguir mostra a taxa de ativação e as execuções do fluxo de dados em lote para os últimos 30 dias, em vez das últimas 24 horas. Você pode ajustar o período selecionando **[!UICONTROL Últimos 30 dias]**.

![Alterar controle de intervalo de datas de retrospectiva realçado para destinos ativados](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Use o ícone de seta (![ícone de seta](/help/images/icons/chevron-up.png)) para expandir ou descartar os cartões na parte superior da tela, que mostram rapidamente informações sobre os detalhes de ativação, com base no tipo de destino - streaming ou lote:

- **[!UICONTROL Taxa de ativação de streaming]**: representa a porcentagem de identidades recebidas que foram ativadas ou ignoradas com êxito. A fórmula usada para calcular essa porcentagem está descrita mais acima nesta página, na seção [Execuções de fluxo de dados para destinos de streaming](#dataflow-runs-for-streaming-destinations).
- **[!UICONTROL Execuções de fluxo de dados com falha em lote]**: representa o número de execuções de fluxo de dados com falha no intervalo de tempo selecionado.

![Mostrar ou descartar cartões na parte superior da página.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

O gráfico **[!UICONTROL Ativation]** é exibido por padrão e você pode desabilitá-lo para expandir a lista de destinos abaixo. Selecione a opção **[!UICONTROL Métricas e gráficos]** para desabilitar os gráficos.

O painel **[!UICONTROL Ativação]** exibe uma lista de destinos que contêm pelo menos uma conta existente. Esta lista também inclui informações sobre os perfis recebidos, identidades ativadas, identidades com falha, identidades excluídas, taxa de ativação, total de fluxos de dados com falha e a última data atualizada para esses destinos. Nem todas as métricas estão disponíveis para todos os tipos de destino. A tabela abaixo descreve as métricas e informações disponíveis por tipo de destino.

| Métrica | Tipo de destino |
|--------------------------------------|-----------------------|
| **[!UICONTROL Registros recebidos]** | Streaming e lote |
| **[!UICONTROL Registros ativados]** | Streaming e lote |
| **[!UICONTROL Registros com falha]** | Transmissão |
| **[!UICONTROL Registros ignorados]** | Streaming e lote |
| **[!UICONTROL Tipo de dados]** | Streaming e lote |
| **[!UICONTROL Taxa de ativação]** | Transmissão |
| **[!UICONTROL Total de fluxos de dados com falha]** | Lote |
| **[!UICONTROL Última atualização]** | Streaming e lote |

{style="table-layout:auto"}

![Painel de monitoramento com todos os destinos ativados realçados.](../assets/ui/monitor-destinations/dashboard-destinations.png)

Também é possível filtrar a lista de destinos para exibir apenas a categoria de destinos selecionada. Selecione a lista suspensa **[!UICONTROL Meus destinos]** e selecione a [categoria de destino](/help/destinations/destination-types.md#categories) para a qual você deseja filtrar.

![Filtrar destinos com o seletor suspenso](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Além disso, você pode inserir um destino na barra de pesquisa para isolar em um único destino. Se quiser ver os fluxos de dados do destino, selecione o filtro ![filtro](/help/images/icons/filter-add.png) ao lado dele para ver uma lista de seus fluxos de dados ativos.

![Filtrar destinos usando a barra de pesquisa realçada na exibição de monitoramento.](../assets/ui/monitor-destinations/filtered-destinations.png)

Para exibir todos os fluxos de dados existentes em todos os destinos, selecione **[!UICONTROL Fluxos de Dados]**.

Uma lista de fluxos de dados é exibida, classificada pela última execução do fluxo de dados. Você pode ver detalhes adicionais para um fluxo de dados específico localizando o destino que deseja monitorar, selecionando o filtro ![filtro](/help/images/icons/filter-add.png) ao lado dele e, em seguida, selecionando o filtro ![filtro](/help/images/icons/filter-add.png) ao lado do fluxo de dados sobre o qual deseja obter mais informações.

![Todos os fluxos de dados destacados no painel de monitoramento.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

Depois de selecionar um fluxo de dados para inspeção adicional, a página de detalhes do fluxo de dados contém um botão que permite ver os dados ativados no fluxo de dados, divididos por execuções de fluxo de dados ou públicos.

### Exibição de execuções de fluxo de dados {#dataflow-runs-view}

Quando **[!UICONTROL Execuções de fluxo de dados]** é selecionado, você pode ver uma lista de execuções de fluxo de dados para o fluxo de dados selecionado e mais informações sobre cada execução.

>[!INFO]
>
>Para fluxos de dados para destinos de transmissão, uma execução de fluxo de dados é dividida em janelas por hora. Cada janela por hora gera uma ID de execução de fluxo de dados correspondente.
>
>Para fluxos de dados para destinos em lote, cada público-alvo tem uma execução de fluxo de dados correspondente gerada, com base na frequência agendada de ativação de público-alvo. Por exemplo, se você configurar uma ativação diária agendada para cinco públicos-alvo no mesmo fluxo de dados de destino, haverá cinco execuções de fluxo de dados separadas geradas todos os dias.

![Painel de execuções de fluxo de dados com várias execuções destacadas.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Use o botão **[!UICONTROL Mostrar somente falhas]** para exibir somente as execuções com falha para um fluxo de dados.

![O fluxo de dados executa o modo de exibição com a opção Mostrar falhas apenas realçada](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Exibição no nível do público {#segment-level-view}

Quando **[!UICONTROL Públicos-alvo]** é selecionado, você vê uma lista de públicos-alvo que foram ativados para o fluxo de dados selecionado, dentro do intervalo de tempo selecionado. Essa tela inclui informações no nível do público-alvo sobre os registros ativados e excluídos, bem como o status e a hora da última execução do fluxo de dados. Ao revisar as métricas de registros excluídos e ativados, é possível verificar se um público-alvo foi ativado com êxito ou não.

Por exemplo, você está ativando um público-alvo chamado &quot;Membros de fidelidade na Califórnia&quot; para um destino do Amazon S3 &quot;Membros de fidelidade Califórnia dezembro&quot;. Vamos supor que haja 100 perfis no público-alvo selecionado, mas apenas 80 dos 100 registros contenham atributos de ID de fidelidade e você tenha definido as regras de mapeamento de exportação como `loyalty.id` é necessário. Nesse caso, em um nível de público-alvo, você verá 80 registros ativados e 20 registros excluídos.

>[!IMPORTANT]
>
>Observe as limitações atuais relacionadas às métricas no nível do público-alvo:
>
>- A exibição no nível do público-alvo está disponível atualmente para os destinos listados abaixo. A implantação está planejada para outros destinos de streaming.
>
>   - [[!DNL Google Customer Match + Display & Video 360]](/help/destinations/catalog/advertising/google-customer-match-dv360.md)
>   - [[!DNL (V2) Marketo Engage]](/help/destinations/catalog/adobe/marketo-engage.md)
>   - [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md)
>   - [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
>   - [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
>   - Destinos em lote (baseados em arquivo)
> 
>- Para destinos em lote, as métricas no nível do público-alvo são atualmente registradas somente para execuções bem-sucedidas de fluxo de dados. Eles não são registrados para execuções de fluxo de dados com falha e registros excluídos. Para execuções de fluxo de dados para destinos de transmissão, as métricas são capturadas e exibidas para registros ativados e excluídos.

![Públicos-alvo destacados no painel de fluxo de dados.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

Na visualização em nível de público-alvo, as métricas são agregadas em várias execuções de fluxo de dados dentro do intervalo selecionado. Se houver várias execuções de fluxo de dados, você poderá detalhar a partir do nível do público-alvo para ver o detalhamento de cada execução de fluxo de dados, filtrado pelo público selecionado.
Use o botão de filtro ![filtro](/help/images/icons/filter-add.png) para detalhar a exibição de execuções de fluxo de dados para cada público no fluxo de dados.

### Página Execuções de fluxo de dados {#dataflow-runs-page}

A página de execuções do fluxo de dados exibe informações sobre suas execuções de fluxo de dados, incluindo o tempo de início da execução do fluxo de dados, o tempo de processamento, os registros recebidos, os registros ativados, os registros excluídos, os registros com falha, a taxa de ativação e o status.

Ao detalhar a página de execuções do fluxo de dados na [exibição no nível de público-alvo](#segment-level-view), você tem a opção de filtrar as execuções do fluxo de dados pelas seguintes opções:

- **[!UICONTROL O fluxo de dados é executado com registros com falha]**: para o público selecionado, essa opção lista todas as execuções de fluxo de dados que falharam na ativação. Para inspecionar por que os registros em uma determinada execução de fluxo de dados falharam, consulte a [página de detalhes da execução do fluxo de dados](#dataflow-run-details-page) dessa execução de fluxo de dados.
- **[!UICONTROL O fluxo de dados é executado com registros excluídos]**: para o público selecionado, essa opção lista todas as execuções de fluxo de dados em que alguns registros não foram totalmente ativados e alguns perfis foram ignorados. Para inspecionar por que os registros em uma determinada execução de fluxo de dados foram ignorados, consulte a [página de detalhes da execução do fluxo de dados](#dataflow-run-details-page) dessa execução de fluxo de dados.
- **[!UICONTROL O fluxo de dados é executado com registros ativados]**: para o público selecionado, essa opção lista todas as execuções de fluxo de dados que têm registros ativados com êxito.

![Botões de opção que mostram como filtrar execuções de fluxo de dados para públicos-alvo.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Para ver mais detalhes sobre uma execução de fluxo de dados específica, selecione o filtro ![filtro](/help/images/icons/filter-add.png) ao lado da hora de início da execução do fluxo de dados para ver a página de detalhes da execução do fluxo de dados.

![O fluxo de dados executa o filtro no painel de monitoramento para detalhar mais informações para uma determinada execução de fluxo de dados.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Página de detalhes da execução do fluxo de dados {#dataflow-run-details-page}

A página de detalhes da execução do fluxo de dados, além dos detalhes mostrados na lista de execuções do fluxo de dados, exibe informações mais específicas sobre o fluxo de dados:

- **[!UICONTROL ID de execução do fluxo de dados]**: a ID do fluxo de dados.
- **[!UICONTROL ID da Organização IMS]**: a organização à qual o fluxo de dados pertence.
- **[!UICONTROL Última atualização]**: a hora em que a execução do fluxo de dados foi atualizada pela última vez.

A página de detalhes também tem um botão para alternar entre erros de execução de fluxo de dados e públicos-alvo. Esta opção só está disponível para execuções de fluxo de dados em destinos em lote e para o destino de streaming do [Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md).

A exibição de erros de execução do fluxo de dados exibe uma lista de registros que falharam e registros que foram ignorados. As informações para os registros com falha e ignorados são exibidas, incluindo o código de erro, a contagem de identidades e a descrição. Por padrão, a lista exibe os registros com falha. Para mostrar os registros ignorados, selecione a opção **[!UICONTROL Registros ignorados]**.

![Alternância de identidades excluídas realçada na exibição de monitoramento](../assets/ui/monitor-destinations/identities-excluded.png)

Quando **[!UICONTROL Públicos-alvo]** é selecionado, você verá uma lista dos públicos-alvo que foram ativados na execução do fluxo de dados selecionado. Essa tela inclui informações no nível do público-alvo sobre os registros ativados e excluídos, bem como o status e a hora da última execução do fluxo de dados.

![Exibição de públicos-alvo na tela de detalhes de execução do fluxo de dados.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Próximas etapas {#next-steps}

Ao seguir este guia, agora você sabe como monitorar fluxos de dados para destinos em lote e de streaming, incluindo todas as informações relevantes, como tempo de processamento, taxa de ativação e status. Para saber mais sobre fluxos de dados no Experience Platform, leia a [visão geral sobre fluxos de dados](../home.md). Para saber mais sobre destinos, leia a [visão geral sobre destinos](../../destinations/home.md).