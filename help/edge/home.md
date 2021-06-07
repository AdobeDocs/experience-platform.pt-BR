---
title: Visão geral do SDK da Web da Adobe Experience Platform
description: Saiba como usar o SDK da Web da Adobe Experience Platform para integrar os recursos da plataforma ao seu site.
keywords: Adobe Experience Platform Web SDK; Plataforma Web SDK; Web SDK; edge; Visitor.js; AppMeasurement.js; AT.js; DIL.js; Web sdk; SDK; Web SDK; Launch; launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7607f01109de1f6207f2e910a8620698c60b89d4
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---

# Visão geral do SDK da Web da Adobe Experience Platform

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes do Adobe Experience Cloud interajam com os vários serviços no [!DNL Experience Cloud] por meio da rede de borda Adobe Experience Platform. Além da biblioteca do JavaScript, há uma [extensão do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) para ajudar com suas configurações do SDK da Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] é parte da coleção que compõe o Experience Edge. O Experience Edge consiste em três tecnologias:

* **[!DNL Adobe Experience Platform Web SDK]:** um SDK e  [!DNL Experience Platform Launch] extensão do JavaScript para simplificar bastante  [!DNL Adobe] as tecnologias de implantação
* **Adobe Experience Platform Mobile SDK:** uma extensão para o SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[!DNL Adobe Experience Platform Edge Network]** Uma rede global distribuída de servidores que permite uma nova metodologia de implantação de  [!DNL Adobe] produtos

O [!DNL Adobe Experience Edge] é uma nova estrutura para coleta de dados de baixa latência, computação de plug-in e rápida ativação de dados em todos os canais endereçáveis.

[!DNL Adobe Experience Edge] O fornece um único SDK consolidado para cada canal (JavaScript, Mobile, lado do servidor), que envia dados para um domínio Adobe comum (`adobedc.net`) e recebe um único payload para entrega de dados e experiência.

No lado do servidor, um gateway de borda unificada e uma estrutura comum de serviços de plataforma facilitam o plug-in e a implantação de novos recursos neste ambiente de computação em tempo real.  Essa arquitetura:

* Diminui o tempo de implantação do cliente
* Encerra a necessidade de integrações &quot;point&quot;
* Melhora o desempenho em comparação às bibliotecas antigas
* Diminui custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para clientes Adobe

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada.  Ele permite que [!DNL Adobe] forneça serviços com custo total de propriedade mais baixo para os clientes.  Também ajuda a aumentar a velocidade da inovação do produto, tornando a borda em tempo real disponível e permitindo que [!DNL Adobe] e seus clientes adicionem mais rapidamente novos recursos e lógica definida pelo cliente a esse sistema em tempo real.

## Vídeo de visão geral

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e do Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDKs substituídos pelo Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Isto não é apenas um wrapper em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e melhor gerenciamento de dependência. É uma nova maneira de implementar o [!DNL Experience Cloud] e é [open source](https://github.com/adobe/alloy).

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções do Adobe. Antes, o Visitor.js enviava uma chamada de bloqueio para o serviço de ID de visitante, depois a AT.js enviava uma chamada para a Adobe Target, a DIL.js enviava uma chamada para a Adobe Audience Manager e, por fim, a AppMeasurement.js enviava uma chamada para a Adobe Analytics. Essa nova biblioteca e terminal podem recuperar uma ID, buscar uma experiência [!DNL Target], enviar dados para [!DNL Audience Manager] e enviar os dados para a Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e o Adobe Experience Platform [!DNL Edge Network] em ação. O exemplo de vídeo usa uma única chamada para o Adobe, que envia dados para [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este produto está em constante evolução e crescimento para suportar cada vez mais casos de uso. Para manter-se atualizado, consulte a [página de casos de uso suportados](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Esta página lista os casos de uso que atualmente oferecemos suporte, com links para mais informações quando disponíveis.

* **Casos de uso ainda não suportados:** esses são casos de uso que estão em nosso roteiro para serem suportados no futuro.
* **Casos de uso em andamento:** esses são os casos de uso que a equipe está trabalhando atualmente para concluir o lançamento.
* **Casos de uso suportados:** esses são os casos de uso suportados e que funcionam hoje.
* **Casos de uso que não oferecemos suporte:** esses são os casos de uso que tomamos a decisão de não apoiar.
