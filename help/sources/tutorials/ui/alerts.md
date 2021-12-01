---
keywords: Experience Platform; home; tópicos populares; alertas
description: Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo.
title: Assinar alertas em contexto na interface do usuário
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Assinar mensagens de alerta para monitorar os fluxos de dados de fontes na interface do usuário

O Adobe Experience Platform permite assinar alertas baseados em eventos sobre atividades do Adobe Experience Platform. Os alertas reduzem ou eliminam a necessidade de pesquisar a variável [[!DNL Observability Insights] API](../../../observability/api/overview.md) para verificar se uma tarefa foi concluída, se um determinado marco em um workflow foi atingido ou se ocorreram erros.

Você pode assinar alertas ao criar um fluxo de dados para receber mensagens de alerta sobre o status, o sucesso ou a falha da execução do fluxo.

Este documento fornece etapas sobre como assinar alertas e receber mensagens de alerta para suas execuções de fluxo.

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços.
* [Observabilidade](../../../observability/home.md): [!DNL Observability Insights] O permite monitorar as atividades do Platform por meio do uso de métricas estatísticas e notificações de eventos.
   * [Alertas](../../../observability/alerts/overview.md): Quando um determinado conjunto de condições em suas operações da plataforma é atingido (como um possível problema quando o sistema viola um limite), a Platform pode enviar mensagens de alerta para qualquer usuário em sua organização que tenha se inscrito nelas.

## Inscrever-se em alertas na interface do usuário {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Assinar alertas de origens"
>abstract="Os alertas permitem receber notificações com base no status dos fluxos de dados de fontes. É possível definir notificações de alerta para obter atualizações caso o fluxo de dados tenha sido iniciado, tenha sido bem-sucedido, tenha falhado ou não tenha assimilado dados."
>text="Learn more in documentation"
