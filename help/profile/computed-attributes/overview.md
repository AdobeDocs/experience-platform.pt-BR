---
title: Visão geral dos atributos computados
description: Os atributos computados são funções para agregar dados de nível de evento em atributos de nível de perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 03f1dfab768e98ef4959d605cc3ead25bb5eb238
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 4%

---

# Visão geral de atributos computados

A personalização baseada no comportamento do usuário é um requisito essencial para que os profissionais de marketing maximizem o impacto da personalização. Por exemplo, personalizar o email de marketing com o produto visualizado mais recentemente para impulsionar a conversão ou personalizar a página da Web com base no total de compras feitas pelos usuários para impulsionar a retenção.

Os atributos computados ajudam a converter rapidamente os dados comportamentais do perfil em valores agregados no nível do perfil, sem depender dos recursos de engenharia para:

- Habilitação de personalização direcionada de um para um ou em lote com ativação de agregações comportamentais para destinos e uso do Real-time Customer Data Platform no Adobe Journey Optimizer
- Segmentação simplificada do público-alvo com armazenamento de agregações comportamentais como atributos de perfil
- Padronização de dados comportamentais agregados de perfis para uso em plataformas e aplicativos
- Melhor gerenciamento de dados com a consolidação de dados antigos de eventos de perfil em insights comportamentais significativos

Essas agregações são calculadas com base nos conjuntos de dados de Evento de experiência habilitados para perfil assimilados na Adobe Experience Platform. Cada atributo calculado é um atributo de perfil criado no esquema de união de perfil e é agrupado no grupo de campos &quot;SystemComputedAttribute&quot; no esquema de união.

Exemplos de casos de uso incluem:

- Personalizar emails de marketing com pontos de recompensa totais para parabenizar os usuários por serem promovidos para um nível premium
- Personalização de comunicações para usuários com base em contagens e frequência de compra
- Personalizar emails de retenção com base nas datas de expiração da assinatura
- Redirecionamento de usuários que visualizaram, mas não compraram um produto com o último produto visualizado
- Ativar agregações de eventos por meio de atributos computados para um sistema downstream usando destinos do Real-Time CDP
- Recolher vários públicos com base em eventos em um grupo mais condensado de atributos computados
- Redirecionamento de usuários não autenticados para fora do site usando IDs de parceiros recentes de eventos

Este guia ajudará você a entender melhor a função dos atributos computados na Platform, além de explicar as noções básicas sobre atributos computados.

## Noções básicas sobre atributos computados

O Adobe Experience Platform permite importar e mesclar dados facilmente de várias fontes para gerar [!DNL Real-Time Customer Profiles]. Cada perfil contém informações importantes relacionadas a um indivíduo, como suas informações de contato, preferências e histórico de compras, fornecendo uma visualização de 360 graus do cliente.

Algumas das informações coletadas no perfil são facilmente compreendidas ao ler os campos de dados diretamente (por exemplo, &quot;nome&quot;), enquanto outros dados exigem a execução de vários cálculos ou a confiança em outros campos e valores para gerar as informações (por exemplo, &quot;total de compras vitalícias&quot;). Para facilitar a compreensão rápida desses dados, [!DNL Platform] O permite criar atributos calculados que executam automaticamente essas referências e cálculos, retornando o valor no campo apropriado.

Os atributos computados incluem a criação de uma expressão, ou &quot;regra&quot;, que opera nos dados recebidos e armazena o valor resultante em um atributo de perfil. As expressões podem ser definidas de várias maneiras diferentes, permitindo especificar em quais eventos agregar, funções agregadas ou as durações de pesquisa.

### Funções

Os atributos computados permitem definir agregações de eventos de maneira automatizada aproveitando funções predefinidas. Os detalhes sobre essas funções podem ser encontrados abaixo:

| Função | Descrição | Tipos de dados compatíveis | Exemplo de uso |
| -------- | ----------- | -------------------- | ------------- |
| SOMA | Uma função que **somas** configure o valor especificado para eventos qualificados. | Inteiros, Números, Longos | Soma de todas as compras nos últimos 7 dias |
| CONTAGEM | Uma função que **contagens** o número de eventos que ocorreram para a regra especificada. | N/D | Contagem de compras nos últimos 3 meses |
| MÍN | Uma função que encontra a variável **mínimo** para os eventos qualificados. | Números inteiros, números, duração, carimbos de data e hora | Dados da primeira compra nos últimos 7 dias<br/>Valor mínimo do pedido nas últimas 4 semanas |
| MAX | Uma função que encontra a variável **máximo** para os eventos qualificados. | Números inteiros, números, duração, carimbos de data e hora | Dados da última compra nos últimos 7 dias<br/>Valor máximo do pedido nas últimas 4 semanas |
| MAIS_RECENTE | Uma função que encontra o valor do atributo especificado do evento qualificado mais recente. Esta função dá **ambos** o valor e a data e hora do atributo. | Todos os valores primitivos, Matrizes de valores primitivos | Produto mais recente exibido nos últimos 7 dias |

### Períodos de pesquisa

Os atributos calculados são calculados em lotes, permitindo que você mantenha suas agregações atualizadas e use os eventos mais recentes. Para oferecer suporte a esses cenários com atraso mínimo, a frequência de atualização varia dependendo do período de retrospectiva do evento.

O período de lookback se refere à quantidade de tempo revisada ao agregar Eventos de experiência para o atributo calculado. Esse período pode ser definido em horas, dias, semanas ou meses.

A frequência de atualização refere-se à frequência com que os atributos calculados são atualizados. Esse valor depende do período de lookback e é automaticamente definido.

| Período de pesquisa | Frequência de atualização |
| --------------- | ----------------- |
| Até 24 horas | Por hora |
| Até 7 dias | Diariamente |
| Até 4 semanas | Semanalmente |
| Até 6 meses | Mensalmente |

Por exemplo, se o atributo calculado tiver um período de lookback dos últimos 7 dias, esse valor será calculado com base nos valores dos últimos 7 dias e atualizado diariamente.

>[!NOTE]
>
>As semanas e os meses são considerados **semanas do calendário** e **meses do calendário** quando usado em retrospectivas de evento. A semana do calendário começa na **domingo** e termina no **Sábado** da semana. O mês do calendário começa no dia **primeiro** do mês e termina no dia **último dia** do mês.

O período de pesquisa para atributos calculados é um **rolagem** período de pesquisa. Por exemplo, se uma primeira avaliação ocorrer em 15 de outubro às 12h00 UTC, o período de lookback de duas semanas recuperará todos os eventos de 1º de outubro a 15 de outubro, atualizará no horário de uma semana em 22 de outubro e recuperará todos os eventos de 8 a 22 de outubro.

**Atualização rápida** {#fast-refresh}

A atualização rápida permite manter seus atributos atualizados. Habilitar essa opção possibilita atualizar os atributos calculados diariamente, mesmo para períodos de retrospectiva mais longos, permitindo reagir rapidamente às atividades do usuário ou usuária.

>[!NOTE]
>
>Ativar a atualização rápida variará a duração da pesquisa de evento, já que o período de pesquisa é acumulado semanal ou mensalmente, respectivamente.
>
>Se você criar um atributo calculado com um período de lookback de duas semanas com a atualização rápida ativada, isso significa que o período de lookback inicial será de duas semanas. No entanto, a cada atualização diária, o período de lookback incluirá eventos do dia adicional. Essa adição de dias continuará até que a próxima semana do calendário comece, na qual a janela de retrospectiva será transferida e retornará para duas semanas.
>
>Por exemplo, se houver um período de lookback de duas semanas começando em 15 de março (domingo) com a atualização rápida ativada, com a atualização diária, o período de lookback continuará expandindo de forma inclusiva até 22 de março, onde será redefinido para duas semanas. Em resumo, o atributo calculado é **atualizado** diariamente, com o período de pesquisa aumentando de **dois** semanas para **três** semanas durante a semana e, em seguida, voltar para **dois** semanas.

## Próximas etapas

Para saber mais sobre como criar e gerenciar atributos computados, leia o [guia da API de atributos computados](./api.md) ou o [guia da interface de atributos computados](./ui.md).
