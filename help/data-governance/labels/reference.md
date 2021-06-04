---
keywords: Experience Platform, home, tópicos populares, governança de dados, api de etiqueta de uso de dados, api de serviço de política, rótulos de uso de dados suportados, rótulos de contrato, rótulos de identidade, rótulos sensíveis
solution: Experience Platform
title: Glossário de rótulos de uso de dados
topic-legacy: labels
description: Este documento descreve todos os rótulos de uso de dados suportados atualmente pelo Adobe Experience Platform.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: 1ae0ce47381585b48020990a71493bbfc1504ec2
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 2%

---

# Glossário de rótulos de uso de dados

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. A Governança de dados do Adobe Experience Platform fornece vários rótulos de uso de dados principais prontos para uso que você pode usar para começar a categorizar seus dados.

Este documento descreve os rótulos de uso de dados principais fornecidos atualmente por [!DNL Experience Platform]. Mais informações sobre [!DNL Data Governance] podem ser encontradas na [Visão geral da governança de dados](../home.md).

## Rótulos do contrato

Os rótulos &quot;C&quot; do contrato são usados para categorizar dados que têm obrigações contratuais ou estão relacionados às políticas de governança de dados da sua organização.

| Rótulo | Definição |
| --- | --- |
| **C1** | Os dados só podem ser exportados do Adobe Experience Cloud de forma agregada sem incluir identificadores individuais ou de dispositivos. [Mais informações...](#c1) |
| **C2** | Os dados não podem ser exportados para um terceiro. [Mais informações...](#c2) |
| **C3** | Os dados não podem ser combinados ou usados com informações diretamente identificáveis. [Mais informações...](#c3) |
| **C4** | Os dados não podem ser usados para direcionar qualquer anúncio ou conteúdo, seja no site ou entre sites. [Mais informações...](#c4) |
| **C5** | Os dados não podem ser usados para direcionamento de conteúdo ou anúncios com base em interesses entre sites. [Mais informações...](#c5) |
| **C6** | Os dados não podem ser usados para o direcionamento de anúncios no site. [Mais informações...](#c6) |
| **C7** | Os dados não podem ser usados para o direcionamento no site do conteúdo. [Mais informações...](#c7) |
| **C8** | Os dados não podem ser usados para medir os sites ou aplicativos de sua organização. [Mais informações...](#c8) |
| **C9** | Os dados não podem ser usados em workflows da ciência de dados. [Mais informações...](#c9) |
| **C10** | Os dados não podem ser usados para a ativação de identidade compilada. [Mais informações...](#c10) |
| **C11** | Os dados não podem ser compartilhados com parceiros de Correspondência de segmentos. [Mais informações...](#c11) |

## Rótulos de identidade

Os rótulos de identidade &quot;I&quot; são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica.

| Rótulo | Definição |
| --- | --- |
| **I1** | Dados diretamente identificáveis que podem identificar ou entrar em contato com uma pessoa específica, em vez de um dispositivo. |
| **I2** | Dados indiretamente identificáveis que podem ser usados em combinação com quaisquer outros dados para identificar ou contactar uma pessoa específica. |

## Rótulos sensíveis

Os rótulos &quot;S&quot; confidenciais são usados para categorizar dados que você e sua organização consideram confidenciais.

Um tipo de dados que você pode considerar sensíveis pode ser diferentes tipos de dados geográficos; no entanto, esta categoria não se limita aos dados geográficos.

| Rótulo | Definição |
| --- | --- |
| **S1** | Dados que especificam latitude e longitude que podem ser usados para determinar a localização precisa de um dispositivo. |
| **S2** | Dados que podem ser usados para determinar uma área de geofence amplamente definida. |

## Apêndice

As seções abaixo fornecem informações adicionais sobre rótulos disponíveis de uso de dados.

### Detalhes do rótulo do contrato

As seções que se seguem fornecem informações detalhadas sobre a aplicação de rótulos &quot;C&quot; específicos do contrato.

#### C1 {#c1}

Alguns dados só podem ser exportados do Adobe Experience Cloud em um formulário agregado sem incluir identificadores individuais ou de dispositivos. Por exemplo, dados que se originaram de redes sociais.

#### C2 {#c2}

Alguns provedores de dados têm termos em seus contratos que proíbem a exportação de dados de onde eles foram originalmente coletados. Por exemplo, os contratos de rede social geralmente restringem a transferência de dados que você recebe deles. O rótulo C2 é mais restritivo do que [C1](#c1), o que requer apenas agregação e dados anônimos.

#### C3 {#c3}

Alguns provedores de dados têm termos em seus contratos que proíbem a combinação ou o uso desses dados com informações diretamente identificáveis. Por exemplo, os contratos para dados obtidos de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis.

#### C4 {#c4}

O C4 é o rótulo mais restritivo: abrange os rótulos [C5](#c5), [C6](#c6) e [C7](#c7).

#### C5 {#c5}

O direcionamento baseado em interesses ou a personalização ocorre se as três condições a seguir forem atendidas: Os dados coletados no site são (1) usados para fazer inferências sobre os interesses de um usuário, (2) são usados em outro contexto, como em outro site ou aplicativo (fora do site) e (3) são usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas inferências.

A combinação de dados de vários sites, incluindo uma combinação de dados no local e dados fora do site ou uma combinação de dados de várias fontes fora do site, é chamada de dados entre sites. Sites diferentes representam contextos diferentes, de modo que o uso de dados entre sites em qualquer contexto é diferente do original. Os dados entre sites geralmente são coletados e processados para fazer inferências sobre os interesses dos usuários. Como resultado, o uso de dados entre sites para o direcionamento de anúncios ou conteúdo normalmente se qualifica como direcionamento baseado em interesses, independentemente do anúncio ou conteúdo aparecer no site ou fora dele. Por exemplo, se os dados no site fossem usados em combinação com dados externos para selecionar qual anúncio mostrar um usuário no próprio site de uma organização, esse uso seria qualificado como direcionamento baseado em interesses. Como outro exemplo, o redirecionamento de anúncios para usuários fora do site também provavelmente se qualificaria como direcionamento baseado em juros.

O uso de dados fora do site sozinhos para direcionamento provavelmente também seria qualificado como direcionamento baseado em interesses, pois os dados fora do site geralmente são coletados e processados para fazer ilações sobre os interesses dos usuários.

No entanto, o direcionamento de conteúdo ou anúncios usando apenas dados no site normalmente não se qualificaria como direcionamento baseado em interesses. O direcionamento no site que de outra forma não se qualifica como direcionamento baseado em interesses é tratado como dois rótulos distintos. Especificamente, o Label C6 aborda o direcionamento e os relatórios de anúncios no site e fala especificamente para seleção de anúncios, delivery e relatórios, e o Label C7 endereça a seleção, delivery e relatórios de conteúdo no site (direcionamento de conteúdo no site).

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado é da sua responsabilidade. Para referência, as estruturas IAB e DAA são fornecidas abaixo:

IAB: Personalização. A coleta e o processamento de informações sobre o uso desse serviço para personalizar subsequentemente a publicidade e/ou o conteúdo para você em outros contextos, como em outros sites ou aplicativos, ao longo do tempo. Normalmente, o conteúdo do site ou aplicativo é usado para fazer ilações sobre seus interesses, que informam a seleção futura de publicidade e/ou conteúdo.

DAA: Anúncio comportamental online. Coleta de dados de um computador ou dispositivo específico com relação a comportamentos de visualização da Web ao longo do tempo e em sites não afiliados com o objetivo de usar esses dados para prever preferências de usuário ou interesses para fornecer publicidade a esse computador ou dispositivo com base em preferências ou interesses inferidos desses comportamentos de visualização da Web.

#### C6 {#c6}

Anúncios são mensagens ou notificações, incluindo texto e imagens, que aparecem em um site ou aplicativo e destinam-se principalmente a promover a venda de bens ou serviços. Cabe a você determinar a finalidade dessas mensagens ou notificações. Os anúncios são separados do conteúdo no site, coberto pelo rótulo [C7](#c7). Os dados com um rótulo C6 não podem ser usados para direcionamento de anúncios no site, incluindo a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia de tais anúncios. Isso inclui o uso de dados no site coletados anteriormente sobre os interesses dos usuários para selecionar anúncios, processar dados sobre quais anúncios foram mostrados, quando e onde foram exibidos e se os usuários tomaram alguma ação relacionada ao anúncio, como selecionar um anúncio ou fazer uma compra. Normalmente, fazer inferências sobre as preferências de um usuário com base nas atividades no site desse usuário e, em seguida, usar essas preferências no direcionamento de anúncios no site não seria qualificado como direcionamento com base em juros (também chamado de personalização), pois não atenderia a todos os três requisitos necessários para o direcionamento com base em juros. *[Consulte o rótulo C5 para conhecer esses requisitos.](#c5)*

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado é da sua responsabilidade. Para referência, as estruturas IAB e DAA são fornecidas abaixo:

IAB: 3. Seleção de anúncios, delivery, relatórios: A coleta de informações e a combinação com informações coletadas anteriormente, para selecionar e fornecer anúncios para você e para medir a entrega e a eficácia de tais anúncios. Isso inclui o uso de informações coletadas anteriormente sobre seus interesses para selecionar anúncios, processar dados sobre quais anúncios foram mostrados, com que frequência foram exibidos, quando e onde foram mostrados e se você tomou alguma ação relacionada ao anúncio, incluindo, por exemplo, selecionar um anúncio ou fazer uma compra. Isso não inclui a Personalização, que é a coleta e o processamento de informações sobre o uso desse serviço para personalizar subsequentemente a publicidade e/ou o conteúdo para você em outros contextos, como sites ou aplicativos, ao longo do tempo.

DAA: A Publicidade comportamental online não inclui as atividades de Primárias, Entrega de anúncios ou Relatório de anúncios ou publicidade contextual (ou seja, publicidade com base no conteúdo da página da Web que está sendo visitada, visita atual de um consumidor a uma página da Web ou uma consulta de pesquisa).

#### C7 {#c7}

O conteúdo no site é um texto e imagens projetadas para informar, educar ou entreter e que não são criadas para promover a venda de bens ou serviços. Cabe a você determinar a finalidade do conteúdo, incluindo se ele se qualificaria como publicidade nativa. O rótulo C7 não se destina a cobrir anúncios no local, que são cobertos pelo rótulo [C6](#c6). Os dados com um rótulo C7 não podem ser usados para direcionamento de conteúdo no site, incluindo a seleção e entrega de conteúdo nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia de tal conteúdo. Isso inclui informações coletadas anteriormente sobre os interesses dos usuários em conteúdo selecionado, dados de processamento sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo foi exibido, quando e onde foi exibido e se os usuários realizaram ações relacionadas ao conteúdo, incluindo, por exemplo, a seleção de conteúdo. Normalmente, fazer inferências sobre as preferências de um usuário com base nas atividades no site desse usuário e, em seguida, usar essas preferências no direcionamento de conteúdo no site não seria qualificado como direcionamento com base em juros (também chamado de personalização), pois não atenderia a todos os três requisitos necessários para o direcionamento com base em juros. *[Consulte o rótulo C5 para conhecer esses requisitos.](#c5)*

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado é da sua responsabilidade. Para referência, as estruturas IAB e DAA são fornecidas abaixo:

IAB: 4. Seleção de conteúdo, delivery, relatórios: A coleta de informações e a combinação com as informações coletadas anteriormente, para selecionar e fornecer conteúdo para você e para medir a entrega e a eficácia desse conteúdo. Isso inclui o uso de informações coletadas anteriormente sobre seus interesses para selecionar conteúdo, processar dados sobre qual conteúdo foi exibido, com que frequência ou por quanto tempo foi exibido, quando e onde foi exibido e se você tomou alguma ação relacionada ao conteúdo, incluindo, por exemplo, a seleção de conteúdo. Isso não inclui a Personalização, que é a coleta e o processamento de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade para você em outros contextos, como sites ou aplicativos, ao longo do tempo.

DAA: O Anúncio comportamental online não inclui as atividades de Partes primárias, Relatório de entrega de anúncios ou Relatório de anúncios ou publicidade contextual (ou seja, publicidade com base no conteúdo da página da Web que está sendo visitada, visita atual de um consumidor a uma página da Web ou uma consulta de pesquisa).

#### C8 {#c8}

Os dados não podem ser usados para medir, entender e relatar o uso dos sites ou aplicativos de sua organização pelos usuários. Isso não inclui o direcionamento com base em interesses (direcionamento entre sites), que é a coleção de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade em outros contextos, ou seja, em outros serviços, como sites ou aplicativos, ao longo do tempo.

#### C9 {#c9}

Alguns contratos incluem proibições explícitas sobre a utilização de dados para a ciência de dados. Às vezes, elas são redigidas em termos que proíbem o uso de dados para Inteligência Artificial (AI), aprendizado de máquina (ML) ou modelagem.

#### C10 {#c10}

Algumas políticas de uso de dados restringem o uso de dados de identidade compilados para personalização. O rótulo C10 é aplicado automaticamente aos segmentos se suas políticas de mesclagem usarem a opção &quot;gráfico privado&quot;.

#### C11 {#c11}

A Correspondência de segmentos do Adobe Experience Platform permite que você corresponda segmentos primários com preferências de privacidade e consentimento, facilitando a criação de perfis enriquecidos e insights de downstream. O rótulo C11 indica dados que não devem ser usados em processos [!DNL Segment Match]. Depois de determinar quais conjuntos de dados e/ou campos você deseja excluir da Correspondência de segmentos e adicionar o rótulo C11 de acordo, o rótulo é aplicado automaticamente pelo fluxo de trabalho Correspondência de segmentos .
