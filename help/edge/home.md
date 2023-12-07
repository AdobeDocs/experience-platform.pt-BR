---
title: Visão geral do Adobe Experience Platform Web Software Development Kit (SDK)
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar recursos da plataforma ao seu site.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

---

# SDK da Web da Adobe Experience Platform {#overview}

O Adobe Experience Platform Web Software Development Kit (SDK) é uma biblioteca JavaScript do lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com seus serviços por meio da Adobe Experience Platform Edge Network. O Adobe oferece dois métodos para implementar o SDK da Web:

* Implementação manual usando o `alloy.js` Biblioteca JavaScript. Este guia do usuário fornece documentação para esse método de implementação.
* A variável [Extensão de tag do SDK da Web](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Consulte [Implementar o Adobe Experience Cloud com o tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=pt-BR) para obter mais informações.

## Rede de borda Experience Platform {#edge-network}

O SDK da Web do Experience Platform faz parte de uma coleção de ferramentas que compõem a Rede de borda da Adobe Experience Platform. A rede de borda consiste nos seguintes componentes:

* **[Experience Platform Web SDK](#overview):** Um SDK JavaScript e extensão de tag para simplificar consideravelmente a implantação de tecnologias Adobe.
* **[SDK móvel do Experience Platform](https://developer.adobe.com/client-sdks/home/):** Uma extensão para o SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[API do servidor de rede de borda Experience Platform](../server-api/overview.md):** Uma API que pode ser usada para vários casos de uso de coleta de dados, personalização, publicidade e marketing. A API do servidor pode ser usada em servidores, dispositivos IoT, decodificadores de sinais e vários outros dispositivos.

A Edge Network é uma estrutura para coleta de dados de baixa latência, computação conectável e ativação rápida de dados em todos os canais endereçáveis. Ele fornece um único SDK consolidado para cada canal (JavaScript, móvel, lado do servidor), que envia dados para um domínio Adobe comum (`adobedc.net`) e recebe uma única carga de retorno para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificado e uma estrutura comum de serviço da plataforma ajudam a implantar novos recursos nesse ambiente de computação em tempo real. Essa arquitetura:

* Reduz o tempo de implantação do cliente
* Elimina a necessidade de integrações &quot;pontuais&quot;
* Melhora o desempenho em relação às bibliotecas antigas
* Reduz os custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para os clientes do Adobe

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada. Ele também permite que a Adobe forneça serviços com menor custo total de propriedade para os clientes. O sistema de borda foi projetado para acomodar a maioria dos tipos de dados, permitindo mapear seu próprio modelo de dados para ser assimilado por vários produtos de Experience Cloud.

## Vídeo da visão geral {#video}

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas substituídas pelo SDK da Web {#sdks}

O SDK da Web não é apenas um invólucro sobre bibliotecas existentes. É uma nova biblioteca, escrita desde o início para incorporar funcionalidades das bibliotecas existentes. Sua finalidade é acabar com os desafios em que as tags precisam ser acionadas na ordem certa, com a inconsistência entre os desafios de controle de versão da biblioteca e com o melhor gerenciamento de dependência. Trata-se de uma nova forma de implementar a [!DNL Experience Cloud] e é [código aberto](https://github.com/adobe/alloy).

O SDK da Web substitui os seguintes SDKs:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Além de uma nova biblioteca, há um novo endpoint que simplifica as solicitações HTTP para soluções Adobe. Antes, `Visitor.js` enviou uma chamada de bloqueio para o serviço de ID de visitante e `AT.js` enviou uma chamada para a Adobe Target, `DIL.js` enviou uma chamada para o Adobe Audience Manager e, por fim, `AppMeasurement.js` O enviou uma chamada para a Adobe Analytics. Essa nova biblioteca e endpoint podem recuperar uma ID, buscar uma [!DNL Target] experiência, enviar dados para [!DNL Audience Manager]e passe os dados para a Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network] em ação. O exemplo do vídeo usa uma única chamada para o Adobe, que envia dados para o [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migração de bibliotecas existentes para o SDK da Web {#migrating-to-web-sdk}

Para simplificar sua migração de qualquer uma das [bibliotecas existentes](#sdks) para o SDK da Web, o Adobe oferece um caminho de atualização simplificado. Esse caminho permite migrar cada página individual do site para o SDK da Web, sem a necessidade de migrar todo o site de uma só vez. Você pode usar o SDK da Web em uma determinada página, enquanto as bibliotecas existentes residem em outras páginas. Quando estiver pronto, você também poderá migrar essas outras páginas.

### Migração de `AT.js` Considerações sobre o SDK da Web {#considerations}

Antes de migrar páginas que usam `AT.js` ao SDK da Web, habilite as seguintes opções de configuração do SDK da Web. Essas opções garantem que o perfil do visitante seja mantido ao navegar de páginas com `AT.js` para páginas que usam o SDK da Web.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&quot;targetMigrationEnabled&quot;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Os seguintes recursos do Target não são compatíveis ao migrar da at.js para o SDK da Web:
>
>* [Ofertas de redirecionamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=pt-BR)
>* [Suporte a CNAME e entre domínios](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Depois de migrar do `AT.js` ao SDK da Web, remova a variável `targetMigrationEnabled` na sua configuração.
