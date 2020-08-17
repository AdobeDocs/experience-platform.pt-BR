---
keywords: web sdk;SDK;web SDK;Launch;launch
title: Ajuda do Adobe Experience Platform Web SDK
seo-title: Ajuda do Adobe Experience Platform Web SDK
description: Saiba o que é o Adobe Experience Platform Web SDK e como ele pode ser usado.
seo-description: permita que os clientes da Adobe Experience Cloud interajam com os vários serviços no Experience Cloud.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---


# O que é o Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com os vários serviços do [!DNL Experience Cloud] por meio da Adobe [!DNL Experience Platform Edge Network]. Além da biblioteca JavaScript, há uma extensão [](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) Launch para ajudar nas configurações do SDK da Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] faz parte da coleção que compõe o Experience Edge. O Experience Edge consiste em três tecnologias:

* **[!DNL Adobe Experience Platform Web SDK]:** Um SDK e uma extensão JavaScript para simplificar consideravelmente [!DNL Launch] as [!DNL Adobe] tecnologias de implantação
* **Adobe Experience Platform Mobile SDK:** Uma extensão do SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[!DNL Adobe Experience Platform Edge Network]:** Uma rede global distribuída de servidores que permite uma nova metodologia de implantação de [!DNL Adobe] produtos

A [!DNL Adobe Experience Edge] é uma nova estrutura para coleta de dados de baixa latência, computação conectável e ativação rápida de dados em todos os canais endereçáveis.

[!DNL Adobe Experience Edge] fornece um único SDK consolidado para cada canal (JavaScript, Mobile, lado do servidor), que envia dados para um domínio Adobe comum (`adobedc.net`) e recebe uma única carga para delivery de dados e experiência.

No lado do servidor, um gateway de borda unificada e uma estrutura de serviços de plataforma comum facilitam o plug-in e a implantação de novos recursos neste ambiente de computação em tempo real.  Essa arquitetura:

* Diminui o tempo de implantação do cliente
* Termina a necessidade de integrações &quot;point&quot;
* Melhora o desempenho em relação às bibliotecas antigas
* Diminui os custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para clientes Adobe

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada.  Ele permite [!DNL Adobe] fornecer serviços com menor custo total de propriedade para os clientes.  Também ajuda a aumentar a velocidade da inovação do produto, tornando a borda em tempo real disponível e permitindo que [!DNL Adobe] e seus clientes adicionem mais rapidamente novos recursos e a lógica definida pelo cliente a esse sistema em tempo real.

## Vídeo de visão geral

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDKs substituídos pelo Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Isto não é apenas um invólucro em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e gerenciamento de melhor dependência. Trata-se de uma nova forma de implementar o acervo comunitário [!DNL Experience Cloud] e é [open source](https://github.com/adobe/alloy).

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções de Adobe. Antes, o Visitante.js enviava uma chamada de bloqueio para o serviço de ID do visitante, depois o AT.js enviava uma chamada para a Adobe Target, o DIL.js enviava uma chamada para a Adobe Audience Manager e, por fim, o AppMeasurement.js enviava uma chamada para a Adobe Analytics. Essa nova biblioteca e terminal podem recuperar uma ID, buscar uma [!DNL Target] experiência, enviar dados para [!DNL Audience Manager]e passar os dados para a Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra o Adobe Experience Platform [!DNL Web SDK] e [!DNL Edge Network] em ação. O exemplo de vídeo usa uma única chamada para Adobe, que envia dados para [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

## Introdução

Recomendamos que você [confira nosso guia](getting-started/quick-start-with-launch.md) de introdução para obter um tutorial rápido sobre como começar a usar o Adobe Launch.

Este produto está em constante evolução e crescendo para suportar cada vez mais casos de uso. Para acompanhar as últimas novidades, verifique nossa placa [de casos de uso](https://github.com/adobe/alloy/projects/5)suportados. Mantemos isso atualizado com os casos de uso que apoiamos atualmente e aqueles em que estamos trabalhando para permitir que você tome as melhores decisões possíveis.

* **Casos De Uso Ainda Não Suportados:** Estes são casos de uso que estão no nosso roteiro para serem apoiados no futuro.
* **Casos De Uso Em Andamento:** Estes são os casos de uso que a equipe está trabalhando para concluir para lançamento.
* **Casos de uso suportados:** Estes são os casos de uso suportados e que funcionam hoje.
* **Casos de uso que não serão suportados:** Estes são os casos de utilização que tomámos a decisão de não apoiar.
