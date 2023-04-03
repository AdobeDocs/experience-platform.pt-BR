---
title: Exibição do Adobe Analytics no Assurance
description: Este guia explica como usar o Adobe Analytics com o Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---


# Exibição do Adobe Analytics no Assurance

A integração do Adobe Experience Platform Assurance com o Adobe Analytics fornece uma exibição mais rica dos eventos do SDK para os usuários que depuram e validam sua implementação do Adobe Analytics. A exibição agora mostra eventos de ciclo de vida e ação/estado enviados para o Adobe Analytics a partir do [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). A exibição também apresenta detalhes de &quot;resposta&quot; que fornecem informações sobre como os eventos foram processados após a aplicação das respectivas regras de processamento do conjunto de relatórios.

![](./images/adobe-analytics/overview.png)

## Introdução

Antes de continuar, verifique se você tem os seguintes serviços:

- O [Interface do usuário da coleta de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Para saber como instalar o Assurance no seu aplicativo, leia o [guia de controle de execução](../tutorials/implement-assurance.md).

## Status pós-processado

Depois que o SDK fizer uma solicitação de rede com o Adobe Analytics, o status informará se o Assurance foi capaz de recuperar as informações de pós-processamento da solicitação do Adobe Analytics.

Observe que para recuperar informações pós-processamento, o usuário conectado deve ter acesso ao conjunto de relatórios correspondente.

| Status | Descrição |
| :----- | :---------- |
| `Queued` | A solicitação de rede está buscando informações pós-processamento. |
| `Processed` | A solicitação de rede foi bem-sucedida e as informações de pós-processamento são recebidas. |
| `Delayed` | O número máximo de solicitações que tentam obter as informações de pós-processamento foi excedido. |
| `Error` | Um erro causou a falha da solicitação de rede. Mais detalhes sobre o erro são exibidos na visualização de detalhes do evento. |
| `Unauthorized` | O usuário não tem acesso ao conjunto de relatórios do Adobe Analytics. |
| `Unavailable` | A solicitação do Adobe Analytics não tem um `AnalyticsResponse` evento. |
| `No Debug Flag` | A versão atual do Adobe Analytics ou do SDK do Assurance pode não ser compatível com o recurso de Depuração do Analytics. Para obter mais informações, leia o [Guia de solução de problemas](../troubleshooting.md). |
| `Expired` | O `AnalyticsTrack` ou `LifecycleStart` tiver mais de 24 horas. |

## Exibição de detalhes do evento

Para um evento de rastreamento do Analytics, a exibição detalhada contém as seguintes partes valiosas:

- Um evento de solicitação de SDK Analytics de origem.
- Metadados e dados de contexto do OOTB da solicitação, como ID do conjunto de relatórios, versões de extensão do SDK, dados de contexto do OOTB e assim por diante.
- Informações pós-processadas sobre o evento do Analytics que contém o mapeamento de revars, evars, props e assim por diante.
