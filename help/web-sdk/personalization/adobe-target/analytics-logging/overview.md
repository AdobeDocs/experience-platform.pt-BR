---
title: Logon do Adobe Analytics for Target (A4T) no Experience Platform Web SDK
description: Saiba como controlar a coleção de dados do Adobe Analytics for Target (A4T) usando o Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registro;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Logon do Adobe Analytics for Target (A4T) no Experience Platform Web SDK

Ao usar o Adobe Target para personalização, você pode escolher qual sistema deseja usar para a avaliação de desempenho. Cada [Atividade do Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) permite selecionar entre relatórios do Target e do Adobe Analytics.

Se você estiver usando os relatórios do Analytics, a Adobe Target precisará comunicar o seguinte ao Analytics:

* Qual atividade do Adobe Target seus visitantes inseriram
* Qual experiência eles já viram?
* Qual conversão foi alcançada

O Adobe Experience Platform Web SDK é compatível com dois tipos de registro do Analytics para casos de uso do Analytics for Target (A4T):

| Método de registro | Descrição |
| --- | --- |
| Registro de análises do servidor | Todas as ocorrências do Analytics enviadas pelo Edge Network são aumentadas com detalhes do Target no lado do servidor, sem precisar passar pelo processo de compilação de ocorrências. |
| Registro de análises do cliente | Os dados de destino são retornados no lado do cliente, permitindo que você aumente e envie dados manualmente para o Analytics usando a [API de inserção de dados](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

O método de log é determinado se você tem o Adobe Analytics habilitado na sua [sequência de dados](../../../../datastreams/overview.md) configurada:

![Fluxo de decisão do método de log](../assets/analytics-logging.png)

## Próximas etapas

Este documento forneceu uma breve introdução aos diferentes métodos de registro de dados do A4T no Web SDK. Para obter informações mais detalhadas sobre cada um desses métodos, consulte a seguinte documentação:

* [Logon do lado do servidor para dados do A4T no Experience Platform Web SDK](./server-side.md)
* [Logon do lado do cliente para dados do A4T no Experience Platform Web SDK](./client-side.md)
