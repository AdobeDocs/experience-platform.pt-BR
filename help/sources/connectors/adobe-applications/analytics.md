---
keywords: Experience Platform, home, tópicos populares, Conector de origem do Analytics, analytics, Analytics
solution: Experience Platform
title: Conector de origem do Adobe Analytics para dados do conjunto de relatórios
topic-legacy: overview
description: Este documento fornece uma visão geral do Analytics e descreve os casos de uso para dados do Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# Conector de origem do Adobe Analytics para dados do conjunto de relatórios

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do conector de origem do Analytics. O [!DNL Analytics] conector de origem envia dados coletados por [!DNL Analytics] para a Plataforma em tempo real, convertendo dados [!DNL Analytics] formatados no SCDS em [!DNL Experience Data Model] (XDM) campos para consumo por Plataforma.

Este documento fornece uma visão geral de [!DNL Analytics] e descreve os casos de uso para dados [!DNL Analytics].

## Dados do Adobe Analytics e do Analytics

[!DNL Analytics] O é um mecanismo poderoso que ajuda você a saber mais sobre seus clientes, como eles interagem com suas propriedades da Web, a ver onde seu investimento em marketing digital é eficaz e a identificar áreas de aprimoramento. [!DNL Analytics] O lida com trilhões de transações da Web por ano e o conector  [!DNL Analytics] de origem permite que você toque facilmente nesses dados comportamentais avançados e enriqueça o  [!DNL Real-time Customer Profile] em questão de minutos.

![](./images/analytics-data-experience-platform.png)

Em um alto nível, [!DNL Analytics] coleta dados de vários canais digitais e vários data centers em todo o mundo. Depois que os dados são coletados, as regras VISTA (Visitor Identification, Segmentation and Transformation Architecture) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passarem por esse processamento leve, eles serão considerados prontos para consumo até [!DNL Real-time Customer Profile]. Em um processo paralelo ao acima, os mesmos dados processados são microlotes e assimilados em conjuntos de dados da plataforma para consumo por [!DNL Data Science Workspace], [!DNL Query Service] e outros aplicativos de detecção de dados.

Consulte a [visão geral das regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obter mais informações sobre as regras de processamento.

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo usar para se comunicar com serviços no Experience Platform.

O cumprimento dos padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a [Visão geral do sistema XDM](../../../xdm/home.md).

## Como os campos são mapeados do Adobe Analytics para o XDM?

Quando uma conexão de origem é estabelecida para trazer os dados [!DNL Analytics] para o Experience Platform usando a interface do usuário da plataforma, os campos de dados são mapeados automaticamente e assimilados em [!DNL Real-time Customer Profile] em minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] usando a interface do usuário da plataforma, consulte o [tutorial do conector de origem do Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obter informações detalhadas sobre o mapeamento de campo que ocorre entre [!DNL Analytics] e o Experience Platform, consulte o guia [Adobe Analytics field mapping](./mapping/analytics.md).

## Qual é a latência esperada para os dados do Analytics na plataforma?

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **não** ativado) | &lt; 2 minutos |
| Novos dados para [!DNL Real-time Customer Profile] (A4T **is** ativado) | &lt; 15 minutos |
| Novos dados para o Data Lake | &lt; 90 minutos |
| Dados de preenchimento retroativo (13 meses de dados ou 10 bilhões de eventos, o que for menor) | &lt; 4 semanas |

>[!NOTE]
>
>A latência varia de acordo com a configuração do cliente, os volumes de dados e os aplicativos do consumidor. Por exemplo, se a implementação [!DNL Analytics] estiver configurada com `A4T` a latência para pipeline aumentará para 5-10 minutos.

## Identificadores primários em dados [!DNL Analytics]

Cada ocorrência do conector de origem [!DNL Analytics] contém um identificador principal que depende da existência de um ECID ou AAID. Se houver uma ECID, a ECID será designada como o identificador principal. Se houver um AAID, o AAID será designado como o principal.
