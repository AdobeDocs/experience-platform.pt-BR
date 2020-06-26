---
title: Ajuda do Adobe Experience Platform Web SDK
seo-title: Ajuda do Adobe Experience Platform Web SDK
description: Saiba o que é o Adobe Experience Platform Web SDK e como ele pode ser usado.
seo-description: permita que os clientes da Adobe Experience Cloud interajam com os vários serviços no Experience Cloud.
translation-type: tm+mt
source-git-commit: 3f52def8318f57cfc6534e15415d172e768a8614
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# O que é o Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com os vários serviços na Experience Cloud por meio da Adobe Experience Platform Edge Network.

## SDKs substituídos por Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Isto não é apenas um invólucro em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e gerenciamento de melhor dependência. É uma nova forma de implementar o Experience Cloud e é [open source](https://github.com/adobe/alloy).

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções da Adobe. Antes, o Visitante.js enviava uma chamada de bloqueio para o serviço de ID do visitante, depois o AT.js enviava uma chamada para o Adobe Target, o DIL.js enviava uma chamada para o Adobe Audience Manager e, por fim, o AppMeasurement.js enviava uma chamada para o Adobe Analytics. Essa nova biblioteca e terminal podem recuperar uma ID, buscar uma [!DNL Target] experiência, enviar dados para o Audience Manager e passar os dados para o Adobe Experience Platform em uma única chamada.

## Introdução

Recomendamos que você [confira nosso guia](getting-started/quick-start-with-launch.md) de introdução para obter um tutorial rápido sobre como começar a usar o Adobe Launch.

Este produto está em constante evolução e crescendo para suportar cada vez mais casos de uso. Para acompanhar as últimas novidades, verifique nossa placa [de casos de uso](https://github.com/adobe/alloy/projects/5)suportados. Mantemos isso atualizado com os casos de uso que apoiamos atualmente e aqueles em que estamos trabalhando para permitir que você tome as melhores decisões possíveis.

* __Casos de uso ainda não suportados__ - Esses são casos de uso que estão em nosso roteiro para serem suportados no futuro.
* __Casos de uso em andamento__ - Estes são os casos de uso que a equipe está trabalhando atualmente para concluir o lançamento.
* __Casos__ de uso suportados - Estes são os casos de uso suportados e que funcionam hoje.
* __Casos de uso que não vamos suportar__ - Estes são os casos de uso que tomamos a decisão de não apoiar.
