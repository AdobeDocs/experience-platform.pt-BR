---
title: Logon do Adobe Analytics for Target (A4T) no SDK da Web da plataforma
description: Saiba como controlar a coleção de dados do Adobe Analytics for Target (A4T) usando o SDK da Web do Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registro;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Logon do Adobe Analytics for Target (A4T) no SDK da Web da plataforma

Ao usar o Adobe Target para personalização, você pode escolher qual sistema deseja usar para a avaliação de desempenho. Each [Atividade do Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) permite selecionar entre relatórios do Target e relatórios do Adobe Analytics.

Se você estiver usando os relatórios do Analytics, a Adobe Target precisará comunicar o seguinte ao Analytics:

* Qual atividade do Adobe Target seus visitantes inseriram
* Qual experiência eles já viram?
* Qual conversão foi alcançada

O SDK da Web do Adobe Experience Platform oferece suporte a dois tipos de log do Analytics para casos de uso do Analytics for Target (A4T):

| Método de registro | Descrição |
| --- | --- |
| Registro de análises do servidor | Todas as ocorrências do Analytics enviadas pela Rede de borda são aumentadas com detalhes do Target no lado do servidor, sem precisar passar pelo processo de compilação de ocorrências. |
| Registro de análises do cliente | Os dados do Target são retornados no lado do cliente, permitindo aumentar e enviar dados manualmente para o Analytics usando o [API de inserção de dados](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

O método de registro é determinado se você tem o Adobe Analytics ativado na sua [sequência de dados](../../../../datastreams/overview.md):

![Fluxo de decisão do método de registro](../assets/analytics-logging.png)

## Próximas etapas

Este documento forneceu uma breve introdução aos diferentes métodos de registro de dados do A4T no SDK da Web. Para obter informações mais detalhadas sobre cada um desses métodos, consulte a seguinte documentação:

* [Logon do lado do servidor para dados do A4T no SDK da Web da plataforma](./server-side.md)
* [Logon do lado do cliente para dados do A4T no SDK da Web da plataforma](./client-side.md)
