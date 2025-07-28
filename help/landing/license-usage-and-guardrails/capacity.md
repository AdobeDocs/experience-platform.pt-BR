---
title: Uso e capacidade da licença
description: Saiba mais sobre o uso de sua licença e os limites de capacidade no Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: b3b0792a1a1dd5270dec697539ed58d895814fc8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# Uso e capacidades da licença

No Adobe Experience Platform, as capacidades informam se sua organização excedeu qualquer uma de suas medidas de proteção e fornecem informações sobre como corrigir esses problemas.

Para obter mais informações sobre medidas de proteção no Experience Platform, leia a [visão geral das medidas de proteção do Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportamento da capacidade {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Taxa de transferência de transmissão"
>abstract="O valor da taxa de transferência de transmissão mede o pico combinado de eventos de entrada por segundo para a assimilação de streaming no serviço de perfil, em suas sandboxes de produção e desenvolvimento."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Contagem de público-alvo de transmissão"
>abstract="O número máximo de públicos-alvo de transmissão por sandbox. Esse número inclui o número de públicos-alvo de borda que você tem na sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Públicos da Edge"
>abstract="O número máximo de públicos-alvo de borda por sandbox."

Atualmente, o Capacity oferece suporte aos seguintes serviços:

- Segmentação de transmissão
- Assimilação por transmissão

Nesses serviços, as seguintes medidas de proteção são rastreadas:

- O número máximo de públicos-alvo de transmissão é 500
   - Desses 500 públicos-alvo de transmissão, o número máximo de públicos-alvo de borda é 150
- A taxa de transferência máxima combinada para a segmentação por transmissão é de 1500 registros por segundo (rps)

A capacidade de público-alvo está no nível de **sandbox**. Isso significa que, para cada sandbox que você tem em sua organização, você pode ter 500 públicos-alvo de transmissão, dos quais 150 podem ser públicos-alvo de borda.

A capacidade de taxa de transferência está em um nível de **organização** e pode ser distribuída para suas sandboxes individuais. Por exemplo, com a taxa de transferência de segmentação de transmissão de 1500 rps, é possível definir a sandbox de produção para 1500 rps e a sandbox de desenvolvimento para 150 rps.

O Experience Platform calcula a taxa de transferência da sandbox em intervalos contínuos de 15 minutos. Essa taxa de transferência é medida em tempo real, com os dados sendo atualizados a cada 60 segundos.

Se o uso atingir 80% e 90% da capacidade licenciada, a Experience Platform emitirá um alerta, notificando que você está atingindo o máximo da capacidade especificada. Você pode modificar as configurações para personalizar a porcentagem de capacidade para receber o alerta ou remover o alerta totalmente.

Se o uso ultrapassar 100% da capacidade licenciada, você será considerado em violação da capacidade. Neste ponto, haverá latência de desempenho, e seus destinos de nível de serviço (SLTs) **não** serão garantidos.

## Perguntas frequentes

A seção a seguir descreve as perguntas mais frequentes sobre os recursos da capacidade.

### Posso ter um limite máximo de rendimento combinado que soma até menos do que o máximo do meu público-alvo?

+++ Resposta

Não. O limite máximo de produtividade combinada **deve** somar até a proteção de sua organização.

+++

### O que acontece se eu exceder minhas capacidades máximas?

+++ Resposta

Isso depende de qual capacidade é excedida.

Atualmente, se você exceder o número máximo de públicos-alvo permitidos, seu número excessivo de públicos-alvo não será afetado. No entanto, a capacidade de criar novos públicos-alvo pode ser restrita no futuro.

Se você exceder a taxa de transferência de transmissão, haverá latência de desempenho na assimilação e segmentação.

+++

### Por que devo aderir às minhas capacidades máximas?

+++ Resposta

Trabalhar com o máximo de suas capacidades garante que seus dados permaneçam consistentes e mantenha a integridade dos dados intacta.

Você garante um desempenho consistente durante os eventos de pico, evitando problemas técnicos que poderiam afetar negativamente o desempenho do sistema e afetar suas experiências de clientes downstream, melhorando, em última análise, a higiene dos dados e o desempenho geral do sistema.

+++

### Quais são as práticas recomendadas para gerenciar a taxa de transferência da segmentação por transmissão?

+++ Resposta

Para gerenciar melhor a taxa de transferência da segmentação por transmissão, avalie os conjuntos de dados para garantir que eles estejam priorizando os dados necessários para personalização.


Se o processamento em tempo real não for necessário, você deverá usar a assimilação em lote em vez da assimilação por transmissão.

+++
