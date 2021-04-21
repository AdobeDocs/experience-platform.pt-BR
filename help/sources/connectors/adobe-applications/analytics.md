---
keywords: Experience Platform, home, tópicos populares, Conector de dados do Analytics, análise, Analytics
solution: Experience Platform
title: Conector de origem do Adobe Analytics para dados do conjunto de relatórios
topic-legacy: overview
description: Este documento fornece uma visão geral do Analytics e descreve os casos de uso para dados do Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---

# Conector Adobe Analytics para dados do conjunto de relatórios

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do ADC (Conector de dados do Analytics). O ADC envia dados coletados por [!DNL Analytics] para [!DNL Platform] em tempo real, convertendo dados [!DNL Analytics] formatados em SCDS em [!DNL Experience Data Model] (XDM) campos para consumo por [!DNL Platform].

Este documento fornece uma visão geral de [!DNL Analytics] e descreve os casos de uso para dados [!DNL Analytics].

## Dados do Adobe Analytics e do Analytics

[!DNL Analytics] O é um mecanismo poderoso para ajudá-lo a saber mais sobre seus clientes, como eles interagem com suas propriedades da Web, ver onde seu investimento em marketing digital é eficaz e identificar áreas de aprimoramento. [!DNL Analytics] O lida com trilhões de transações da Web por ano e o ADC permite que você toque facilmente nesses dados comportamentais avançados e enriqueça o  [!DNL Real-time Customer Profile] em questão de minutos.

![](./images/analytics-data-experience-platform.png)

Em um alto nível, [!DNL Analytics] coleta dados de vários canais digitais e vários data centers em todo o mundo. Depois que os dados são coletados, as regras VISTA (Visitor Identification, Segmentation and Transformation Architecture) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passarem por esse processamento leve, eles serão considerados prontos para consumo até [!DNL Real-time Customer Profile]. Em um processo paralelo ao acima, os mesmos dados processados são microlotes e assimilados em conjuntos de dados da plataforma para consumo por [!DNL Data Science Workspace], [!DNL Query Service] e outros aplicativos de detecção de dados.

Consulte [Visão geral das regras de processamento](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obter mais informações sobre as regras de processamento.

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo usar para se comunicar com serviços em [!DNL Experience Platform].

O cumprimento dos padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a [Visão geral do sistema XDM](../../../xdm/home.md).

## Como os campos são mapeados do Adobe Analytics para o XDM?

Quando uma conexão de origem é estabelecida para trazer [!DNL Analytics] dados para [!DNL Experience Platform] usando a interface do usuário [!DNL Platform], os campos de dados são mapeados automaticamente e assimilados em [!DNL Real-time Customer Profile] em minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] usando a interface do usuário [!DNL Platform], consulte o [tutorial do conector de dados do Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obter informações detalhadas sobre o mapeamento de campo que ocorre entre [!DNL Analytics] e [!DNL Experience Platform], visite o guia [Adobe Analytics field mapping](./mapping/analytics.md).

## Qual é a latência esperada para os dados do Analytics na plataforma?

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **não** ativado) | &lt; 2 minutos |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **is** ativado) | &lt; 15 minutos |
| Novos dados para o Data Lake | &lt; 90 minutos |
| Dados de preenchimento retroativo (13 meses de dados ou 10 bilhões de eventos, o que for menor) | &lt; 4 semanas |

>[!NOTE]
>
>A latência varia de acordo com a configuração do cliente, os volumes de dados e os aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T` a latência para Pipeline aumentará para 5-10 minutos.

## Identificadores primários em dados do Analytics

Cada ocorrência do conector de dados do Analytics contém um identificador principal que depende da existência de uma ECID ou AAID. Se houver uma ECID, a ECID será designada como o identificador principal. Se houver um AAID, o AAID será designado como o principal.
