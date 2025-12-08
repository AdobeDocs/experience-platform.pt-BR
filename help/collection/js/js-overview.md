---
title: Visão geral da biblioteca JavaScript do Web SDK
description: Envie dados para o Adobe Experience Platform Edge Network usando o JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Visão geral da biblioteca JavaScript do Web SDK

A **Adobe Experience Platform Web SDK** é uma biblioteca JavaScript do lado do cliente que permite enviar dados para o Adobe Experience Platform Edge Network. Este guia documenta o caminho de implementação da biblioteca JavaScript do Web SDK (`alloy.js`), incluindo conceitos, instalação, configuração e comandos principais. Para obter a extensão de tag do Web SDK na interface da Coleção de dados, consulte a [extensão de tag do Web SDK](/help/tags/extensions/client/web-sdk/overview.md).

O Web SDK envia dados de maneira independente de solução (XDM) para o Experience Platform Edge Network, que mapeia os dados para formatos e destinos específicos da solução e os envia em tempo real.

## Experience Platform Edge Network {#edge-network}

O Adobe Experience Platform Edge Network fornece coleta de dados de baixa latência, computação conectável e ativação rápida de dados em todos os canais endereçáveis. Ele oferece uma única SDK consolidada para canais da Web, móveis e do lado do servidor, enviando dados para um domínio comum do Adobe (`adobedc.net`) e recebendo uma única carga para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificado e uma estrutura de serviço de plataforma comum simplificam a implantação de novos recursos, enquanto oferecem os seguintes benefícios:

* redução do tempo de implantação do cliente;
* Acabar com a necessidade de integrações &quot;pontuais&quot;;
* Melhoria do desempenho em relação às bibliotecas antigas;
* Redução dos custos operacionais;
* Aumentar a velocidade da inovação;
* Criar vantagens competitivas sustentadas para os clientes da Adobe.

Um sistema de borda consolidado permite gerenciar campanhas de publicidade, marketing e personalização em todos os canais. Ele reduz o custo total de propriedade e aceita vários tipos de dados, permitindo mapear seu modelo de dados para uso com vários produtos da Experience Cloud.

>[!VIDEO](https://video.tv.adobe.com/v/37265?captions=por_br&quality=12&learn=on)

## Bibliotecas substituídas pelo Web SDK {#sdks}

O Web SDK é uma biblioteca de código aberto criada do zero para integrar funcionalidades de bibliotecas existentes. Ele soluciona problemas de ordem de acionamento de tags, inconsistência de versão e gerenciamento de dependência, oferecendo uma maneira de implementar muitos produtos da Experience Cloud. O Web SDK substitui a coleta de dados dos seguintes serviços:

* Serviço de ID de visitante da Adobe Experience Platform (`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

Ele também apresenta um novo endpoint que simplifica as solicitações HTTP para soluções da Adobe. Anteriormente, várias chamadas eram necessárias para cada biblioteca de coleta de dados. Agora, uma única chamada pode recuperar uma ID, buscar uma experiência do [!DNL Target], enviar dados para o [!DNL Audience Manager] e passar dados para o Adobe Experience Platform.

## Migração de bibliotecas existentes para o Web SDK {#migrating-to-web-sdk}

O Adobe oferece um caminho de atualização simplificado para simplificar sua migração de qualquer uma das bibliotecas existentes para o Web SDK. Você pode migrar cada página do seu site individualmente, sem precisar migrar o site inteiro de uma só vez. Você pode usar o Web SDK em algumas páginas, enquanto as bibliotecas existentes permanecem em outras, permitindo uma transição gradual.
