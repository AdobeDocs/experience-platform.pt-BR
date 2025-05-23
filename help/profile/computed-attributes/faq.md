---
title: Perguntas frequentes sobre atributos computados
description: Descubra respostas para perguntas frequentes sobre o uso de atributos computados.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: 7d515401eb49ffd2ad5cf0bd074896b274c4fb05
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Perguntas frequentes

No Adobe Experience Platform, os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Veja a seguir uma lista das perguntas frequentes sobre atributos computados.

## Como faço para obter acesso a atributos computados?

Para obter acesso a atributos computados, você precisará ter as permissões apropriadas (**Exibir atributos computados** e **Gerenciar atributos computados**). Para obter mais informações sobre as permissões necessárias, leia a [documentação sobre controle de acesso](../../access-control/home.md). Para saber como aplicar essas permissões, leia o [guia de gerenciamento de permissões](../../access-control/ui/permissions.md).

## Quais conjuntos de dados contribuem para os cálculos de atributos calculados?

Os atributos computados consideram conjuntos de dados de Evento de experiência habilitados para Perfil do cliente em tempo real para calcular atributos computados.

## Quais campos do Experience Data Model (XDM) podem ser usados para criar atributos calculados?

Todos os campos XDM no esquema de união do Evento de experiência podem ser usados para criar atributos calculados.

## O que &quot;última avaliação&quot; e &quot;último status de avaliação&quot; representam?

Última avaliação refere-se ao carimbo de data e hora até o qual os eventos são considerados na última execução bem-sucedida. O status da última avaliação refere-se a se a última execução de avaliação foi ou não bem-sucedida.

## Posso escolher a frequência de atualização? Como isso é decidido?

A frequência de atualização é determinada automaticamente com base no período de pesquisa do seu atributo calculado. Para obter mais informações sobre isso, leia a [seção do período de lookback](./overview.md#lookback-periods) da visão geral dos atributos computados.

## Como os cálculos são afetados pelas expirações de dados do Evento de experiência?

Os cálculos de atributos calculados são preenchidos retroativamente para a duração de pesquisa definida na primeira avaliação e atualizados com base em eventos incrementais para atualizações subsequentes. Como resultado, esses cálculos são **não** afetados pelas expirações dos dados antigos do Evento de experiência após a primeira avaliação.

Por exemplo, se você criar um atributo calculado que é avaliado mensalmente com um período de lookback de três meses, para a primeira avaliação, o atributo calculado será calculado para todos os eventos dentro desse período de lookback de três meses. Mesmo que o conjunto de dados do Evento de experiência tenha uma expiração de dados de um mês, essa expiração de dados **não** afetará a atualização mensal do atributo computado, já que a execução de avaliação do próximo mês agregará eventos incrementalmente e atualizará a computação.

>[!NOTE]
>
>Dados expirados **não podem** ser preenchidos retroativamente mais tarde por um atributo computado. A expiração dos dados do conjunto de dados do evento **maio** limitou a capacidade de validar o valor do atributo computado em um momento posterior. Para validar o valor de atributo calculado, o período de pesquisa deve permanecer **dentro** dos limites das expirações de dados.

## Posso criar um atributo calculado com base em outro atributo calculado?

Como os atributos calculados são criados usando campos de Evento de experiência e residem em um campo de Perfil, não há como usar diretamente um atributo calculado para criar outro atributo calculado.

## Existem limites para o número de atributos computados que eu posso criar?

Sim, há um limite para o número de atributos computados que você pode criar. Esse limite se aplica somente a atributos computados **ativos**. Consulte a descrição do produto ou entre em contato com a equipe da conta da Adobe para obter mais informações.

## Há alguma implicação downstream na desativação de um atributo calculado?

Antes de desabilitar o atributo computado, você **deve** removê-los dos sistemas downstream (como segmentação, jornadas ou destinos), pois pode haver complicações que surgirão se não forem removidos.

## O que acontece quando eu desabilitar um atributo calculado? {#inactive-status}

Quando um atributo calculado é desativado ou tornado inativo, ele não é mais atualizado. Como resultado, este atributo computado **não pode** ser usado na pesquisa de perfil ou em outros usos downstream.

## Como os atributos computados ajudam a impulsionar o engajamento?

Os atributos computados impulsionam o enriquecimento do perfil ao agregar os atributos do evento em um nível de perfil mesclado. Por exemplo, você pode personalizar emails de marketing com o produto visualizado mais recentemente.

## Com que frequência os atributos calculados são avaliados? Isso está relacionado ao cronograma de avaliação do público-alvo?

Os atributos computados são avaliados em uma frequência de **lote** que é **independente** para o cronograma de sua avaliação de público, destino e jornada. Isso significa que, independentemente do tipo de segmentação (segmentação em lote ou segmentação por transmissão), o atributo calculado será avaliado em seu próprio agendamento (por hora, dia, semana ou mês).

A primeira avaliação do atributo computado ocorre dentro das 24 horas após a **criação**. As avaliações subsequentes em lote ocorrem de hora em hora, dia, semana ou mês, dependendo do período de pesquisa definido.

Por exemplo, se uma primeira avaliação ocorrer às 12h00 UTC de 9 de outubro, as avaliações subsequentes ocorrerão nos seguintes horários:

- Próxima atualização diária: 12:00 UTC de 10 de outubro
- Próxima atualização semanal: 12:00 UTC de 15 de outubro
- Próxima atualização mensal: 12h UTC de 1º de novembro

>[!IMPORTANT]
>
>Este somente é o caso se a atualização rápida estiver **não** habilitada. Para saber como o período de pesquisa muda quando a atualização rápida está habilitada, leia a [seção de atualização rápida](./overview.md#fast-refresh).

As atualizações **semanais** e **mensais** ocorrem no início da **semana do calendário** (o domingo da nova semana) ou no início do **mês do calendário** (o primeiro do novo mês), em vez de exatamente uma semana ou um mês após a primeira data de avaliação.

>[!NOTE]
>
>O valor do atributo calculado é **não** atualizado imediatamente no perfil após cada execução de avaliação. Para garantir que o valor atualizado esteja em seus perfis, você deve considerar um buffer de algumas horas entre o tempo de avaliação e o uso do atributo calculado. O agendamento de atualização de atributo computado é **determinado pelo sistema** e **não pode** ser modificado. Para obter mais informações, entre em contato com o Atendimento ao cliente da Adobe.

## Como os atributos computados interagem com os públicos avaliados usando a segmentação por transmissão?

Se um público avaliado por transmissão de segmentação estiver usando um atributo computado, ele pegará o **último valor** do atributo computado enquanto o público estiver sendo avaliado. Por exemplo, se o público-alvo estiver procurando eventos de compra, o público-alvo se referirá ao último valor de atributo calculado avaliado quando o evento de compra chegar.

## Posso usar atributos computados no Edge?

Como qualquer outro atributo de perfil, os atributos calculados estão disponíveis e podem ser usados em bordas. Observe que os atributos computados são **não** computados na borda.

## Como os rótulos de uso de dados são aplicados em atributos calculados?

Os atributos calculados derivam automaticamente rótulos de uso de dados dos campos e conjuntos de dados de origem que foram usados para definir os atributos calculados. Isso garante que seus dados comportamentais sejam usados corretamente.

## Como usar atributos computados com o Adobe Journey Optimizer?

Para usar atributos computados no jornada, você precisará adicionar o grupo de campos `SystemComputedAttributes` à fonte de dados Experience Platform. Para obter mais informações sobre como configurar a fonte de dados do Experience Platform, leia o [guia da fonte de dados do Adobe Experience Platform](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html?lang=pt-BR).
