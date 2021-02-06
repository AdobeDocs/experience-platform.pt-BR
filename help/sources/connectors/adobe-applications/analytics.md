---
keywords: Experience Platform;home;popular tópicos;Analytics Data Connector;analytics;Analytics
solution: Experience Platform
title: Conector de origem Adobe Analytics para dados do conjunto de relatórios
topic: overview
description: Este documento fornece uma visão geral do Analytics e descreve os casos de uso dos dados do Analytics.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---


# Conector Adobe Analytics para dados do conjunto de relatórios

A Adobe Experience Platform permite que você ingira dados da Adobe Analytics por meio do ADC (Analytics Data Connector). O ADC transmite os dados coletados por [!DNL Analytics] para [!DNL Platform] em tempo real, convertendo os dados [!DNL Analytics] formatados pelo SCDS em [!DNL Experience Data Model] (XDM) campos para consumo por [!DNL Platform].

Este documento fornece uma visão geral de [!DNL Analytics] e descreve os casos de uso dos dados [!DNL Analytics].

## Dados do Adobe Analytics e do Analytics

[!DNL Analytics] é um mecanismo poderoso para ajudá-lo a saber mais sobre seus clientes, como eles interagem com suas propriedades da Web, ver onde seus gastos com marketing digital são efetivos e identificar áreas de aprimoramento. [!DNL Analytics] lida com trilhões de transações da Web por ano e o ADC permite que você se aprofunde com facilidade nesses dados comportamentais ricos e aprimore o conteúdo  [!DNL Real-time Customer Profile] em questão de minutos.

![](./images/analytics-data-experience-platform.png)

Em um nível alto, [!DNL Analytics] coleta dados de vários canais digitais e vários data centers no mundo inteiro. Depois que os dados são coletados, as regras de identificação, segmentação e transformação do Visitante (VISTA) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passarem por esse processamento leve, serão considerados prontos para consumo por [!DNL Real-time Customer Profile]. Em um processo paralelo ao acima, os mesmos dados processados são agrupados em microlotes e assimilados em conjuntos de dados da plataforma para consumo por [!DNL Data Science Workspace], [!DNL Query Service] e outros aplicativos de detecção de dados.

Consulte [Visão geral das regras de processamento](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obter mais informações sobre as regras de processamento.

## Modelo de dados de experiência (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo a ser usado para se comunicar com serviços em [!DNL Experience Platform].

A adesão aos padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a [visão geral do sistema XDM](../../../xdm/home.md).

## Como os campos são mapeados do Adobe Analytics para o XDM?

Quando uma conexão de origem é estabelecida para trazer [!DNL Analytics] dados para [!DNL Experience Platform] usando a interface do usuário [!DNL Platform], os campos de dados são mapeados e assimilados automaticamente para [!DNL Real-time Customer Profile] em minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] usando a interface do usuário [!DNL Platform], consulte o tutorial do conector de dados do Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).[

Para obter informações detalhadas sobre o mapeamento de campos que ocorre entre [!DNL Analytics] e [!DNL Experience Platform], visite o guia [Mapeamento de campos da Adobe Analytics](./mapping/analytics.md).

## Qual é a latência esperada para os dados do Analytics na plataforma?

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **not** ativado) | &lt; 2 minutos |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **está** ativado) | &lt; 15 minutos |
| Novos dados para Data Lake | &lt; 45 minutos |
| Dados de preenchimento retroativo (13 meses de dados ou 10 bilhões de eventos, o que for menor) | &lt; 4 semanas |

>[!NOTE]
>
>A latência varia dependendo da configuração do cliente, dos volumes de dados e dos aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T` a latência para Pipeline aumentará para 5 a 10 minutos.

## Identificadores principais nos dados do Analytics

Cada ocorrência do conector de dados do Analytics contém um identificador primário que depende da existência de um ECID ou AAID. Se existir um ECID, o ECID é designado como o identificador principal. Se houver um AAID, o AAID será designado como o principal.