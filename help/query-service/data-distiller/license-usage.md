---
title: Monitorar uso de licença de consulta em lote
description: A interface do usuário do Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre o uso da licença do Data Distiller da sua organização.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: f33629d73e9bc7273e6ee5170294618f3e9731a8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Monitorar o uso de licença de consulta em lote {#monitor-license-usage}

O painel de uso da licença fornece relatórios detalhados sobre o uso da licença do Serviço de consulta de sua organização e as métricas de uso de cada produto adquirido. Para saber mais sobre as métricas disponíveis exibidas no painel, visite o [guia do painel de uso da licença](../../dashboards/guides/license-usage.md#available-metrics).

O painel fornece métricas de uso para cada produto comprado, o uso consolidado de métricas em todas as sandboxes de produção ou desenvolvimento e as métricas de uso de uma sandbox específica. As informações exibidas aqui são capturadas durante um instantâneo diário da sua instância da Platform.

>[!NOTE]
>
>O painel de uso de licença não está habilitado por padrão. Os usuários devem receber a permissão &quot;Exibir painel de uso da licença&quot; para poderem exibir o painel. Para obter etapas sobre como conceder permissões de acesso para exibir o painel de uso da licença, consulte o [guia de permissões do painel](../../dashboards/permissions.md).

## Computar horas {#compute-hours}

A variável [!UICONTROL Computar horas] A métrica só é aplicável a clientes com a licença do Data Distiller para consultas em lote. [!UICONTROL Computar horas] são a medida do tempo gasto pelos mecanismos do Serviço de consulta para ler, processar e gravar dados de volta no data lake quando uma consulta em lote é executada.

>[!NOTE]
>
>**A variável [!UICONTROL Computar horas] Os dados do estão disponíveis com limitações**: os dados começam em 1º de outubro de 2023 sem tendências.<br>A variável **preenchimento retroativo** de dados a partir da data de início do contrato é um trabalho em andamento. Espera-se que esteja disponível até o final do ano civil.

![O painel de uso da licença com a métrica horas de computação realçada.](../images/data-distiller/compute-hours.png)

Para encontrar mais informações sobre as métricas disponíveis para sua organização com base na licença adquirida da organização, consulte a [guia do painel de uso da licença](../../dashboards/guides/license-usage.md).
