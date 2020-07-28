---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de dados Analytics
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Conector de dados Analytics

O Adobe Experience Platform permite que você ingira dados do Adobe Analytics por meio do Analytics Data Connector (ADC). O ADC transmite os dados coletados pela Adobe Analytics para a Platform em tempo real, convertendo dados Analytics formatados pelo SCDS em campos do Modelo de dados de experiência (XDM) para consumo pela Platform.

Este documento fornece uma visão geral do Adobe Analytics e descreve os casos de uso para dados do Analytics.

## Dados Adobe Analytics e Analytics

A Adobe Analytics é um mecanismo poderoso para ajudá-lo a saber mais sobre seus clientes, como eles interagem com suas propriedades da Web, onde seus gastos com marketing digital são efetivos e identificam áreas de aprimoramento. A Adobe Analytics lida com trilhões de transações da Web por ano e o ADC permite que você se aprofunde com facilidade nesses ricos dados comportamentais e aprimore o Perfil do cliente em tempo real em questão de minutos.

![](./images/analytics-data-experience-platform.png)

Em um nível superior, a Adobe Analytics coleta dados de vários canais digitais e vários data centers no mundo inteiro. Depois que os dados são coletados, as regras de identificação, segmentação e transformação do Visitante (VISTA) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passam por esse processamento leve, eles são considerados prontos para consumo pelo Perfil do cliente em tempo real. Em um processo paralelo ao acima, os mesmos dados processados são agrupados em microlotes e ingeridos em conjuntos de dados da Platform para consumo pela Data Science Workspace, pelo Query Service e por outros aplicativos de descoberta de dados.

Consulte Visão geral [das regras de](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules.html) processamento para obter mais informações sobre as regras de processamento.

## Modelo de dados de experiência (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo a ser usado para se comunicar com serviços no Adobe Experience Platform.

A adesão aos padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a visão geral [do Sistema](../../../xdm/home.md)XDM.

## Como os campos são mapeados do Adobe Analytics para o XDM?

Quando uma conexão de origem é estabelecida para trazer dados do Analytics para o Experience Platform usando a interface do usuário do Platform, os campos de dados são automaticamente mapeados e assimilados no Perfil do cliente em tempo real em minutos. Para obter instruções sobre como criar uma conexão de origem com o Adobe Analytics usando a interface do usuário do Platform, consulte o tutorial [do conector de dados](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Para obter informações detalhadas sobre o mapeamento de campos que ocorre entre o Analytics e o Experience Platform, visite o guia de mapeamento [de campos da](./mapping/analytics.md) Adobe Analytics.

## Qual é a latência esperada para os Dados Analytics no Platform?

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para o Perfil do cliente em tempo real (A4T **não** ativado) | &lt; 2 minutos |
| Novos dados para o Perfil do cliente em tempo real (A4T **está** ativado) | &lt; 15 minutos |
| Novos dados para Data Lake | &lt; 45 minutos |
| Dados de preenchimento retroativo (13 meses de dados ou 10 bilhões de eventos, o que for menor) | &lt; 4 semanas |

>[!NOTE]
>
>A latência varia dependendo da configuração do cliente, dos volumes de dados e dos aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T` a latência para Pipeline, ela aumentará para 5 a 10 minutos.