---
keywords: Experience Platform, home, tópicos populares, coleta de dados, launch, sdk da web
solution: Experience Platform
title: Visão geral da coleção de dados
topic-legacy: overview
description: Saiba mais sobre as várias tecnologias envolvidas na coleta de dados sobre as experiências do cliente no Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# Visão geral da coleta de dados

O Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente de fontes do lado do cliente e enviá-los para a Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe em segundos.

A coleta de dados é compatível com as seguintes fontes do lado do cliente:

* Aplicativos baseados na Web
* Aplicativos móveis nativos
* Aplicativos OTT (Over-the-top)

As tecnologias de coleta de dados fornecidas pelo Experience Platform se concentram na descoberta e acessibilidade de conjuntos de dados assimilados. Essas tecnologias incluem o seguinte:

* [Rede de borda Adobe Experience Platform](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tags](../tags/home.md)
* [Encaminhamento de evento](../tags/ui/event-forwarding/overview.md)
* [SDK da Web da Adobe Experience Platform](../edge/home.md)
* [Experience Data Model (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Implementações mais simples, desempenho mais rápido do lado do cliente

Os SDKs móveis e da Web da Adobe Experience Platform recolhem e compactam todas as bibliotecas de produtos do Adobe em um único kit de desenvolvimento para plataformas móveis ou da Web. A compactação dessas bibliotecas acelera a coleta de dados e consolida as operações em um único fluxo, de dispositivos do lado do cliente para a Adobe Experience Platform Edge Network.

## Processo de mudança para implantar a tecnologia Adobe

A Platform Edge Network é uma rede distribuída globalmente, rápida e confiável, de servidores capazes de receber e processar dados em grande escala. Usando tags, você pode configurar [datastreams](../edge/fundamentals/datastreams.md) para produtos como Adobe Target, Adobe Audience Manager e Adobe Analytics, que permitem ativar esses produtos no lado do servidor sem alterar o código do lado do cliente.

![](./images/deploy.png)

## Transformar, enriquecer e enviar dados de forma rápida e segura

[O encaminhamento de eventos na Adobe Experience ](../tags/ui/event-forwarding/overview.md) Platform pode entrar em qualquer fluxo de dados da plataforma. Você pode transformar, enriquecer e enviar dados para qualquer destino que não seja Adobe com latência extrema de baixa latência sem adicionar nenhum código de terceiros ao dispositivo cliente, fornecendo coleta e distribuição de dados mais rápida e segura.

![](./images/launch.png)
