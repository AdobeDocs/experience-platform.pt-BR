---
title: Visão geral do SDK da Web da Adobe Experience Platform
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar os recursos da plataforma ao seu site.
keywords: Adobe Experience Platform Web SDK; Plataforma Web SDK; Web SDK; edge; Visitor.js; AppMeasurement.js; AT.js; DIL.js; Web sdk; SDK; Web SDK; Launch; launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Visão geral do SDK da Web da Adobe Experience Platform {#overview}

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes do Adobe Experience Cloud interajam com os vários serviços na [!DNL Experience Cloud] pela rede de borda Adobe Experience Platform. Além da biblioteca do JavaScript, há uma [extensão de tag](./extension/web-sdk-extension-configuration.md) para ajudar nas configurações do SDK da Web.

Para obter um guia passo a passo sobre como configurar o SDK da Web com tags e enviar dados para as soluções, consulte nosso [Implementar o Adobe Experience Cloud com o tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>Este produto está em constante evolução e crescimento para suportar cada vez mais casos de uso. Para saber mais sobre as últimas novidades e ver o que oferecemos suporte atualmente, consulte o [página casos de uso suportados](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] faz parte da coleção que compõe a variável [!DNL Adobe Experience Edge]. [!DNL Experience Edge] consiste nas seguintes tecnologias:

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** Um SDK JavaScript e uma extensão de tag para simplificar consideravelmente a implantação [!DNL Adobe] tecnologias.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** Uma extensão para o SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** Uma rede global distribuída de servidores que habilita uma nova metodologia de implantação [!DNL Adobe] products

O [!DNL Adobe Experience Edge] é uma nova estrutura para coleta de dados de baixa latência, computação de plug-in e rápida ativação de dados em todos os canais endereçáveis.

[!DNL Adobe Experience Edge] O fornece um único SDK consolidado para cada canal (JavaScript, Mobile, lado do servidor), que envia dados para um domínio Adobe comum (`adobedc.net`) e recebe uma única carga para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificada e uma estrutura comum de serviços de plataforma facilitam o plug-in e a implantação de novos recursos neste ambiente de computação em tempo real.  Essa arquitetura:

* Diminui o tempo de implantação do cliente
* Encerra a necessidade de integrações &quot;point&quot;
* Melhora o desempenho em comparação às bibliotecas antigas
* Diminui custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para clientes Adobe

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada. Permite [!DNL Adobe] fornecer serviços com um custo total de propriedade mais baixo para os clientes.  Também ajuda a aumentar a velocidade da inovação do produto ao tornar a borda em tempo real disponível e permitir [!DNL Adobe] e seus clientes para adicionar mais rapidamente novos recursos e lógica definida pelo cliente a esse sistema em tempo real.

## Vídeo de visão geral {#video}

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas substituídas pelo SDK da Web {#sdks}

O SDK da Web não é apenas um wrapper em torno das bibliotecas existentes. É uma biblioteca completamente nova, escrita desde o início para incorporar funcionalidades de bibliotecas existentes. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e melhor gerenciamento de dependência. É uma nova forma de implementar a variável [!DNL Experience Cloud] e é [código aberto](https://github.com/adobe/alloy).

O Web SDK substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções do Adobe. Antes, o Visitor.js enviava uma chamada de bloqueio para o serviço de ID de visitante, depois a AT.js enviava uma chamada para a Adobe Target, a DIL.js enviava uma chamada para a Adobe Audience Manager e, por fim, a AppMeasurement.js enviava uma chamada para a Adobe Analytics. Essa nova biblioteca e endpoint podem recuperar uma ID, buscar um [!DNL Target] experiência, enviar dados para [!DNL Audience Manager]e transmita os dados para o Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] em ação. O exemplo de vídeo usa uma única chamada para o Adobe, que envia dados para o [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migração de bibliotecas existentes para o SDK da Web {#migrating-to-web-sdk}

Para simplificar sua migração de qualquer uma das [bibliotecas existentes](#sdks) para o SDK da Web, o Adobe oferece um caminho de atualização simplificado, permitindo migrar cada página individual do seu site para o SDK da Web, sem a necessidade de migrar todo o seu site ao mesmo tempo.

Isso significa que você pode usar o SDK da Web em uma página e deixar as bibliotecas existentes em outras páginas, até que também possa migrá-las.

### Considerações sobre a migração da at.js para o SDK da Web {#considerations}

Antes de migrar as páginas que usam [!DNL at.js] para o SDK da Web, ative as seguintes opções de configuração do SDK da Web. Isso garante que o perfil do visitante seja mantido ao navegar de páginas com [!DNL at.js ] para páginas que usam o SDK da Web.

* [`idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [`targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Os seguintes recursos do Target não são compatíveis ao migrar da at.js para o SDK da Web:
> * [Ofertas de redirecionamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [Suporte CNAME e entre domínios](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


Depois de migrar da at.js para o SDK da Web, você deve remover o `targetMigrationEnabled` na sua configuração.



