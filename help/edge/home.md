---
title: Visão geral do SDK da Web da Adobe Experience Platform
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar os recursos da plataforma ao seu site.
keywords: Adobe Experience Platform Web SDK; Plataforma Web SDK; Web SDK; edge; Visitor.js; AppMeasurement.js; AT.js; DIL.js; Web sdk; SDK; Web SDK; Launch; launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 71857ffc5e671f4d9a0502fb95d89d30fdec1f15
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# Visão geral do SDK da Web da Adobe Experience Platform

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes do Adobe Experience Cloud interajam com os vários serviços na [!DNL Experience Cloud] pela rede de borda Adobe Experience Platform. In addition to the JavaScript library, there is a [tag extension](./extension/web-sdk-extension-configuration.md) to help with your Web SDK configurations.

**Para obter um guia passo a passo sobre como configurar o SDK da Web com tags e enviar dados para as soluções, consulte nosso [Implementar o Adobe Experience Cloud com o tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] é parte da coleção que compõe o Experience Edge. Experience Edge consists of three technologies:

* **[!DNL Adobe Experience Platform Web SDK]:** Um SDK JavaScript e uma extensão de tag para simplificar consideravelmente a implantação [!DNL Adobe] tecnologias
* **Adobe Experience Platform Mobile SDK:** Uma extensão para o SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[!DNL Adobe Experience Platform Edge Network]:** A global distributed network of servers that enable a new methodology of deploying [!DNL Adobe] products

The [!DNL Adobe Experience Edge] is a new framework for low-latency data collection, pluggable computing and rapid data activation across all addressable channels.

[!DNL Adobe Experience Edge] provides a single consolidated SDK for every channel (JavaScript, Mobile, Server-side), which sends data to a common Adobe domain (`adobedc.net`) and receives a single payload back for data and experience delivery.

On the server-side, a unified edge gateway and a common platform services framework makes it easy to plug-in and deploy new capabilities into this real-time computing environment.  Essa arquitetura:

* Decreases customer time to value
* Encerra a necessidade de integrações &quot;point&quot;
* Improves performance compared to the old libraries
* Diminui custos
* Increases the speed of innovation
* Creates sustained competitive advantages for Adobe customers

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada.  Permite [!DNL Adobe] fornecer serviços com um custo total de propriedade mais baixo para os clientes.  Também ajuda a aumentar a velocidade da inovação do produto ao tornar a borda em tempo real disponível e permitir [!DNL Adobe] e seus clientes para adicionar mais rapidamente novos recursos e lógica definida pelo cliente a esse sistema em tempo real.

## Vídeo de visão geral

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDKs substituídos pelo Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

This is not just a wrapper around existing libraries. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e melhor gerenciamento de dependência. É uma nova forma de implementar a variável [!DNL Experience Cloud] e é [código aberto](https://github.com/adobe/alloy).

In addition to a new library, there is a new endpoint that streamlines the HTTP requests to Adobe solutions. Antes, o Visitor.js enviava uma chamada de bloqueio para o serviço de ID de visitante, depois a AT.js enviava uma chamada para a Adobe Target, a DIL.js enviava uma chamada para a Adobe Audience Manager e, por fim, a AppMeasurement.js enviava uma chamada para a Adobe Analytics. This new library and endpoint can retrieve an ID, fetch a [!DNL Target] experience, send data to [!DNL Audience Manager], and pass the data to Adobe Experience Platform in a single call.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] em ação. O exemplo de vídeo usa uma única chamada para o Adobe, que envia dados para o [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este produto está em constante evolução e crescimento para suportar cada vez mais casos de uso. To keep up with the latest and see what we currently support, see the [supported use cases page](https://github.com/orgs/adobe/projects/18/views/1).
