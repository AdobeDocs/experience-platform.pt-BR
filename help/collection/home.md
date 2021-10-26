---
keywords: Experience Platform, home, tópicos populares, coleta de dados, launch, sdk da web
solution: Experience Platform
title: Visão geral da coleção de dados
topic-legacy: overview
description: Saiba mais sobre as várias tecnologias envolvidas na coleta de dados sobre as experiências do cliente no Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 6%

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
* [SDK móvel da Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Data Model (XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

<!-- (Outdated terminology)
![](./images/Collection.png)
-->

## Implementações mais simples, desempenho mais rápido do lado do cliente

Os SDKs móveis e da Web da Adobe Experience Platform recolhem e compactam todas as bibliotecas de produtos do Adobe em um único kit de desenvolvimento para plataformas móveis ou da Web. A compactação dessas bibliotecas acelera a coleta de dados e consolida as operações em um único fluxo, de dispositivos do lado do cliente para a Adobe Experience Platform Edge Network.

## Processo de mudança para implantar a tecnologia Adobe {#edge}

A Platform Edge Network é uma rede distribuída globalmente, rápida e confiável, de servidores capazes de receber e processar dados em grande escala. Usando tags, você pode configurar [datastreams](../edge/fundamentals/datastreams.md) para produtos como Adobe Target, Adobe Audience Manager e Adobe Analytics, que permitem ativar esses produtos no lado do servidor sem alterar o código do lado do cliente.

<!-- (Outdated terminology)
![](./images/deploy.png)
-->

>[!NOTE]
>
>Para obter uma introdução de alto nível à Rede de borda da plataforma, consulte o seguinte [tour interativo de produtos](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Transformar, enriquecer e enviar dados de forma rápida e segura

[Encaminhamento de eventos no Adobe Experience Platform](../tags/ui/event-forwarding/overview.md) pode tocar em qualquer fluxo de dados da plataforma. Você pode transformar, enriquecer e enviar dados para qualquer destino que não seja Adobe com latência extrema de baixa latência sem adicionar nenhum código de terceiros ao dispositivo cliente, fornecendo coleta e distribuição de dados mais rápida e segura.

<!-- (Outdated terminology)
![](./images/launch.png)
-->