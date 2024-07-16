---
keywords: Experience Platform;página inicial;tópicos populares;coleção de dados;iniciar;sdk da web
solution: Experience Platform
title: Visão geral da coleção de dados
description: Saiba mais sobre as várias tecnologias envolvidas na coleta de dados sobre as experiências do cliente no Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 5%

---

# Visão geral da coleção de dados

O Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente de fontes do lado do cliente e enviá-los para o Edge Network da Adobe Experience Platform, onde podem ser enriquecidos, transformados e distribuídos para destinos Adobe ou não Adobe em segundos.

A coleta de dados é compatível com as seguintes fontes do lado do cliente:

* Aplicativos baseados na Web
* Aplicativos móveis nativos
* Aplicativos Over-the-top (OTT)

A coleta de dados se concentra na descoberta e na acessibilidade de conjuntos de dados assimilados, abrangendo o seguinte:

* [Edge Network Adobe Experience Platform](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Tags](../tags/home.md)
* [Sequências de dados](../datastreams/overview.md)
* [Encaminhamento de eventos](../tags/ui/event-forwarding/overview.md)
* [SDK da Web da Adobe Experience Platform](../web-sdk/home.md)
* [SDK móvel da Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/)
* [API do servidor da rede de borda](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform Assurance](../assurance/home.md)


Este guia fornece uma introdução de alto nível à coleta de dados e como ela funciona para enviar dados para produtos Adobe Experience Cloud e aplicativos não-Adobe pelo Edge Network da plataforma.

## Tags, SDK da Web e SDK móvel

O SDK da Web da Platform e o SDK móvel da Platform recolhem e compactam todas as bibliotecas de produtos do Adobe em um único kit de desenvolvimento para plataformas móveis e da Web, respectivamente. Eles podem ser implementados com o uso de código bruto ou de [marcas](../tags/home.md) por meio da interface da Coleção de Dados ou da interface do Adobe Experience Platform.

A compactação dessas bibliotecas acelera a coleta de dados e consolida as operações em um único fluxo de dispositivos do lado do cliente para o Edge Network da plataforma.

![Tags, SDK da Web, SDK móvel](./images/home/tags-sdks.png)

## Edge Network da plataforma e fluxos de dados {#edge}

O Platform Edge Network é uma rede de servidores distribuídos globalmente, rápida e confiável, capaz de receber e processar dados em tremenda escala. Usando tags, você pode configurar [sequências de dados](../datastreams/overview.md) para produtos como Adobe Target, Adobe Audience Manager e Adobe Analytics, que permitem ativar esses produtos no lado do servidor sem alterar o código do lado do cliente.

Além disso, os fluxos de dados são integrados a vários recursos da Platform que ajudam a garantir que todos os dados confidenciais enviados sejam tratados adequadamente de acordo com as políticas organizacionais e os regulamentos legais. Consulte a seção sobre [manipulação de dados confidenciais](../datastreams/overview.md#sensitive) na documentação de sequências de dados para obter mais informações.

![Fluxos de dados e soluções de Adobe](./images/home/adobe-solutions.png)

>[!NOTE]
>
>Para obter uma introdução de alto nível ao Edge Network da Platform, consulte o seguinte [tour interativo do produto](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## Encaminhamento de eventos

O [encaminhamento de eventos](../tags/ui/event-forwarding/overview.md) pode acessar qualquer sequência de dados de Experience Platform, permitindo transformar, enriquecer e enviar dados para qualquer destino que não seja de Adobe com latência extremamente baixa e sem adicionar código de terceiros ao dispositivo cliente.

![Encaminhamento de evento](./images/home/event-forwarding.png)

>[!NOTE]
>
>O encaminhamento de eventos é um recurso pago incluído como parte das ofertas do Adobe Real-time Customer Data Platform Connections, Prime ou Ultimate.

## Próximas etapas

Este documento forneceu uma visão geral de alto nível sobre como a coleta de dados funciona para automatizar o processo de envio dos dados coletados da experiência do cliente para produtos Adobe e destinos de terceiros.

![Estrutura de coleta de dados](./images/home/collection.png)

Para obter mais informações sobre o fluxo de trabalho geral envolvido no envio de dados do evento por meio do Edge Network, consulte a [visão geral completa](./e2e.md).
