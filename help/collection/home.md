---
keywords: Experience Platform, home, tópicos populares, coleta de dados, launch, sdk da web
solution: Experience Platform
title: Visão geral da coleta de dados
topic: overview
description: Saiba mais sobre as várias tecnologias envolvidas na coleta de dados sobre as experiências do cliente no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 629fe68029a9f45e45d5e2d238ffff455c7d6de6
workflow-type: tm+mt
source-wordcount: '321'
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
* [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en)
* [SDK da Web da Adobe Experience Platform](../edge/home.md)
* [Experience Data Model (XDM)](../xdm/home.md)

![](./images/Collection.png)

## Implementações mais simples, desempenho mais rápido do lado do cliente

Os SDKs móveis e da Web da Adobe Experience Platform recolhem e compactam todas as bibliotecas de produtos do Adobe em um único kit de desenvolvimento para plataformas móveis ou da Web. A compactação dessas bibliotecas acelera a coleta de dados e consolida as operações em um único fluxo, de dispositivos do lado do cliente para a Adobe Experience Platform Edge Network.

## Processo de mudança para implantar a tecnologia Adobe

A Platform Edge Network é uma rede distribuída globalmente, rápida e confiável, de servidores capazes de receber e processar dados em grande escala. Usando o Platform launch, você pode configurar [configurações de borda](../edge/fundamentals/edge-configuration.md) para produtos como Adobe Target, Adobe Audience Manager e Adobe Analytics, que permitem ativar esses produtos no lado do servidor sem alterar o código do lado do cliente.

![](./images/deploy.png)

## Transformar, enriquecer e enviar dados de forma rápida e segura

[O Adobe Experience Platform Launch Server ](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html) Sidecan pode tocar em qualquer fluxo de dados da plataforma. Você pode transformar, enriquecer e enviar dados para qualquer destino que não seja Adobe com latência extrema de baixa latência sem adicionar nenhum código de terceiros ao dispositivo cliente, fornecendo coleta e distribuição de dados mais rápida e segura.

![](./images/launch.png)