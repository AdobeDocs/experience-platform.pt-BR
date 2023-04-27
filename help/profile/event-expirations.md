---
keywords: Experience Platform; home; tópicos populares; conjunto de dados; conjunto de dados; tempo de vida; ttl; tempo de vida;
solution: Experience Platform
title: Expirações de evento de experiência
description: Este documento fornece orientação geral sobre como configurar os tempos de expiração de eventos de experiência individuais em um conjunto de dados da Adobe Experience Platform.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: bb2d0075b234ec750046e1f28cac07a58a9d7e72
workflow-type: tm+mt
source-wordcount: '849'
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
1. Todos os dados existentes no conjunto de dados têm o valor de expiração aplicado retroativamente como uma tarefa de sistema de preenchimento retroativo única. Depois que o valor de expiração for colocado no conjunto de dados, os eventos mais antigos que o valor de expiração serão soltos imediatamente assim que o trabalho do sistema for executado. Todos os outros eventos serão descartados assim que atingirem seus valores de expiração no carimbo de data e hora do evento. Quando todos os Eventos de experiência tiverem sido removidos, se o perfil não tiver mais atributos de perfil, o perfil não existirá mais.

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

## Perguntas frequentes {#faq}

A seção a seguir lista perguntas frequentes sobre a expiração de dados do Evento de experiência:

### Como a expiração dos dados do Evento de experiência difere da expiração dos dados do Perfil pseudônimo?

A expiração dos dados do Evento de experiência e a expiração dos dados do Perfil pseudônimo são recursos complementares.

#### Granularidade

A expiração de dados do Evento de experiência funciona em um **conjunto de dados** nível. Como resultado, cada conjunto de dados pode ter uma configuração de expiração de dados diferente.

A expiração de dados do perfil pseudônimo funciona em um **sandbox** nível. Como resultado, a expiração dos dados afetará todos os perfis na sandbox.

#### Tipos de identidade

A expiração de dados do Evento de experiência remove eventos **only** com base no carimbo de data e hora do registro de eventos. Os namespaces de identidade incluídos são **ignored** para fins de expiração.

Expiração de dados do perfil pseudônimo **only** O considera perfis com gráficos de identidade que contêm namespaces de identidade que foram selecionados pelo cliente, como `ECID`, `AAID`ou outros tipos de cookies. Se o perfil contiver **any** namespace de identidade adicional que era **not** na lista selecionada do cliente, o perfil **not** ser eliminado.

#### Itens removidos

Expiração de dados do evento de experiência **only** remove eventos e faz **not** remover dados de classe de perfil. Os dados da classe de perfil só são removidos quando todos os dados são removidos **all** conjuntos de dados e há **não** registros de classe de perfil restantes para o perfil.

A expiração de dados de perfil pseudônimo remove **both** registros de evento e perfil. Como resultado, os dados da classe de perfil também serão removidos.

### Como a expiração de dados do Perfil Pseudônimo pode ser usada juntamente com a expiração de dados do Evento de Experiência?

A expiração de dados do Perfil pseudônimo e a expiração de dados do Evento de Experiência podem ser usadas para complementar um ao outro.

Você deveria **always** configure a expiração dos dados do Evento de experiência em seus conjuntos de dados, com base nas suas necessidades de retenção de dados sobre seus clientes conhecidos. Depois que os dados do Evento de experiência expirarem, você poderá usar a expiração de dados do Perfil pseudônimo para remover automaticamente os Perfis pseudônimos. Normalmente, o período de expiração dos dados para Perfis pseudônimos é menor que o período de expiração dos dados para Eventos de experiência.

Para um caso de uso típico, você pode definir sua expiração de dados do Evento de experiência com base nos valores de seus dados de usuário conhecidos e pode definir sua expiração de dados do Perfil pseudônimo em um período muito menor para limitar o impacto dos perfis pseudônimos na conformidade com a licença da plataforma.
