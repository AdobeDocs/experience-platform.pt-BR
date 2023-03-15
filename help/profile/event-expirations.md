---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;tempo de vida;ttl;time-to-live;
solution: Experience Platform
title: Expirações do evento de experiência
description: Este documento fornece orientação geral sobre como configurar tempos de expiração para eventos de experiência individuais em um conjunto de dados do Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 0fce883528abc62075914abc4a8f81d2bff8f2e6
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Expirações do evento de experiência

No Adobe Experience Platform, você pode configurar os tempos de expiração para todos os Eventos de experiência que são assimilados em um conjunto de dados habilitado para [Perfil do cliente em tempo real](./home.md). Isso permite remover automaticamente dados da Loja de perfis que não são mais válidos ou úteis para seus casos de uso.

As expirações de evento de experiência não podem ser configuradas por meio da interface do usuário da plataforma ou das APIs. Em vez disso, você deve entrar em contato com o suporte para ativar as expirações do evento de experiência nos conjuntos de dados necessários.

>[!IMPORTANT]
>
>As expirações de evento de experiência não devem ser confundidas com as expirações de conjunto de dados, que excluem o conjunto de dados inteiro após a data de expiração ser atingida. Eles são configurados manualmente por meio de [Higiene de dados do Adobe Experience Platform](../hygiene/home.md).

## Processo de expiração automatizado

Depois que as expirações de evento de experiência são ativadas em um conjunto de dados habilitado para perfil, o Platform aplica automaticamente os valores de expiração para cada evento capturado em um processo de duas etapas:

1. Todos os novos dados assimilados no conjunto de dados têm o valor de expiração aplicado no momento da assimilação com base no carimbo de data e hora do evento.
1. Todos os dados existentes no conjunto de dados têm o valor de expiração aplicado retroativamente como um trabalho único do sistema de preenchimento retroativo. Depois que o valor de expiração for colocado no conjunto de dados, os eventos mais antigos que o valor de expiração serão descartados imediatamente assim que o trabalho do sistema for executado. Todos os outros eventos serão ignorados assim que atingirem seus valores de expiração no carimbo de data e hora do evento. Quando todos os eventos de experiência forem removidos, se o perfil não tiver mais atributos de perfil, o perfil não existirá mais.

>[!WARNING]
>
>Depois de aplicados, todos os dados anteriores ao número de dias alocados pelo valor de expiração serão **excluído permanentemente** e não podem ser restaurados.

Por exemplo, se você aplicasse um valor de expiração de 30 dias em 15 de maio, as seguintes etapas ocorreriam:

1. Todos os novos eventos recebem um valor de expiração de 30 dias aplicados conforme são assimilados.
1. Todos os eventos existentes com um carimbo de data e hora anterior a 15 de abril são imediatamente excluídos com o trabalho do sistema.
1. Todos os eventos existentes com um carimbo de data e hora mais recente que 15 de abril têm um valor de expiração 30 dias após o carimbo de data e hora do evento. Portanto, se um evento tiver um carimbo de data e hora de 18 de abril, ele será excluído 30 dias após a data desse carimbo, que seria 18 de maio.

## Efeitos na segmentação

Você deve garantir que as janelas de retrospectiva dos segmentos estejam dentro dos limites de expiração de seus conjuntos de dados dependentes para manter os resultados precisos. Por exemplo, se você aplicar um valor de expiração de 30 dias e tiver um segmento que tenta visualizar dados de até 45 dias atrás, o público-alvo resultante provavelmente será impreciso.

Portanto, você deve manter o mesmo valor de expiração do evento de experiência para todos os conjuntos de dados, se possível, para evitar o impacto de valores de expiração diferentes em conjuntos de dados diferentes na lógica de segmentação.
