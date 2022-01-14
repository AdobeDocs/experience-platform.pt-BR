---
title: Visão geral do SDK da Web da Adobe Experience Platform
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar os recursos da plataforma ao seu site.
keywords: Adobe Experience Platform Web SDK; Plataforma Web SDK; Web SDK; edge; Visitor.js; AppMeasurement.js; AT.js; DIL.js; Web sdk; SDK; Web SDK; Launch; launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 1048f19e2395f63fac8c4218ed92a546b8071a93
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---

# Visão geral do SDK da Web da Adobe Experience Platform

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes do Adobe Experience Cloud interajam com os vários serviços na [!DNL Experience Cloud] pela rede de borda Adobe Experience Platform. Além da biblioteca do JavaScript, há uma [extensão de tag](./extension/web-sdk-extension-configuration.md) para ajudar nas configurações do SDK da Web.

**Para obter um guia passo a passo sobre como configurar o SDK da Web com tags e enviar dados para as soluções, consulte nosso [Implementar o Adobe Experience Cloud com o tutorial do SDK da Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] é parte da coleção que compõe o Experience Edge. O Experience Edge consiste em três tecnologias:

* **[!DNL Adobe Experience Platform Web SDK]:** Um SDK JavaScript e uma extensão de tag para simplificar consideravelmente a implantação [!DNL Adobe] tecnologias
* **Adobe Experience Platform Mobile SDK:** Uma extensão para o SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[!DNL Adobe Experience Platform Edge Network]:** Uma rede global distribuída de servidores que habilita uma nova metodologia de implantação [!DNL Adobe] products

O [!DNL Adobe Experience Edge] é uma nova estrutura para coleta de dados de baixa latência, computação de plug-in e rápida ativação de dados em todos os canais endereçáveis.

[!DNL Adobe Experience Edge] O fornece um único SDK consolidado para cada canal (JavaScript, Mobile, lado do servidor), que envia dados para um domínio Adobe comum (`adobedc.net`) e recebe uma única carga para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificada e uma estrutura comum de serviços de plataforma facilitam o plug-in e a implantação de novos recursos neste ambiente de computação em tempo real.  Essa arquitetura:

* Diminui o tempo de implantação do cliente
* Encerra a necessidade de integrações &quot;point&quot;
* Melhora o desempenho em comparação às bibliotecas antigas
* Diminui custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para clientes Adobe

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

Isto não é apenas um wrapper em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e melhor gerenciamento de dependência. É uma nova forma de implementar a variável [!DNL Experience Cloud] e é [código aberto](https://github.com/adobe/alloy).

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções do Adobe. Antes, o Visitor.js enviava uma chamada de bloqueio para o serviço de ID de visitante, depois a AT.js enviava uma chamada para a Adobe Target, a DIL.js enviava uma chamada para a Adobe Audience Manager e, por fim, a AppMeasurement.js enviava uma chamada para a Adobe Analytics. Essa nova biblioteca e endpoint podem recuperar uma ID, buscar um [!DNL Target] experiência, enviar dados para [!DNL Audience Manager]e transmita os dados para o Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] em ação. O exemplo de vídeo usa uma única chamada para o Adobe, que envia dados para o [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este produto está em constante evolução e crescimento para suportar cada vez mais casos de uso. Para manter-se atualizado, consulte o [página casos de uso suportados](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Esta página lista os casos de uso que atualmente oferecemos suporte, com links para mais informações quando disponíveis.

* **Casos de uso ainda não suportados:** Esses são casos de uso que estão em nosso roteiro para serem suportados no futuro.
* **Casos De Uso Em Andamento:** Esses são os casos de uso que a equipe está trabalhando atualmente na conclusão do para lançamento.
* **Casos de uso suportados:** Esses são os casos de uso suportados e que funcionam hoje.
* **Casos de uso que não oferecemos suporte:** Foram estes os casos de utilização que tomámos a decisão de não apoiar.
