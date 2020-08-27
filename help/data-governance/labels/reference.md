---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;supported data usage labels;contract labels;identity labels;sensitive labels
solution: Experience Platform
title: Rótulos principais de uso de dados
topic: labels
description: Este documento descreve todas as etiquetas de uso de dados atualmente suportadas pela Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 2%

---


# Rótulos principais de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. O Adobe Experience Platform Data Governance fornece vários rótulos principais de uso de dados prontos para uso que você pode usar para classificar seus dados por start.

Este documento descreve as principais etiquetas de uso de dados fornecidas atualmente por [!DNL Experience Platform]. Para obter mais informações sobre [!DNL Data Governance] o, consulte a visão geral [do](../home.md)Data Governance.

## Rótulos do contrato

As etiquetas &quot;C&quot; do contrato são usadas para categorizar dados que têm obrigações contratuais ou estão relacionados às políticas de controle de dados de sua organização.

| Rótulo | Definição |
|---|---|
| **C1** | Os dados só podem ser exportados da Adobe Experience Cloud em um formulário agregado sem incluir identificadores individuais ou de dispositivos. [Mais informações...](#c1) |
| **C2** | Os dados não podem ser exportados para terceiros. [Mais informações...](#c2) |
| **C3** | Os dados não podem ser combinados ou usados com informações diretamente identificáveis. [Mais informações...](#c3) |
| **C4** | Os dados não podem ser usados para direcionar qualquer anúncio ou conteúdo, seja no site ou entre sites. [Mais informações...](#c4) |
| **C5** | Os dados não podem ser usados para direcionamento de conteúdo ou anúncios entre sites com base em interesses. [Mais informações...](#c5) |
| **C6** | Os dados não podem ser usados para direcionamento de anúncios no site. [Mais informações...](#c6) |
| **C7** | Os dados não podem ser usados para direcionamento de conteúdo no site. [Mais informações...](#c7) |
| **C8** | Os dados não podem ser usados para medir os sites ou aplicativos de sua organização. [Mais informações...](#c8) |
| **C9** | Os dados não podem ser usados em workflows da Data Science. [Mais informações...](#c9) |
| **C10** | Os dados não podem ser usados para a ativação de identidade costurada. [Mais informações...](#c10) |

## Rótulos de identidade

Os rótulos &quot;I&quot; de identidade são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica.

| Rótulo | Definição |
|---|---|
| **I1** | Dados diretamente identificáveis que podem identificar ou entrar em contato com uma pessoa específica, em vez de um dispositivo. |
| **I2** | Dados indiretamente identificáveis que podem ser usados em combinação com quaisquer outros dados para identificar ou entrar em contato com uma pessoa específica. |

## Etiquetas sensíveis

As etiquetas &quot;S&quot; sensíveis são usadas para categorizar dados que você e sua organização consideram confidenciais.

Um tipo de dados que você pode considerar sensíveis pode ser de diferentes tipos de dados geográficos; no entanto, esta categoria não se limita aos dados geográficos.

| Rótulo | Definição |
|---|---|
| **S1** | Dados que especificam a latitude e a longitude que podem ser usados para determinar a localização precisa de um dispositivo. |
| **S2** | Dados que podem ser usados para determinar uma área de geofence amplamente definida. |

## Apêndice

As seções abaixo fornecem informações adicionais sobre rótulos de uso de dados disponíveis.

### Detalhes do rótulo do contrato

As seções que se seguem apresentam informações pormenorizadas relativas à aplicação de rótulos &quot;C&quot; específicos do contrato.

#### C1 {#c1}

Alguns dados só podem ser exportados da Adobe Experience Cloud em um formulário agregado sem incluir identificadores individuais ou de dispositivos. Por exemplo, dados que se originaram de redes sociais.

#### C2 {#c2}

Alguns fornecedores de dados têm termos nos seus contratos que proíbem a exportação de dados de onde foram originalmente recolhidos. Por exemplo, os contratos de rede social muitas vezes restringem a transferência de dados que você recebe deles. O rótulo C2 é mais restritivo do que [C1](#c1), o que requer apenas agregação e dados anônimos.

#### C3 {#c3}

Alguns fornecedores de dados têm termos nos seus contratos que proíbem a combinação ou utilização desses dados com informações diretamente identificáveis. Por exemplo, os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis.

#### C4 {#c4}

O C4 é o rótulo mais restritivo - inclui os rótulos [C5](#c5), [C6](#c6)e [C7](#c7).

#### C5 {#c5}

A definição de metas ou personalização baseada em interesses ocorre se as três condições a seguir forem atendidas: Os dados coletados no site são (1) usados para fazer inferências sobre os interesses dos usuários, (2) são usados em outro contexto, como em outro site ou aplicativo (fora do site) E (3) são usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas inferências.

A combinação de dados de vários sites, incluindo uma combinação de dados no local e dados fora do local ou uma combinação de dados de várias fontes fora do local, é chamada de dados entre sites. Sites diferentes representam contextos diferentes, de modo que o uso de dados entre sites em qualquer contexto é diferente do original. Os dados entre sites são normalmente coletados e processados para fazer inferências sobre os interesses dos usuários. Como resultado, o uso de dados entre sites para direcionar anúncios ou conteúdo normalmente se qualifica como direcionamento baseado em interesses, independentemente de o anúncio ou conteúdo aparecer no site ou fora dele. Por exemplo, se os dados no site fossem usados em combinação com dados fora do site para selecionar qual anúncio mostrar a um usuário no site de uma organização, esse uso seria qualificado como direcionamento baseado em juros. Como outro exemplo, o redirecionamento de anúncios para usuários fora do site também se qualificaria como direcionamento com base em juros.

O uso de dados fora do site sozinho para definição de metas provavelmente também se qualificaria como definição de metas com base em juros, já que os dados fora do site normalmente são coletados e processados para fazer inferências sobre os interesses dos usuários.

No entanto, a definição de metas para conteúdo ou anúncios que usam apenas dados no site normalmente não se qualificaria como direcionamento baseado em interesses. A definição de metas no site que, de outra forma, não se qualifica como definição de metas baseada em interesses é tratada como dois rótulos distintos. Especificamente, o Rótulo C6 endereça a definição de metas e o relatórios do anúncio no site e fala especificamente sobre seleção de anúncios, delivery e relatórios, e o Rótulo C7 endereça a seleção de conteúdo no site, delivery e relatórios (definição de metas de conteúdo no site).

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado depende de você. Para referência, os quadros IAB e DAA são fornecidos a seguir:

IAB: Personalização. A coleta e o processamento de informações sobre o uso deste serviço para personalizar subsequentemente a publicidade e/ou o conteúdo para você em outros contextos, como em outros sites ou aplicativos, ao longo do tempo. Normalmente, o conteúdo do site ou aplicativo é usado para fazer inferências sobre seus interesses que informam a seleção futura de publicidade e/ou conteúdo.

DAA: Anúncio comportamental online. Coleta de dados de um computador ou dispositivo específico com relação a comportamentos de visualização na Web ao longo do tempo e em sites não afiliados com o objetivo de usar esses dados para prever preferências de usuário ou interesses em fornecer publicidade a esse computador ou dispositivo com base em preferências ou interesses inferidos desses comportamentos de visualização na Web.

#### C6 {#c6}

Anúncios são mensagens ou notificações, incluindo texto e imagens, que aparecem em um site ou aplicativo que se destinam principalmente a promover a venda de bens ou serviços. Cabe a você determinar a finalidade dessas mensagens ou notificações. Os anúncios são separados do conteúdo no site, coberto pela etiqueta [C7](#c7). Os dados com uma etiqueta C6 não podem ser usados para direcionamento de anúncios no site, incluindo a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização, nem para medir o delivery e a eficácia desses anúncios. Isso inclui o uso de dados no site coletados anteriormente sobre os interesses dos usuários para selecionar anúncios, processar dados sobre o que os anúncios foram exibidos, quando e onde eles foram mostrados e se os usuários tomaram alguma ação relacionada ao anúncio, como clicar em um anúncio ou fazer uma compra. Geralmente, fazer inferências sobre as preferências de um usuário com base nas atividades no site desse usuário e, em seguida, usar essas preferências no direcionamento de anúncio no site não se qualificaria como direcionamento com base em juros (também chamado de personalização), pois não atenderia aos três requisitos necessários para o direcionamento com base em juros. _[Consulte a etiqueta C5 para ver estes requisitos.](#c5)_

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado depende de você. Para referência, os quadros IAB e DAA são fornecidos a seguir:

IAB: 3. Seleção de anúncio, delivery, relatórios: A coleta de informações e a combinação com informações coletadas anteriormente, para selecionar e fornecer anúncios para você e para medir o delivery e a eficácia de tais anúncios. Isso inclui o uso de informações coletadas anteriormente sobre seus interesses para selecionar anúncios, processar dados sobre o que os anúncios foram exibidos, com que frequência eles foram exibidos, quando e onde eles foram exibidos e se você tomou alguma ação relacionada ao anúncio, incluindo, por exemplo, clicar em um anúncio ou fazer uma compra. Isso não inclui a Personalização, que é a coleta e o processamento de informações sobre seu uso desse serviço para personalizar subsequentemente a publicidade e/ou o conteúdo para você em outros contextos, como sites ou aplicativos, ao longo do tempo.

DAA: O Anúncio comportamental online não inclui as atividades das primeiras partes, o Delivery do anúncio ou o Relatórios do anúncio, ou publicidade contextual (isto é, publicidade baseada no conteúdo da página da Web que está sendo visitada, visita atual do consumidor a uma página da Web ou query de pesquisa).

#### C7 {#c7}

O conteúdo no site é um texto e imagens que foram criados para informar, educar ou entreter e que não foram criados para promover a venda de bens ou serviços. Cabe a você determinar a finalidade do conteúdo, incluindo se ele se qualificaria como publicidade nativa. A etiqueta C7 não se destina a cobrir anúncios no local, que são cobertos pela etiqueta [C6](#c6). Os dados com um rótulo C7 não podem ser usados para direcionamento de conteúdo no site, incluindo a seleção e o delivery de conteúdo nos sites ou aplicativos de sua organização, ou para medir o delivery e a eficácia desse conteúdo. Isso inclui informações coletadas anteriormente sobre os interesses dos usuários em conteúdo selecionado, o processamento de dados sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo ele foi exibido, quando e onde ele foi exibido e se os usuários tomaram quaisquer ações relacionadas ao conteúdo, incluindo, por exemplo, clicar no conteúdo. Geralmente, fazer inferências sobre as preferências de um usuário com base nas atividades no site desse usuário e, em seguida, usar essas preferências na definição de metas de conteúdo no site não se qualificaria como definição de metas baseada em juros (também chamada de personalização), pois não atenderia aos três requisitos necessários para a definição de metas com base em juros. _[Consulte a etiqueta C5 para ver estes requisitos.](#c5)_

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado depende de você. Para referência, os quadros IAB e DAA são fornecidos a seguir:

IAB: 4. Seleção de conteúdo, delivery, relatórios: A coleta de informações e a combinação com informações coletadas anteriormente, para selecionar e fornecer conteúdo para você e para medir o delivery e a eficácia de tal conteúdo. Isso inclui o uso de informações coletadas anteriormente sobre seus interesses para selecionar conteúdo, processar dados sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo ele foi exibido, quando e onde ele foi exibido e se você executou alguma ação relacionada ao conteúdo, incluindo, por exemplo, clicar no conteúdo. Isso não inclui a Personalização, que é a coleta e o processamento de informações sobre seu uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade para você em outros contextos, como sites ou aplicativos, ao longo do tempo.

DAA: O Anúncio comportamental online não inclui as atividades das primeiras partes, o Delivery do anúncio ou o Relatórios do anúncio, ou publicidade contextual (isto é, publicidade baseada no conteúdo da página da Web que está sendo visitada, visita atual do consumidor a uma página da Web ou query de pesquisa).

#### C8 {#c8}

Os dados não podem ser usados para medir, entender e relatar sobre o uso pelos usuários dos sites ou aplicativos de sua organização. Isso não inclui a definição de metas com base em interesses (definição de metas entre sites), que é a coleção de informações sobre a utilização deste serviço para personalizar subsequentemente o conteúdo e/ou a publicidade para você em outros contextos, ou seja, em outros serviços, como sites ou aplicativos, ao longo do tempo.

#### C9 {#c9}

Alguns contratos incluem proibições explícitas sobre a utilização de dados para a ciência de dados. Às vezes, são redigidos em termos que proíbem o uso de dados para Inteligência Artificial (AI), aprendizado de máquina (ML) ou modelagem.

#### C10 {#c10}

Algumas políticas de uso de dados restringem o uso de dados de identidade agrupados para personalização. O rótulo C10 é aplicado automaticamente aos segmentos se suas políticas de mesclagem usarem a opção &quot;gráfico privado&quot;.
