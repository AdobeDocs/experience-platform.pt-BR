---
title: Visão geral dos atributos computados
description: Os atributos computados são funções para agregar dados de nível de evento em atributos de nível de perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.
badge: "Beta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Visão geral de atributos computados

>[!IMPORTANT]
>
>Atributos computados estão atualmente em **beta** e está **não** disponível para todos os usuários.

A personalização baseada no comportamento do usuário é um requisito essencial para que os profissionais de marketing maximizem o impacto da personalização. Por exemplo, personalizar o email de marketing com o produto visualizado mais recentemente para impulsionar a conversão ou personalizar a página da Web com base no total de compras feitas pelos usuários para impulsionar a retenção.

Os atributos computados ajudam a converter rapidamente os dados comportamentais do perfil em valores agregados no nível do perfil, sem depender dos recursos de engenharia para:

- Ativação da personalização direcionada com ativação de agregações comportamentais para destinos do Real-time Customer Data Platform, uso no Adobe Journey Optimizer ou na segmentação
- Padronização de dados comportamentais agregados de perfis para uso em plataformas e aplicativos
- Melhor gerenciamento de dados com a consolidação de dados antigos de eventos de perfil em insights comportamentais significativos

Essas agregações são calculadas com base nos conjuntos de dados de Evento de experiência habilitados para perfil assimilados na Adobe Experience Platform. Cada atributo calculado é um atributo de perfil criado no esquema de união de perfil e é agrupado no grupo de campos &quot;Atributo calculado&quot; no esquema de união.

Casos de uso de amostra incluem a personalização de anúncios com o nome do último produto visualizado para pessoas sem compras nos últimos 7 dias, a personalização de emails de marketing com o total de pontos de recompensa ganhos para parabenizar os usuários por serem promovidos para um nível premium ou o cálculo do valor vitalício de cada cliente para impulsionar um melhor direcionamento.

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
| MAIS_RECENTE | Uma função localiza o valor do atributo especificado a partir do evento qualificado mais recente. | Todos os valores primitivos, Matrizes de valores primitivos | Produto mais recente exibido nos últimos 7 dias |

### Períodos de pesquisa

Os atributos calculados são calculados em lotes, permitindo que você mantenha suas agregações atualizadas e use os eventos mais recentes. Para oferecer suporte a esses cenários quase em tempo real, a frequência de atualização varia dependendo do período de retrospectiva do evento.

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
>As semanas e os meses são considerados **semanas do calendário** e **meses do calendário** quando usado em retrospectivas de evento.

**Atualização rápida**

>[!IMPORTANT]
>
>Um máximo de **cinco** os atributos, por sandbox, podem ter a atualização rápida ativada.

A atualização rápida permite manter seus atributos atualizados. Ativar essa opção permite atualizar os atributos calculados diariamente, mesmo para períodos de pesquisa mais longos. Isso permite que você reaja em tempo quase real às atividades do usuário. Esse valor só é aplicável para atributos calculados com um período de lookback maior que uma base semanal.

>[!NOTE]
>
>Ativar a atualização rápida variará a duração da pesquisa de evento, já que o período de pesquisa é acumulado semanal ou mensalmente, respectivamente.
>
>Por exemplo, se você criar um atributo calculado com um período de lookback de duas semanas com a atualização rápida ativada, isso significa que o período de lookback inicial será de duas semanas. No entanto, a cada atualização diária, o período de lookback incluirá eventos do dia adicional. Essa adição de dias continuará até que a próxima semana do calendário comece, na qual a janela de retrospectiva será transferida e retornará para duas semanas.

## Próximas etapas

Para saber mais sobre como criar e gerenciar atributos computados, leia o [guia da API de atributos computados](./api.md) ou o [guia da interface de atributos computados](./ui.md).
