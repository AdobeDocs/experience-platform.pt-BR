---
title: Monitorar públicos-alvo de transmissão
description: Saiba como usar o painel de monitoramento para monitorar públicos avaliados usando a segmentação por transmissão
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 6%

---


# Monitorar públicos-alvo de transmissão

intro blurb

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fluxos de dados](../home.md): os fluxos de dados representam trabalhos de dados que transferem informações pela Experience Platform. Eles são configurados em vários serviços para facilitar a movimentação de dados dos conectores de origem para os conjuntos de dados de destino, bem como para o Serviço de identidade, o Perfil do cliente em tempo real e os Destinos.
* [Serviço de segmentação](../../segmentation/home.md):
* [Capacidades](../../landing/license-usage-and-guardrails/capacity.md): no Experience Platform, as capacidades informam se sua organização excedeu alguma das medidas de proteção e fornecem informações sobre como corrigir esses problemas.

## Monitoramento de métricas para públicos-alvo de transmissão {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Taxa de avaliação"
>abstract="Essa métrica representa o número de registros avaliados por segundo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="Latência de assimilação P95"
>abstract="Essa métrica mede a latência do 95º percentil de um evento que chega ao Adobe Experience Platform para avaliação bem-sucedida no público-alvo."
>text="Learn more in documentation"

A tabela a seguir fornece informações mais detalhadas sobre as métricas usadas para públicos-alvo de transmissão.

| Métrica | Descrição | Dimensões |
| ------ | ----------- | ---------- |
| Taxa de avaliação | O número de avaliações de público processadas por segundo. | Sandbox, conjunto de dados |
| Latência de assimilação P95 | A latência do percentil 95 da chegada bem-sucedida do evento ao público. | Sandbox, conjunto de dados |
| Registros recebidos | O número total de registros recebidos da assimilação por transmissão para segmentação por transmissão durante a janela de tempo selecionada. | Conjunto de dados |
| Registros avaliados | O número total de registros que **com êxito** avaliaram usando a segmentação por transmissão durante a janela de tempo selecionada. | Conjunto de dados |
| Registros com falha | O número total de registros que **falharam** na avaliação da segmentação por transmissão devido a erros durante a janela de tempo selecionada. | Conjunto de dados, execução de fluxo |
| Registros ignorados | O número total de registros que **ignoraram** avaliação na segmentação por transmissão devido a erros durante a janela de tempo selecionada. | Conjunto de dados, execução de fluxo |
| Perfis qualificados | O número de perfis qualificados para o público durante a janela de tempo selecionada. | Sandbox, Audience |
| Perfis desqualificados | O número de perfis que se desqualificaram do público-alvo durante a janela de tempo selecionada. | Sandbox, Audience |

{style="table-layout:auto"}

## Usar o painel de monitoramento para públicos-alvo de transmissão {#monitoring-dashboard}

Para acessar o painel de monitoramento de públicos-alvo de streaming, vá para a interface do usuário do Experience Platform, selecione **[!UICONTROL Monitoring]** na navegação à esquerda e selecione **[!UICONTROL Streaming end-to-end]**.

IMAGEM

Na parte superior do painel está o cartão de métrica **[!UICONTROL Audiences]**. Isso exibe informações sobre a **Taxa de avaliação** para os públicos-alvo.