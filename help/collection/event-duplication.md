---
title: Manipulação de duplicação de eventos no Experience Platform
description: Saiba como o Adobe Experience Platform lida com a duplicação de eventos
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Manipulação de duplicação de eventos no Adobe Experience Platform

O Adobe Experience Platform é um sistema altamente distribuído, projetado para maximizar a confiabilidade e, ao mesmo tempo, dimensionar para volumes de dados cada vez maiores.

Para a coleta de dados em tempo real, os [Eventos de experiência](../xdm/classes/experienceevent.md) são coletados por meio do [Edge Network](../web-sdk/home.md#edge-network), de fontes do lado do cliente, como o [SDK da Web](../web-sdk/home.md) ou o [SDK móvel](https://developer.adobe.com/client-sdks/home/), e entregues às camadas de processamento e armazenamento do Experience Platform. Essas camadas compõem soluções como Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR).

Para minimizar a perda de eventos de experiência, os SDKs do lado do cliente e o serviço de entrega de Experience Platform interno esperam uma confirmação de que um evento foi coletado com êxito.

Se essa confirmação não for recebida, os SDKs do lado do cliente ou o serviço de entrega interno da Platform acionarão uma nova tentativa e o Evento de experiência será enviado novamente.

Essa é uma prática recomendada para lidar com falhas transitórias. O efeito colateral é a possibilidade de introduzir eventos duplicados.

Para entender melhor as práticas recomendadas para lidar com falhas transitórias, consulte este artigo sobre [manipulação de falhas transitórias](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Cenários de duplicação de eventos {#scenarios}

A duplicação de eventos pode ocorrer em vários cenários, como, entre outros:

* Problemas relacionados à rede entre os SDKs do lado do cliente e o [!DNL Edge Network]. Esses problemas podem se originar de falhas do provedor de serviços de Internet, perda de sinal móvel ou outras falhas de rede, já que a conectividade entre o cliente e o Edge Network é feita através da Internet pública.
* Eventos internos de dimensionamento automático de Experience Platform. Ocasionalmente, os dados podem ser rebalanceados devido à volatilidade da infraestrutura em nuvem.

A camada de coleção de dados do Adobe Experience Platform foi projetada para oferecer suporte ao processamento &quot;pelo menos uma vez&quot;. Consequentemente, a duplicação de eventos pode ocorrer em situações limitadas e raras.

Para saber mais sobre o processamento &quot;pelo menos uma vez&quot;, consulte este artigo em [garantias de entrega de mensagens](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Opções de desduplicação de eventos {#deduplication}

Para cenários de negócios sensíveis a eventos duplicados, o Experience Platform usa vários métodos de desduplicação de eventos em seus sistemas de armazenamento downstream, como os descritos abaixo.

* O repositório de perfis da Real-Time CDP remove eventos se um evento com o mesmo `_id` já existir no [!DNL Profile store]. Consulte a documentação da [classe XDM ExperienceEvent](../xdm/classes/experienceevent.md) para obter mais detalhes.
* O Customer Journey Analytics permite que os usuários configurem uma métrica para contar apenas valores de forma não repetitiva. Para saber como fazer isso, consulte a documentação em [configurações do componente de desduplicação de métrica](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=pt-BR).
* O Serviço de consulta Experience Platform oferece suporte à desduplicação de dados quando é necessário remover uma linha inteira de um cálculo ou ignorar um conjunto específico de campos, pois apenas parte dos dados na linha é informação duplicada. Consulte a documentação sobre a [eliminação de duplicação de dados no Serviço de Consulta](../query-service/key-concepts/deduplication.md) para obter mais informações.

>[!NOTE]
>
>Se você estiver tendo problemas de duplicação de eventos fora dos casos de uso apresentados acima, entre em contato com o representante da Adobe e forneça informações detalhadas sobre seu caso de uso.
