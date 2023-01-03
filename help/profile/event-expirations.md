---
keywords: Experience Platform; home; tópicos populares; conjunto de dados; conjunto de dados; tempo de vida; ttl; tempo de vida;
solution: Experience Platform
title: Expirações de evento de experiência
description: Este documento fornece orientação geral sobre como configurar os tempos de expiração de eventos de experiência individuais em um conjunto de dados da Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Expirações de evento de experiência

No Adobe Experience Platform, você pode configurar os tempos de expiração para todos os Eventos de experiência assimilados em um conjunto de dados habilitado para [Perfil do cliente em tempo real](./home.md). Isso permite remover automaticamente os dados da Loja de perfis que não são mais válidos ou úteis para seus casos de uso.

As expirações do evento de experiência não podem ser configuradas por meio da interface do usuário da plataforma ou das APIs. Em vez disso, você deve entrar em contato com o suporte para habilitar as expirações do evento de experiência em seus conjuntos de dados necessários.

>[!IMPORTANT]
>
>As expirações do evento de experiência não devem ser confundidas com as expirações do conjunto de dados, que excluem todo o conjunto de dados após a data de expiração ser atingida. Eles são configurados manualmente por meio de [Higiene dos dados do Adobe Experience Platform](../hygiene/home.md).

## Processo de expiração automatizado

Depois que as expirações do evento de experiência são ativadas em um conjunto de dados habilitado para perfil, a Platform aplica automaticamente os valores de expiração para cada evento capturado em um processo de duas etapas:

1. Todos os novos dados assimilados no conjunto de dados têm o valor de expiração aplicado no momento da assimilação com base no carimbo de data e hora do evento.
1. Todos os dados existentes no conjunto de dados têm o valor de expiração aplicado retroativamente como uma tarefa de sistema de preenchimento retroativo única. Depois que o valor de expiração for colocado no conjunto de dados, os eventos mais antigos que o valor de expiração serão soltos imediatamente assim que o trabalho do sistema for executado. Todos os outros eventos serão descartados assim que atingirem seus valores de expiração no carimbo de data e hora do evento.

>[!WARNING]
>
>Depois de aplicado, todos os dados anteriores ao número de dias alocados pelo valor de expiração são **excluído permanentemente** e não podem ser restauradas.

Por exemplo, se você aplicasse um valor de expiração de 30 dias em 15 de maio, as seguintes etapas ocorriam:

1. Todos os novos eventos recebem um valor de expiração de 30 dias quando são assimilados.
1. Todos os eventos existentes que têm um carimbo de data e hora anterior a 15 de abril são imediatamente excluídos com o trabalho do sistema.
1. Todos os eventos existentes que têm um carimbo de data e hora que é mais recente que 15 de abril têm um valor de expiração de 30 dias após o carimbo de data e hora do evento. Portanto, se um evento tiver um carimbo de data e hora de 18 de abril, ele será excluído 30 dias após a data desse carimbo de data e hora, que seria 18 de maio.

## Efeitos na segmentação

Você deve garantir que as janelas de pesquisa para seus segmentos estejam dentro dos limites de expiração de seus conjuntos de dados dependentes para manter os resultados precisos. Por exemplo, se você aplicar um valor de expiração de 30 dias e tiver um segmento que tenta visualizar dados de até 45 dias atrás, o público resultante provavelmente será impreciso.

Portanto, é necessário manter o mesmo valor de expiração do Evento de experiência para todos os conjuntos de dados, se possível, para evitar o impacto de diferentes valores de expiração em diferentes conjuntos de dados na lógica de segmentação.
