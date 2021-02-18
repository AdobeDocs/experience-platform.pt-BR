---
title: Visão geral do Adobe Experience Platform Web SDK
description: Saiba como usar o Adobe Experience Platform Web SDK para integrar recursos da plataforma ao seu site.
keywords: Adobe Experience Platform Web SDK;Plataforma Web SDK;Web SDK;edge;Visitante.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch;Web SDK;Platform Web SDK;borda;.js;AppMeasurement.js;AT.js;.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---


# Visão geral do Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com os vários serviços no [!DNL Experience Cloud] por meio da Adobe Experience Platform Edge Network. Além da biblioteca JavaScript, há uma [extensão do Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) para ajudar nas configurações do SDK da Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] faz parte da coleção que compõe o Experience Edge. O Experience Edge consiste em três tecnologias:

* **[!DNL Adobe Experience Platform Web SDK]:** Um SDK e  [!DNL Experience Platform Launch] extensão JavaScript para simplificar drasticamente  [!DNL Adobe] as tecnologias de implantação
* **Adobe Experience Platform Mobile SDK:** uma extensão do SDK móvel v5 para permitir que os clientes usem a nova metodologia de implantação
* **[!DNL Adobe Experience Platform Edge Network]:** Uma rede global distribuída de servidores que permite uma nova metodologia de implantação de  [!DNL Adobe] produtos

O [!DNL Adobe Experience Edge] é uma nova estrutura para a coleta de dados de baixa latência, computação conectável e ativação rápida de dados em todos os canais endereçáveis.

[!DNL Adobe Experience Edge] fornece um único SDK consolidado para cada canal (JavaScript, Mobile, lado do servidor), que envia dados para um domínio Adobe comum (`adobedc.net`) e recebe uma única carga para delivery de dados e experiência.

No lado do servidor, um gateway de borda unificada e uma estrutura de serviços de plataforma comum facilitam o plug-in e a implantação de novos recursos neste ambiente de computação em tempo real.  Essa arquitetura:

* Diminui o tempo de implantação do cliente
* Termina a necessidade de integrações &quot;point&quot;
* Melhora o desempenho em relação às bibliotecas antigas
* Diminui os custos
* Aumenta a velocidade da inovação
* Cria vantagens competitivas sustentadas para clientes Adobe

Um único sistema de borda consolidado permite que os clientes gerenciem suas campanhas de publicidade, marketing ou personalização em todos os canais como uma experiência integrada.  Ela permite que [!DNL Adobe] forneça serviços com menor custo total de propriedade para os clientes.  Também ajuda a aumentar a velocidade da inovação de produtos tornando a borda em tempo real disponível e permitindo que [!DNL Adobe] e seus clientes adicionem mais rapidamente novos recursos e a lógica definida pelo cliente a esse sistema em tempo real.

## Vídeo de visão geral

O vídeo a seguir fornece uma visão geral do Adobe Experience Platform [!DNL Web SDK] e do Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDKs substituídos pelo Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK substitui os seguintes SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Isto não é apenas um invólucro em torno das bibliotecas existentes. É uma reescrita completa. Seu objetivo é acabar com os desafios com tags que precisam ser acionadas na ordem correta, inconsistência com os desafios do controle de versão da biblioteca e gerenciamento de melhor dependência. É uma nova maneira de implementar o [!DNL Experience Cloud] e é [open source](https://github.com/adobe/alloy).

Além de uma nova biblioteca, há um novo terminal que simplifica as solicitações HTTP para as soluções de Adobe. Antes, o Visitante.js enviava uma chamada de bloqueio para o serviço de ID do visitante, depois o AT.js enviava uma chamada para a Adobe Target, o DIL.js enviava uma chamada para a Adobe Audience Manager e, por fim, o AppMeasurement.js enviava uma chamada para a Adobe Analytics. Essa nova biblioteca e terminal podem recuperar uma ID, buscar uma experiência [!DNL Target], enviar dados para [!DNL Audience Manager] e passar os dados para a Adobe Experience Platform em uma única chamada.

O vídeo a seguir demonstra Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] em ação. O exemplo de vídeo usa uma única chamada para o Adobe que envia dados para [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este produto está em constante evolução e crescendo para suportar cada vez mais casos de uso. Para acompanhar o que há de mais recente, verifique nossa [placa de casos de uso com suporte](https://github.com/adobe/alloy/projects/5). Mantemos isso atualizado com os casos de uso que apoiamos atualmente e aqueles em que estamos trabalhando para permitir que você tome as melhores decisões possíveis.

* **Casos de uso ainda não suportados:** Esses são casos de uso que estão em nosso roteiro para serem suportados no futuro.
* **Casos de uso em andamento:** Estes são os casos de uso que a equipe está trabalhando atualmente para concluir o lançamento.
* **Casos de uso suportados:** Estes são os casos de uso suportados e que funcionam hoje.
* **Casos de uso que não vamos suportar:** Estes são os casos de uso que tomamos a decisão de não apoiar.
