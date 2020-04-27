---
title: Ajuda do Adobe Experience Platform Web SDK
seo-title: Ajuda do Adobe Experience Platform Web SDK
description: Saiba o que é o SDK da Web da plataforma Adobe Experience e como ele pode ser usado.
seo-description: permitir que os clientes da Adobe Experience Cloud interajam com os vários serviços na Experience Cloud
translation-type: tm+mt
source-git-commit: 6ad09df6f6867ebe057d0043dea4bc97de2b66b3

---


# (Beta) O que é o SDK da Web da Adobe Experience Platform

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com os vários serviços na Experience Cloud por meio da Adobe Experience Platform Edge Network.

## SDKs substituídos pelo SDK da Web da plataforma Adobe Experience

O SDK da Web da plataforma Adobe Experience substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Isto não é apenas um invólucro em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags disparando na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e gerenciamento de melhor dependência. É uma nova maneira de implementar a Experience Cloud.

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções da Adobe. Antes, o Visitante.js enviava uma chamada de bloqueio para o serviço de ID do visitante, depois o AT.js enviava uma chamada para o Público alvo da Adobe, o DIL.js enviava uma chamada para o Adobe Audiência Manager e, por fim, o AppMeasurement.js enviava uma chamada para o Adobe Analytics. Essa nova biblioteca e terminal podem recuperar uma ID, buscar uma experiência de Público alvo, enviar dados para o Audiência Manager e passar os dados para a Adobe Experience Platform em uma única chamada.