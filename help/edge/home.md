---
title: Visão geral do SDK da Web da Adobe Experience Platform
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar recursos da plataforma ao seu site.
keywords: SDK da Web da Adobe Experience Platform;SDK da Web da plataforma;borda;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;SDK da Web;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Visão geral do SDK da Web do Adobe Experience Platform {#overview}

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript no lado do cliente que permite aos clientes da Adobe Experience Cloud interagir com os vários serviços na [!DNL Experience Cloud] por meio da Rede de borda da Adobe Experience Platform. Além da biblioteca do JavaScript, há uma [extensão de tag](./extension/web-sdk-extension-configuration.md) para ajudar nas configurações do SDK da Web.

Para obter um guia passo a passo para configurar o SDK da Web com tags e enviar dados para as soluções, consulte nosso [Implementar o Adobe Experience Cloud com o tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>Esse produto está em constante evolução e crescimento para oferecer suporte a mais e mais casos de uso. Para acompanhar as atualizações mais recentes e ver o que oferecemos suporte no momento, consulte a [página de casos de uso suportados](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] O faz parte da coleção que compõe a [!DNL Adobe Experience Edge]. [!DNL Experience Edge] O consiste nas seguintes tecnologias:

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** Um SDK JavaScript e uma extensão de tag para simplificar consideravelmente a implantação [!DNL Adobe] tecnologias.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** Uma extensão para o SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** Uma rede global distribuída de servidores que possibilita uma nova metodologia de implantação [!DNL Adobe] products

A variável [!DNL Adobe Experience Edge] O é uma nova estrutura para coleta de dados de baixa latência, computação conectável e ativação rápida de dados em todos os canais endereçáveis.

[!DNL Adobe Experience Edge] O fornece um único SDK consolidado para cada canal (JavaScript, Mobile, lado do servidor), que envia dados para um domínio de Adobe comum (`adobedc.net`) e recebe uma única carga de retorno para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificado e uma estrutura comum de serviços da plataforma facilitam a conexão e a implantação de novos recursos nesse ambiente de computação em tempo real.  Essa arquitetura:

* Reduz o tempo de implantação do cliente
* Elimina a necessidade de integrações &quot;pontuais&quot;
* Melhora o desempenho em relação às bibliotecas antigas
* Reduz os custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para os clientes do Adobe

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada. Ele permite [!DNL Adobe] para fornecer serviços com menor custo total de propriedade para os clientes.  Também ajuda a aumentar a velocidade da inovação do produto, tornando a borda em tempo real conectável e permitindo [!DNL Adobe] e seus clientes para adicionar mais rapidamente novos recursos e lógica definida pelo cliente a esse sistema em tempo real.

## Vídeo de visão geral {#video}

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas substituídas pelo SDK da Web {#sdks}

O SDK da Web não é apenas um invólucro sobre bibliotecas existentes. É uma biblioteca completamente nova, escrita desde o início para incorporar funcionalidades das bibliotecas existentes. Sua finalidade é acabar com os desafios em que as tags precisam ser acionadas na ordem certa, com a inconsistência entre os desafios de controle de versão da biblioteca e com o melhor gerenciamento de dependência. Trata-se de uma nova forma de implementar a [!DNL Experience Cloud] e é [código aberto](https://github.com/adobe/alloy).

O SDK da Web substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Além de uma nova biblioteca, há um novo endpoint que simplifica as solicitações HTTP para soluções Adobe. Antes, o Visitor.js enviava uma chamada de bloqueio para o serviço de ID de visitante, em seguida, o AT.js enviava uma chamada para o Adobe Target, o DIL.js enviava uma chamada para o Adobe Audience Manager e, por fim, o AppMeasurement.js enviava uma chamada para o Adobe Analytics. Essa nova biblioteca e endpoint podem recuperar uma ID, buscar uma [!DNL Target] experiência, enviar dados para [!DNL Audience Manager]e passe os dados para a Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network] em ação. O exemplo do vídeo usa uma única chamada para o Adobe, que envia dados para o [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migração de bibliotecas existentes para o SDK da Web {#migrating-to-web-sdk}

Para simplificar sua migração de qualquer uma das [bibliotecas existentes](#sdks) para o SDK da Web, o Adobe oferece um caminho de atualização simplificado, permitindo migrar cada página individual do site para o SDK da Web, sem a necessidade de migrar todo o site de uma só vez.

Isso significa que você pode usar o SDK da Web em uma página e deixar as bibliotecas existentes nas outras páginas, até que também possa migrá-las.

### Considerações sobre a migração do at.js para o SDK da Web {#considerations}

Antes de migrar páginas que usam [!DNL at.js] ao SDK da Web, habilite as seguintes opções de configuração do SDK da Web. Isso garante que o perfil do visitante seja mantido ao navegar de páginas com [!DNL at.js ] para páginas que usam o SDK da Web.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&quot;targetMigrationEnabled&quot;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Os seguintes recursos do Target não são compatíveis ao migrar da at.js para o SDK da Web:
> * [Ofertas de redirecionamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [Suporte a CNAME e entre domínios](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


Depois de migrar do at.js para o SDK da Web, você deve remover o `targetMigrationEnabled` na sua configuração.



