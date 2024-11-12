---
title: Visão geral do Adobe Experience Platform Web Software Development Kit (SDK)
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar recursos da plataforma ao seu site.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 2bf9c7ada9fd223df92b5cc9b1415f20705c2042
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# SDK da Web da Adobe Experience Platform {#overview}

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com seus serviços por meio do Edge Network Adobe Experience Platform.

Você pode implementar o SDK da Web de duas maneiras:

* A [extensão de tag do SDK da Web](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Consulte o tutorial sobre como [implementar o Adobe Experience Cloud com o SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR) para obter mais informações.
* Implementação manual usando a [biblioteca JavaScript do SDK da Web](install/library.md).

Este guia inclui instruções para interagir com soluções Experience Cloud usando a biblioteca JavaScript do SDK da Web e a extensão de tag.

## Edge Network Experience Platform {#edge-network}



O SDK da Web do Experience Platform faz parte do Edge Network Adobe Experience Platform, que inclui:

* **[SDK da Web do Experience Platform](#overview)**: uma biblioteca JavaScript e extensão de tag para simplificar a implantação da tecnologia Adobe.
* **[SDK móvel do Experience Platform](https://developer.adobe.com/client-sdks/home/)**: uma extensão para o SDK móvel v5 para a nova metodologia de implantação.
* **[API Edge Network](../server-api/overview.md)**: uma API do lado do servidor para casos de uso de coleta de dados, personalização, publicidade e marketing. Você pode usá-lo em servidores, dispositivos IoT, decodificadores de sinais e outros dispositivos.

O Edge Network fornece coleta de dados de baixa latência, computação conectável e ativação rápida de dados em todos os canais endereçáveis. Ele oferece um único SDK consolidado para canais da Web, móveis e do lado do servidor, enviando dados para um domínio Adobe comum (`adobedc.net`) e recebendo uma única carga para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificado e uma estrutura de serviço de plataforma comum simplificam a implantação de novos recursos, enquanto oferecem os seguintes benefícios:

* redução do tempo de implantação do cliente;
* Acabar com a necessidade de integrações &quot;pontuais&quot;;
* Melhoria do desempenho em relação às bibliotecas antigas;
* Redução dos custos operacionais;
* Aumentar a velocidade da inovação;
* Criando vantagens competitivas sustentadas para os clientes do Adobe.

Um sistema de borda consolidado permite gerenciar campanhas de publicidade, marketing e personalização em todos os canais. Ele reduz o custo total de propriedade e oferece suporte a vários tipos de dados, permitindo mapear seu modelo de dados para uso com vários produtos de Experience Cloud.

## Visão geral do vídeo {#video}

Assista ao vídeo abaixo para obter uma visão geral do Adobe Experience Platform [!DNL Web SDK] e do [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas substituídas pelo SDK da Web {#sdks}

O SDK da Web é uma nova biblioteca de código aberto criada do zero para integrar funcionalidades de bibliotecas existentes. Ele soluciona problemas de ordem de disparo de tags, inconsistência de versão e gerenciamento de dependência, oferecendo uma nova maneira [open source](https://github.com/adobe/alloy) de implementar o [!DNL Experience Cloud].

O SDK da Web substitui:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Ele também apresenta um novo endpoint que simplifica as solicitações HTTP para soluções Adobe. Anteriormente, várias chamadas eram necessárias para `Visitor.js`, `AT.js`, `DIL.js` e `AppMeasurement.js`. Agora, uma única chamada pode recuperar uma ID, buscar uma experiência do [!DNL Target], enviar dados para o [!DNL Audience Manager] e passar dados para o Adobe Experience Platform.

Assista ao vídeo abaixo para ver o Adobe Experience Platform [!DNL Web SDK] e [!DNL Edge Network] em ação, usando uma única chamada para enviar dados para [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migração de bibliotecas existentes para o SDK da Web {#migrating-to-web-sdk}

O Adobe oferece um caminho de atualização simplificado para simplificar sua migração de qualquer uma das [bibliotecas existentes](#sdks) para o SDK da Web. Você pode migrar cada página do seu site individualmente, sem precisar migrar o site inteiro de uma só vez. Você pode usar o SDK da Web em algumas páginas, enquanto as bibliotecas existentes permanecem em outras, permitindo uma transição gradual.

### Migração de `AT.js` para considerações do SDK da Web {#considerations}

Antes de migrar páginas usando o `AT.js` para o SDK da Web, habilite as seguintes opções de configuração do SDK da Web para garantir que o perfil do visitante seja mantido ao navegar entre páginas.

* [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&quot;targetMigrationEnabled&quot;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Os seguintes recursos do Target não têm suporte ao migrar do `at.js` para o SDK da Web:
>
>* [Ofertas de redirecionamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=pt-BR)
>* [Suporte a CNAME e entre domínios](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Depois de migrar do `AT.js` para o SDK da Web, remova a opção `targetMigrationEnabled` da sua configuração.
