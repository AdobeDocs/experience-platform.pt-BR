---
title: Monitorar assimilação de perfil por transmissão
description: Saiba como usar o painel de monitoramento para monitorar a assimilação do perfil de transmissão
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# Monitorar assimilação de perfil por transmissão

Você pode usar o painel de monitoramento na interface do usuário do Adobe Experience Platform para realizar o monitoramento em tempo real das taxas de assimilação de perfil de transmissão na sua organização. Use esse recurso para obter mais transparência nas métricas de taxa de transferência, latência e qualidade dos dados em torno dos dados de transmissão. Além disso, você pode usar esse recurso para alertas proativos e recuperação de insights acionáveis para identificar possíveis violações de capacidade e problemas de assimilação de dados.

Leia o guia a seguir para saber como você pode usar o painel de monitoramento para monitorar taxas e métricas de trabalhos de assimilação de perfil de transmissão na sua organização.

## Noções básicas do painel de assimilação do perfil de transmissão

Você pode usar três categorias de métrica diferentes no painel de monitoramento para assimilação do perfil de streaming: [!UICONTROL Taxa de transferência], [!UICONTROL Assimilação] e [!UICONTROL Latência].

* **Taxa de transferência**: selecione **[!UICONTROL Taxa de transferência]** para exibir informações sobre a quantidade de dados que o Experience Platform está processando, dado um período configurado. Consulte esta métrica para avaliar a eficiência e a capacidade do seu sistema.
   * **Capacidade**: a quantidade máxima de dados que sua sandbox pode processar sob condições definidas.
   * **Taxa de transferência de solicitação**: a taxa na qual os eventos são recebidos pelo sistema de assimilação, medida em eventos por segundo.
   * **Taxa de transferência de processamento**: a taxa na qual o sistema assimila e processa com êxito as cargas de evento de entrada, medida em eventos por segundo.
* **Assimilação**: selecione [!UICONTROL Assimilação] para exibir informações sobre os trabalhos de assimilação na sandbox. Esses trabalhos de assimilação são medidos em três métricas diferentes:
   * **Registros criados**: a quantidade total de registros criados em um determinado período. Essa métrica representa processos de assimilação de dados bem-sucedidos em sua sandbox.
   * **Registros com falha**: o número total de registros não assimilados devido a erros.
   * **Registros descartados**: o número total de registros que foram descartados devido à violação dos limites de capacidade.
* **Latência**: selecione [!UICONTROL Latência] para exibir informações sobre o tempo que o Experience Platform leva para responder a uma solicitação ou concluir uma operação em um determinado período.

## Métricas de monitoramento para assimilação de perfil de transmissão {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Monitorar assimilação de perfil por transmissão"
>abstract="O painel de monitoramento para perfis de transmissão exibe informações sobre taxa de transferência, taxas de assimilação e latência. Use esse painel para exibir, entender e analisar as métricas de processamento de dados. de seus perfis de streaming no Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Taxa de transferência da solicitação"
>abstract="Essa métrica representa o número de eventos que entram no sistema de assimilação por segundo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Taxa de transferência de processamento"
>abstract="Essa métrica representa o número de eventos assimilados com êxito pelo sistema a cada segundo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="Latência de assimilação P95"
>abstract="Essa métrica mede a latência do percentil 95 do momento em que um evento chega ao Experience Platform até quando ele é assimilado com êxito no armazenamento de Perfil."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Taxa de transferência máxima"
>abstract="Essa métrica representa o número máximo de solicitações de entrada por segundo ao entrar na assimilação do perfil de streaming."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Registros assimilados"
>abstract="Essa métrica representa o número total de registros assimilados no armazenamento de Perfil em uma janela de tempo configurada."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Registros com falha"
>abstract="Essa métrica representa o número total de registros que falharam na assimilação no armazenamento de Perfil, em uma janela de tempo configurada, devido a erros."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Registros ignorados"
>abstract="Essa métrica representa o número total de registros que foram descartados em uma janela de tempo configurada devido a falhas de configuração ou de capacidade."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Detalhes do erro"
>abstract="Essa métrica representa o número de eventos com falha devido a erros."
>text="Learn more in documentation"

| Métrica | Descrição | Dimensões | Frequência de medição |
| --- | --- | --- | --- |
| Taxa de transferência da solicitação | Essa métrica representa o número de eventos que entram no sistema de assimilação por segundo. | Sandbox/Fluxo de dados | Monitoramento em tempo real com uma atualização de dados a cada 60 segundos. |
| Taxa de transferência de processamento | Essa métrica representa o número de eventos assimilados com êxito pelo sistema a cada segundo. | Sandbox/Fluxo de dados | Monitoramento em tempo real com uma atualização de dados a cada 60 segundos. |
| Latência de assimilação P95 | Essa métrica mede a latência do percentil 95 do momento em que um evento chega ao Experience Platform até quando ele é assimilado com êxito no armazenamento de Perfil. | Sandbox/Fluxo de dados | Monitoramento em tempo real com uma atualização de dados a cada 60 segundos. |
| Taxa de transferência máxima |
| Registros assimilados | Essa métrica representa o número total de registros assimilados no armazenamento de Perfil em uma janela de tempo configurada. | <ul><li>Sandbox/Fluxo de dados</li><li>Execução do fluxo de dados</li></ul> | <ul><li>Sandbox/Fluxo de dados: monitoramento em tempo real com uma atualização de dados a cada 60 segundos.</li><li>Execução do fluxo de dados: agrupado em 15 minutos.</li></ul> |
| Registros com falha | Essa métrica representa o número total de registros que falharam na assimilação no armazenamento de Perfil, em uma janela de tempo configurada, devido a erros. | <ul><li>Sandbox/Fluxo de dados</li><li>Execução do fluxo de dados</li></ul> | <ul><li>Sandbox/Fluxo de dados: monitoramento em tempo real com uma atualização de dados a cada 60 segundos.</li><li>Execução do fluxo de dados: agrupado em 15 minutos.</li></ul> |
| Registros ignorados | Essa métrica representa o número total de registros que foram descartados em uma janela de tempo configurada devido a falhas de configuração ou de capacidade. | <ul><li>Sandbox/Fluxo de dados</li><li>Execução do fluxo de dados</li></ul> | <ul><li>Sandbox/Fluxo de dados: monitoramento em tempo real com uma atualização de dados a cada 60 segundos.</li><li>Execução do fluxo de dados: agrupado em 15 minutos.</li></ul> |
| Detalhes do erro | Essa métrica representa o número de eventos com falha devido a erros. | Execução do fluxo de dados | Agrupado em uma janela por hora. |

{style="table-layout:auto"}