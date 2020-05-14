---
title: Ajuda do Adobe Experience Platform Web SDK
seo-title: Ajuda do Adobe Experience Platform Web SDK
description: Saiba o que é o SDK da Web da plataforma Adobe Experience e como ele pode ser usado.
seo-description: permita que os clientes da Adobe Experience Cloud interajam com os vários serviços na Experience Cloud.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# O que é o SDK da Web da Adobe Experience Platform

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com os vários serviços na Experience Cloud por meio da Adobe Experience Platform Edge Network.

## SDKs substituídos pelo SDK da Web da plataforma Adobe Experience

O SDK da Web da plataforma Adobe Experience substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Isto não é apenas um invólucro em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags disparando na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e gerenciamento de melhor dependência. É uma nova maneira de implementar a Experience Cloud e é de código [aberto](https://github.com/adobe/alloy)

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções da Adobe. Antes, o Visitante.js enviava uma chamada de bloqueio para o serviço de ID do visitante, depois o AT.js enviava uma chamada para o Público alvo da Adobe, o DIL.js enviava uma chamada para o Adobe Audiência Manager e, por fim, o AppMeasurement.js enviava uma chamada para o Adobe Analytics. Essa nova biblioteca e terminal podem recuperar uma ID, buscar uma experiência de Público alvo, enviar dados para o Audiência Manager e passar os dados para a Adobe Experience Platform em uma única chamada.

## Introdução

Recomendamos que você [faça check-out do nosso guia](getting-started/quick-start-with-launch.md) de introdução para obter um tutorial rápido sobre como começar a usar a inicialização.

Este produto está em constante evolução e crescendo para suportar cada vez mais casos de uso. Para acompanhar o que há de mais recente, fazemos check-out do nosso quadro [de casos de uso](https://github.com/adobe/alloy/projects/5)suportados. Mantemos isso atualizado com os casos de uso que atualmente apoiamos e aqueles em que estamos trabalhando para permitir que você tome as melhores decisões possíveis.

* __Casos de uso ainda não suportados__ - são casos de uso que estão em nosso roteiro a ser feito no futuro.
* __Casos de uso em andamento__ - Estes são os casos de uso que a equipe está trabalhando atualmente para concluir o lançamento.
* __Casos__ de uso suportados - Estes são os casos de uso suportados e que funcionam hoje.
* __Casos de uso que não vamos suportar__ - Estes são os casos de uso que tomamos a decisão de não apoiar.
