---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;tempo de vida;ttl;time-to-live;
solution: Experience Platform
title: Expirações do evento de experiência
description: Este documento fornece orientação geral sobre como configurar tempos de expiração para eventos de experiência individuais em um conjunto de dados do Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 05479dcfd1a375b3589ce212168f324aa72af4ba
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# Expirações do evento de experiência

No Adobe Experience Platform, você pode configurar as horas de expiração para todos os Eventos de experiência que são assimilados em um conjunto de dados habilitado para o [Perfil de cliente em tempo real](./home.md). Isso permite remover automaticamente dados do armazenamento de Perfil que não são mais válidos ou úteis para seus casos de uso.

Para saber como gerenciar as expirações do Evento de experiência em seus conjuntos de dados, leia o [guia da interface do usuário do conjunto de dados](../catalog/datasets/user-guide.md#data-retention-policy).

>[!IMPORTANT]
>
>As expirações de evento de experiência não devem ser confundidas com as expirações de conjunto de dados, que excluem o conjunto de dados inteiro após a data de expiração ser atingida. Eles são configurados manualmente por meio da [Limpeza de Dados do Adobe Experience Platform](../hygiene/home.md).

## Processo de expiração automatizado

Depois que as expirações de evento de experiência são ativadas em um conjunto de dados habilitado para perfil, o Experience Platform aplica automaticamente os valores de expiração para cada evento capturado em um processo de duas etapas:

1. Todos os novos dados assimilados no conjunto de dados têm o valor de expiração aplicado no momento da assimilação com base no carimbo de data e hora do evento.
1. Todos os dados existentes no conjunto de dados têm o valor de expiração aplicado retroativamente como um trabalho único do sistema de preenchimento retroativo. Depois que o valor de expiração for colocado no conjunto de dados, os eventos mais antigos que o valor de expiração serão descartados imediatamente assim que o trabalho do sistema for executado. Todos os outros eventos serão ignorados assim que atingirem seus valores de expiração no carimbo de data e hora do evento. Quando todos os eventos de experiência forem removidos, se o perfil não tiver mais atributos de perfil, o perfil não existirá mais.

>[!WARNING]
>
>Uma vez aplicados, todos os dados anteriores ao número de dias alocados pelo valor de expiração são **permanentemente excluídos** e não podem ser restaurados.

Por exemplo, se você aplicasse um valor de expiração de 30 dias em 15 de maio, as seguintes etapas ocorreriam:

1. Todos os novos eventos recebem um valor de expiração de 30 dias aplicados conforme são assimilados.
1. Todos os eventos existentes com um carimbo de data e hora anterior a 15 de abril são imediatamente excluídos com o trabalho do sistema.
1. Todos os eventos existentes com um carimbo de data e hora mais recente que 15 de abril têm um valor de expiração 30 dias após o carimbo de data e hora do evento. Portanto, se um evento tiver um carimbo de data e hora de 18 de abril, ele será excluído 30 dias após a data desse carimbo, que seria 18 de maio.

## Efeitos na segmentação

Você deve garantir que as janelas de retrospectiva para seus públicos-alvo estejam dentro dos limites de expiração de seus conjuntos de dados dependentes para manter os resultados precisos. Por exemplo, se você aplicar um valor de expiração de 30 dias e tiver um público-alvo que tente visualizar dados de até 45 dias atrás, o público-alvo resultante provavelmente será impreciso.

Portanto, você deve manter o mesmo valor de expiração do evento de experiência para todos os conjuntos de dados, se possível, para evitar o impacto de valores de expiração diferentes em conjuntos de dados diferentes na lógica de segmentação.

## Perguntas frequentes {#faq}

A seção a seguir lista as perguntas frequentes sobre a expiração dos dados do evento de experiência:

### Qual é a duração mínima para a qual posso definir a expiração de dados de um evento de experiência?

A duração mínima para uma expiração de dados de Evento de experiência é **um dia**.

### Como a expiração de dados do Evento de experiência difere da expiração de dados do Perfil de pseudônimo?

A expiração de dados do evento de experiência e a expiração de dados do perfil de pseudônimo são recursos complementares.

#### Granularidade

A expiração de dados do Evento de experiência funciona em um nível de **conjunto de dados**. Como resultado, cada conjunto de dados pode ter uma configuração de expiração de dados diferente.

A expiração de dados do Perfil de pseudônimo funciona em um nível de **sandbox**. Como resultado, a expiração dos dados afetará todos os perfis na sandbox.

#### Tipos de identidade

A expiração de dados do Evento de experiência remove os eventos **only** com base no carimbo de data/hora do registro do evento. Os namespaces de identidade incluídos são **ignorados** para fins de expiração.

A expiração de dados de Perfil pseudônimo **only** considera perfis que têm gráficos de identidade que contêm namespaces de identidade selecionados pelo cliente, como `ECID`, `AAID` ou outros tipos de cookies. Se o perfil contiver **qualquer** namespace de identidade adicional que fosse **não** na lista selecionada pelo cliente, o perfil **não** será excluído.

#### Itens Removidos

A expiração de dados do Evento de Experiência **only** remove eventos e **not** remove dados da classe de perfil. Os dados da classe de perfil só são removidos quando todos os dados são removidos em **todos** conjuntos de dados e há **não** registros de classe de perfil restantes para o perfil.

A expiração de dados de Perfil pseudônimo remove **ambos** registros de evento e perfil. Como resultado, os dados da classe de perfil também serão removidos.

### Como a expiração de dados do Perfil de pseudônimo pode ser usada juntamente com a expiração de dados do Evento de experiência?

A expiração de dados do perfil de pseudônimo e a expiração de dados do evento de experiência podem ser usadas para se complementar.

Você deve **sempre** configurar a expiração dos dados do Evento de experiência em seus conjuntos de dados, com base nas suas necessidades de retenção de dados sobre clientes conhecidos. Depois que a expiração de dados do evento de experiência for configurada, você poderá usar a expiração de dados do perfil de pseudônimo para remover automaticamente os perfis de pseudônimo. Normalmente, o período de expiração dos dados para perfis pseudônimos é menor que o período de expiração dos dados para eventos de experiência.

Para um caso de uso típico, você pode definir a expiração de dados do evento de experiência com base nos valores dos dados do usuário conhecidos e pode definir a expiração de dados do perfil pseudônimo para uma duração muito mais curta, a fim de limitar o impacto dos perfis pseudônimos na conformidade com a licença do Experience Platform.
