---
title: Adobe Analytics View in Assurance
description: Este guia explica como usar o Adobe Analytics com o Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# Visualização do Adobe Analytics no Assurance

A integração do Adobe Experience Platform Assurance com o Adobe Analytics fornece uma visualização mais avançada dos eventos do SDK para os usuários que depuram e validam a implementação do Adobe Analytics. A exibição agora mostra eventos de ciclo de vida e de ação/estado enviados para o Adobe Analytics pelo [ADOBE EXPERIENCE PLATFORM SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). A exibição também apresenta detalhes de &quot;resposta&quot; que fornecem informações sobre como os eventos foram processados após a aplicação das respectivas regras de processamento do conjunto de relatórios.

![](./images/adobe-analytics/overview.png)

## Introdução

Antes de continuar, verifique se você tem os seguintes serviços:

- A variável [Interface da coleção de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para saber como instalar o Assurance em seu aplicativo, leia o [guia de implementação do Assurance](../tutorials/implement-assurance.md).

## Status pós-processado

Depois que o SDK fizer uma solicitação de rede com o Adobe Analytics, o status informará se o Assurance conseguiu recuperar as informações de pós-processamento da solicitação do Adobe Analytics.

Observe que para recuperar informações pós-processamento, o usuário conectado deve ter acesso ao conjunto de relatórios correspondente.

| Status | Descrição |
| :----- | :---------- |
| `Queued` | A solicitação de rede está buscando as informações de pós-processamento. |
| `Processed` | A solicitação de rede foi bem-sucedida e as informações de pós-processamento são recebidas. |
| `Delayed` | O número máximo de tentativas de solicitações para buscar as informações de pós-processamento foi excedido. |
| `Error` | Um erro causou a falha na solicitação de rede. Mais detalhes sobre o erro são exibidos na visualização de detalhes do evento. |
| `Unauthorized` | O usuário não tem acesso ao conjunto de relatórios do Adobe Analytics. |
| `Unavailable` | A solicitação Adobe Analytics não tem um correspondente `AnalyticsResponse` evento. |
| `No Debug Flag` | A versão atual do Adobe Analytics ou do Assurance SDK pode não ser compatível com o recurso de depuração do Analytics. Para obter mais informações, leia a [Guia de solução de problemas](../troubleshooting.md). |
| `Expired` | A variável `AnalyticsTrack` ou `LifecycleStart` tiver mais de 24 horas. |

## Exibição de detalhes do evento

Para um evento de rastreamento do Analytics, a exibição detalhada contém as seguintes partes valiosas:

- Um evento de solicitação de SDK do Analytics de origem.
- Metadados e dados de contexto OOTB da solicitação, como ID do conjunto de relatórios, versões de extensão do SDK, dados de contexto OOTB e assim por diante.
- Informações pós-processadas sobre o evento do Analytics que contêm o mapeamento de revars, evars, props e assim por diante.
