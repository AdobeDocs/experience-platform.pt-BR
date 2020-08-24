---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de dados do Analytics
topic: overview
translation-type: tm+mt
source-git-commit: a93b3a1980ca0f1d3a32257a923eb7ffc8896fd5
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# Conector de dados do Analytics

A Adobe Experience Platform permite que você ingira dados da Adobe Analytics por meio do ADC (Analytics Data Connector). O ADC transmite os dados coletados por [!DNL Analytics] para [!DNL Platform] em tempo real, convertendo os dados formatados pelo SCDS em campos [!DNL Analytics] (XDM) para consumo [!DNL Experience Data Model] [!DNL Platform].

Este documento fornece uma visão geral de [!DNL Analytics] e descreve os casos de uso de [!DNL Analytics] dados.

## Dados do Adobe Analytics e do Analytics

[!DNL Analytics] é um mecanismo poderoso para ajudá-lo a saber mais sobre seus clientes, como eles interagem com suas propriedades da Web, ver onde seus gastos com marketing digital são efetivos e identificar áreas de aprimoramento. [!DNL Analytics] lida com trilhões de transações da Web por ano e o ADC permite que você se aprofunde com facilidade nesses dados comportamentais ricos e aprimore os dados [!DNL Real-time Customer Profile] em questão de minutos.

![](./images/analytics-data-experience-platform.png)

Em um nível alto, [!DNL Analytics] coleta dados de vários canais digitais e vários data centers no mundo inteiro. Depois que os dados são coletados, as regras de identificação, segmentação e transformação do Visitante (VISTA) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passam por esse processamento leve, são considerados prontos para consumo por [!DNL Real-time Customer Profile]. Em um processo paralelo ao acima, os mesmos dados processados são agrupados em microlotes e ingeridos em conjuntos de dados da plataforma para consumo por [!DNL Data Science Workspace], [!DNL Query Service]e outros aplicativos de descoberta de dados.

Consulte Visão geral [das regras de](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules.html) processamento para obter mais informações sobre as regras de processamento.

## Modelo de dados de experiência (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo usar para se comunicar com os serviços no [!DNL Experience Platform].

A adesão aos padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a visão geral [do Sistema](../../../xdm/home.md)XDM.

## Como os campos são mapeados do Adobe Analytics para o XDM?

Quando uma conexão de origem é estabelecida para trazer [!DNL Analytics] dados para [!DNL Experience Platform] o uso da interface do [!DNL Platform] usuário, os campos de dados são automaticamente mapeados e assimilados em [!DNL Real-time Customer Profile] minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] o uso da [!DNL Platform] interface do usuário, consulte o tutorial [do conector de dados do](../../tutorials/ui/create/adobe-applications/analytics.md)Analytics.

Para obter informações detalhadas sobre o mapeamento de campos que ocorre entre [!DNL Analytics] e [!DNL Experience Platform], visite o guia de mapeamento [de campos da](./mapping/analytics.md) Adobe Analytics.

## Qual é a latência esperada para os dados do Analytics na plataforma?

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **não** ativado) | &lt; 2 minutos |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **está** ativado) | &lt; 15 minutos |
| Novos dados para Data Lake | &lt; 45 minutos |
| Dados de preenchimento retroativo (13 meses de dados ou 10 bilhões de eventos, o que for menor) | &lt; 4 semanas |

>[!NOTE]
>
>A latência varia dependendo da configuração do cliente, dos volumes de dados e dos aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T` a latência para Pipeline, ela aumentará para 5 a 10 minutos.

## Identificadores principais nos dados do Analytics

Cada ocorrência do conector de dados do Analytics contém um identificador primário que depende da existência de um ECID ou AAID. Se existir um ECID, o ECID é designado como o identificador principal. Se houver um AAID, o AAID será designado como o principal.