---
description: Saiba como identificar e resolver antipadrões comuns de configuração de agendamento de trabalho no Adobe Experience Platform.
solution: Experience Platform
title: Identificar Antipadrões de Programação de Job
type: Tutorial
exl-id: f94e3ef3-2252-46f5-8075-45b5483d9d83
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identificar superescritos da programação de trabalho

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] estão disponíveis no momento apenas para os seguintes trabalhos do Real-Time CDP:
>
> * Assimilação em lote de data lake
> * Assimilação de perfil em lote
> * Segmentação em lote
> * Ativação do destino de lote

A exibição da linha do tempo [Cronogramas de trabalho](job-schedules.md) ajuda a identificar problemas comuns de configuração que podem afetar negativamente o desempenho e a confiabilidade do seu pipeline de dados. Esses antipadrões geralmente levam a falhas de trabalho, inconsistências de dados ou degradação do desempenho do sistema. Ao detectar esses padrões antecipadamente, você pode reconfigurar seus jobs para evitar problemas antes que eles afetem suas operações de negócios.

## Pré-requisitos {#prerequisites}

Antes de identificar antipadrões, você deve:

* Ter acesso a [!UICONTROL Job Schedules] com a **[!UICONTROL View Job Schedules]** [permissão de controle de acesso](/help/access-control/home.md#permissions).
* Familiarize-se com a [interface de Agendamentos de Trabalho](job-schedules.md#understanding-interface) e como ler a exibição da linha do tempo.
* Entenda os conceitos básicos de [assimilação em lote](../ingestion/batch-ingestion/overview.md), [segmentação](../segmentation/home.md) e [processamento de perfil](../profile/home.md).

## Referência rápida {#anti-pattern-quick-reference}

| Anti- padrão | O que você verá na linha do tempo | Impacto principal | Severidade |
|--------------|----------------------------------|----------------|----------|
| [Sobreposição de agendamento](#schedule-overlap-pattern) | Vários trabalhos em execução simultaneamente | Contenção de recursos e falhas de trabalho | Alto |
| [Densidade do trabalho agendado](#scheduled-density) | Vários conjuntos de dados com lotes agrupados na mesma hora | Gargalos de pipeline e segmentação incompleta | Alto |
| [Lotes excessivos por conjunto de dados](#excessive-batches-per-dataset) | Conjunto de dados único com dezenas de lotes diários | Complexidade operacional e de processamento ineficiente | Médio |

## Sobreposição de agendamento {#schedule-overlap-pattern}

**Severidade do impacto**: Alta | **Problema principal**: Contenção de recursos

**O que procurar**: vários trabalhos agendados para execução ao mesmo tempo ou em estreita sucessão, especialmente quando os trabalhos com muitos recursos se sobrepõem.

Um exemplo comum são os trabalhos de assimilação em lote em execução ao mesmo tempo que um trabalho de segmentação programado. Isso cria contenção de recursos porque ambas as operações exigem capacidade de processamento e memória significativas.

**Por que isso é problemático**:

* **Contenção de recursos**: quando vários trabalhos com muitos recursos são executados simultaneamente, eles competem pelos recursos do sistema (CPU, memória, E/S), tornando a execução mais lenta de todos os trabalhos.
* **Desempenho imprevisível**: a duração do trabalho se torna inconsistente, dificultando o planejamento de agendamentos confiáveis.
* **Atrasos em cascata**: se os trabalhos demorarem mais do que o esperado, eles poderão atrasar os trabalhos dependentes de downstream, criando um efeito de ondulação em todo o pipeline.
* **Risco de falha aumentado**: o esgotamento de recursos pode fazer com que os trabalhos atinjam o tempo limite ou falhem completamente.

**Como corrigir**:

* **Agendas de trabalho escalonadas**: certifique-se de que as operações com uso intensivo de recursos sejam executadas sequencialmente em vez de simultaneamente.
* **Adicionar tempo de buffer**: deixe um espaçamento adequado entre os trabalhos para levar em conta as variações de processamento.
* **Revisar dependências**: identifique quais trabalhos devem ser concluídos antes que outros possam iniciar com segurança.

## Densidade do trabalho agendado {#scheduled-density}

**Severidade do impacto**: Alta | **Problema principal**: Gargalos de pipeline

**O que procurar**: muitos conjuntos de dados com vários lotes agendados na mesma hora, principalmente quando esses lotes são empilhados próximos e agendados próximo a janelas de processamento críticas, como horas de início de segmentação.

Normalmente, esse padrão inclui:

* Vários conjuntos de dados, cada um executando vários lotes por dia
* Trabalhos ETL (assimilação de data lake e assimilação de perfil) clusterizados na mesma hora
* Assimilação em lote programada imediatamente antes ou durante as janelas de segmentação programada

**Por que isso é problemático**:

* **Gargalo de pipeline**: quando vários lotes de diferentes conjuntos de dados são empilhados em uma janela de tempo curta, eles criam um gargalo de processamento que pode sobrecarregar o pipeline de assimilação.
* **Disponibilidade de perfil atrasada**: trabalhos de assimilação de perfil que são executados muito perto dos horários de início da segmentação podem não ser concluídos a tempo, resultando em avaliações de público-alvo incompletas ou obsoletas.
* **Segmentação imprevisível**: se os trabalhos de assimilação de upstream ainda estiverem em execução quando a segmentação começar, você corre o risco de avaliar os públicos com relação a dados incompletos, resultando em associação incorreta de público.
* **Falhas em cascata**: um único lote atrasado em um agendamento densamente empilhado pode causar um efeito dominó, atrasando todos os lotes subsequentes e processos downstream.
* **Esforço de recursos**: o sistema pode ter dificuldades para alocar recursos suficientes ao processar muitos trabalhos de assimilação simultâneos, resultando em tempos de processamento mais lentos ou falhas.

**Como corrigir**:

* **Consolidar lotes**: reduza a frequência do lote combinando vários lotes pequenos em lotes menores e maiores por conjunto de dados.
* **Distribuir uniformemente**: espalhe os trabalhos de assimilação ao longo do dia, em vez de agrupá-los em horas específicas.
* **Adicionar tempo de buffer**: garanta um buffer mínimo de 1 a 2 horas entre a conclusão da assimilação de perfil e o início da segmentação.
* **Requisitos de revisão**: avalie se todos os conjuntos de dados realmente precisam de vários lotes diários. Muitos casos de uso funcionam com menos atualizações frequentes.

## Lotes excessivos por conjunto de dados {#excessive-batches-per-dataset}

**Severidade do impacto**: Medium | **Problema principal**: Processamento ineficiente

**O que procurar**: um único conjunto de dados com um número excessivo de trabalhos em lotes individuais agendados ao longo do dia, criando uma longa pilha vertical de trabalhos na linha do tempo.

Esse padrão envolve um único conjunto de dados com muitos trabalhos individuais de assimilação em lotes agendados em intervalos frequentes, às vezes dezenas de lotes por dia.

**Por que isso é problemático**:

* **Processamento ineficiente**: cada trabalho em lotes tem custos indiretos (inicialização, validação, atualizações de metadados). O processamento de muitos lotes pequenos é significativamente menos eficiente do que o processamento de menos lotes maiores.
* **Maior superfície de falha**: mais trabalhos significam mais oportunidades para falha. Cada lote que falhar requer investigação e potencial reprocessamento.
* **Carga desnecessária do sistema**: lotes pequenos frequentes mantêm o sistema constantemente ocupado com tarefas de sobrecarga em vez do processamento de dados real, reduzindo a taxa de transferência geral.
* **Disponibilidade de dados atrasada**: paradoxalmente, a execução de muitos lotes pequenos pode atrasar quando os dados se tornam disponíveis para processos downstream em comparação aos lotes consolidados.
* **Inspeção difícil**: rastrear o sucesso e o desempenho de dezenas de trabalhos em lotes individuais por conjunto de dados torna-se operacionalmente complexo e demorado.
* **Atraso no processamento do perfil**: cada lote de assimilação de perfil aciona o processamento do perfil. Lotes pequenos frequentes podem fazer com que o processamento de perfil seja executado quase continuamente, impedindo uma otimização de lote eficiente.

**Como corrigir**:

* **Reduzir a frequência de lotes**: consolide para menos lotes por dia por conjunto de dados para a maioria dos casos de uso.
* **Aumentar tamanho do lote**: acumule mais dados antes de acionar a assimilação, em vez de assimilar imediatamente.
* **Alinhar-se às necessidades comerciais**: verifique se as atualizações por hora são realmente necessárias ou se são suficientes atualizações diárias/duas vezes por dia.
* **Usar streaming em tempo real**: alterne para a assimilação de streaming para requisitos genuínos em tempo real, em vez de simulá-la com lotes frequentes.

## Próximas etapas {#next-steps}

Depois de identificar os antipadrões em suas programações de job:

* Visualize [detalhes do trabalho](job-schedules-details.md) para investigar conjuntos de dados específicos e execuções de trabalho que podem estar causando problemas.
* Revise a [visão geral das Agendas de Trabalho](job-schedules.md) para entender a interface e os recursos de inspeção.
* Saiba mais sobre a [assimilação em lote](../ingestion/batch-ingestion/overview.md) para otimizar os agendamentos de carregamento de dados.
* Entenda os [agendamentos de segmentação](../segmentation/home.md) para garantir o tempo adequado das avaliações de público-alvo.
* Explore o [monitoramento dos fluxos de dados de destino](../dataflows/ui/monitor-destinations.md) para uma visibilidade completa do pipeline.
