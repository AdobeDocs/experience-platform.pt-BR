---
keywords: Experience Platform;início;tópicos populares;coleção de dados;iniciar;sdk da web;;home;popular topics;data collection;launch;web sdk
solution: Experience Platform
title: Visão geral da coleção de dados
description: Saiba mais sobre as várias tecnologias envolvidas na coleta de dados sobre as experiências do cliente no Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 4%

---

# Visão geral da coleção de dados

O Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente de fontes do lado do cliente e enviá-los para o Adobe Experience Platform Edge Network, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou que não sejam da Adobe em segundos.

A coleta de dados é compatível com as seguintes fontes do lado do cliente:

* Aplicativos baseados na Web
* Aplicativos móveis nativos
* Aplicativos Over-the-top (OTT)

A coleta de dados se concentra na descoberta e na acessibilidade de conjuntos de dados assimilados, abrangendo o seguinte:

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html?lang=pt-BR)
* [Tags](../tags/home.md)
* [Sequências de dados](../datastreams/overview.md)
* [Encaminhamento de eventos](../tags/ui/event-forwarding/overview.md)
* [SDK da Web da Adobe Experience Platform](../web-sdk/home.md)
* [SDK móvel da Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/)
* [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Este guia fornece uma introdução de alto nível à coleta de dados e como ela funciona para enviar dados para produtos da Adobe Experience Cloud e aplicativos que não sejam da Adobe por meio do Experience Platform Edge Network.

## Tags, Web SDK e SDK móvel

O Experience Platform Web SDK e o Experience Platform Mobile SDK recolhem e compactam todas as bibliotecas de produtos Adobe em um único kit de desenvolvimento para plataformas móveis e da Web, respectivamente. Eles podem ser implementados com o uso de código bruto ou de [marcas](../tags/home.md) por meio da interface da Coleção de Dados ou da interface do Adobe Experience Platform.

A compactação dessas bibliotecas acelera a coleta de dados e consolida as operações em um único fluxo de dispositivos do lado do cliente para o Experience Platform Edge Network.

![Tags, Web SDK, SDK Móvel](./images/home/tags-sdks.png)

## Experience Platform Edge Network e fluxos de dados {#edge}

O Experience Platform Edge Network é uma rede de servidores distribuídos globalmente, rápida e confiável, capaz de receber e processar dados em enorme escala. Usando tags, você pode configurar [sequências de dados](../datastreams/overview.md) para produtos como Adobe Target, Adobe Audience Manager e Adobe Analytics, que permitem ativar esses produtos no lado do servidor sem alterar o código do lado do cliente.

Além disso, os fluxos de dados são integrados a vários recursos do Experience Platform que ajudam a garantir que todos os dados confidenciais enviados sejam tratados adequadamente de acordo com as políticas organizacionais e os regulamentos legais. Consulte a seção sobre [manipulação de dados confidenciais](../datastreams/overview.md#sensitive) na documentação de sequências de dados para obter mais informações.

![Fluxos de dados e soluções da Adobe](./images/home/adobe-solutions.png)

## Encaminhamento de eventos

O [encaminhamento de eventos](../tags/ui/event-forwarding/overview.md) pode acessar qualquer sequência de dados do Experience Platform, permitindo transformar, enriquecer e enviar dados para qualquer destino que não seja da Adobe com latência extremamente baixa e sem adicionar código de terceiros ao dispositivo cliente.

![Encaminhamento de evento](./images/home/event-forwarding.png)

>[!NOTE]
>
>O encaminhamento de eventos é um recurso pago incluído como parte das ofertas de Conexões da Adobe Real-Time Customer Data Platform, Prime ou Ultimate.

## Próximas etapas

Este documento forneceu uma visão geral de alto nível sobre como a coleta de dados funciona para automatizar o processo de envio dos dados coletados da experiência do cliente para produtos da Adobe e destinos de terceiros.

![Estrutura de coleta de dados](./images/home/collection.png)

Para obter mais informações sobre o fluxo de trabalho geral envolvido no envio de dados do evento por meio da Edge Network, consulte a [visão geral completa](./e2e.md).
