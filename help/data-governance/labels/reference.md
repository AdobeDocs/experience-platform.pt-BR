---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;uso de dados rótulo api;política serviço api;dados suportados uso rótulos;rótulos de contrato;rótulos de identidade rótulos;rótulos sensíveis
solution: Experience Platform
title: Glossário de rótulos de uso de dados
description: Este documento descreve todos os rótulos de uso de dados atualmente compatíveis com o Adobe Experience Platform.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 7%

---

# Glossário de rótulos de uso de dados {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Tipos de rótulos"
>abstract="Há várias categorias de rótulos de uso de dados. Os rótulos definidos pela Adobe incluem rótulos de contrato, rótulos de identidade e rótulos sensíveis. Rótulos definidos pela sua organização são categorizados como rótulos personalizados."
>text="See the data usage labels glossary for more information on these label types."

Os rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as [políticas de governança](../policies/overview.md) e as [políticas de controle de acesso](../../access-control/abac/overview.md) que se aplicam a esses dados. O Adobe Experience Platform fornece vários rótulos de uso de dados principais prontos para uso que você pode usar para começar a categorizar seus dados.

Este documento descreve os rótulos de uso de dados principais fornecidos atualmente pela Experience Platform.

## Rótulos de contrato {#contract}

Os rótulos de contrato (C) são usados para categorizar dados que contêm obrigações contratuais ou estão relacionados às políticas de governança de dados da sua organização.

| Rótulo | Definição |
| --- | --- |
| [C1](#c1) | Os dados só podem ser exportados da Adobe Experience Cloud de forma agregada sem incluir identificadores individuais ou de dispositivo. |
| [C2](#c2) | Os dados não podem ser exportados para terceiros. |
| [C3](#c3) | Os dados não podem ser combinados nem utilizados de outra forma com informações diretamente identificáveis. |
| [C4](#c4) | Os dados não podem ser usados para direcionar anúncios ou conteúdo, no local ou entre locais. |
| [C5](#c5) | Os dados não podem ser usados para direcionamento de conteúdo ou anúncios entre sites com base em interesses. |
| [C6](#c6) | Os dados não podem ser utilizados para direcionamento de anúncios no local. |
| [C7](#c7) | Os dados não podem ser utilizados para o direcionamento de conteúdo no local. |
| [C8](#c8) | Os dados não podem ser usados para medir os sites ou aplicativos de sua organização. |
| [C9](#c9) | Os dados não podem ser usados em fluxos de trabalho de ciência de dados. |
| [C10](#c10) | Os dados não podem ser usados para ativação de identidade compilada. |
| [C11](#c11) | Os dados não podem ser compartilhados com parceiros de Correspondência de Segmentos. |
| [C12](#c12) | Os dados não podem ser exportados de forma alguma. |

## Rótulos de identidade {#identity}

Os rótulos “I” de identidade são usados para categorizar dados que podem identificar ou entrar em contato com uma pessoa específica.

| Rótulo | Definição |
| --- | --- |
| **I1** | Dados diretamente identificáveis que podem identificar ou entrar em contato com uma pessoa específica, em vez de com um dispositivo. |
| **I2** | Dados indiretamente identificáveis que podem ser utilizados em ção com quaisquer outros dados para identificar ou contactar uma pessoa específica. |

## Rótulos de sensibilidade {#sensitive}

Os rótulos de sensibilidade (S) são usados para categorizar dados que você e sua organização consideram sensíveis.

Um tipo de dados que você pode considerar confidenciais pode ser o de diferentes tipos de dados geográficos; no entanto, essa categoria não se limita a dados geográficos.

| Rótulo | Definição |
| --- | --- |
| **S1** | Dados que especificam a latitude e a longitude que podem ser utilizados para determinar a localização precisa de um dispositivo. |
| **S2** | Dados que podem ser utilizados para determinar uma área de cerca geográfica amplamente definida. |
| **PSPD** | Dados pessoais confidenciais permitidos (PSPD) refere-se aos dados que você tem permissão contratual do Adobe para carregar e que são considerados &quot;confidenciais&quot;, &quot;categoria especial de dados&quot; ou um termo semelhante usado pelas leis aplicáveis. Isso exclui especificamente as Informações de Saúde Protegidas (PHI) e outros dados de saúde regulamentados. |
| **RHD** | Dados que se referem a PHI (Protected Health Information, informações protegidas de saúde) ou informações sobre um paciente que você tem permissão contratual do Adobe para carregar. |

## Rótulos de ecossistema de parceiros {#partner}

Os rótulos do ecossistema do parceiro são usados para categorizar dados obtidos de fontes externas à sua organização.

Este rótulo é usado para controlar o uso de dados de prospecto.

| Rótulo | Definição |
| --- | --- |
| **Terceiros** | Dados de terceiros são dados fornecidos a você por um fornecedor de dados de terceiros. Um fornecedor de dados de terceiros é uma entidade que celebrou um contrato com sua organização autorizando você a acessar, usar, exibir e transmitir os dados de terceiros em conjunto com a Experience Platform. |
| **Enriquecimento de Terceiros** | Dados coletados por uma organização de terceiros que não esteja diretamente relacionada ao titular dos dados. O rótulo deve ser aplicado aos dados de terceiros usados para enriquecer perfis primários. |
| **Prospecção de Terceiros** | Dados coletados por uma organização de terceiros que não esteja diretamente relacionada ao titular dos dados. A etiqueta deve ser aplicada aos dados de terceiros usados além da prospecção da funnel para novos clientes em rede. |

## Apêndice

As seções abaixo fornecem informações adicionais sobre os rótulos de uso de dados disponíveis.

### Detalhes do rótulo do contrato

As seções seguintes fornecem informações detalhadas relacionadas à implementação de rótulos &quot;C&quot; de contrato específicos.

#### C1 {#c1}

Alguns dados só podem ser exportados do Adobe Experience Cloud de forma agregada sem incluir identificadores individuais ou de dispositivo. Por exemplo, dados originados de redes sociais.

#### C2 {#c2}

Alguns provedores de dados têm termos em seus contratos que proíbem a exportação de dados de onde foram originalmente coletados. Por exemplo, os contratos de redes sociais geralmente restringem a transferência de dados recebidos deles. O rótulo C2 é mais restritivo que [C1](#c1), que requer apenas agregação e dados anônimos, mas é menos restritivo que [C12](#c12), o que impede exportações de dados completamente, independentemente do destino.

#### C3 {#c3}

Alguns provedores de dados têm termos em seus contratos que proíbem a combinação ou o uso desses dados com informações diretamente identificáveis. Por exemplo, os contratos para dados obtidos a partir de redes de publicidade, servidores de publicidade e fornecedores de dados de terceiros incluem frequentemente proibições contratuais específicas sobre a utilização desses dados com dados diretamente identificáveis.

#### C4 {#c4}

C4 abrange os rótulos [C5](#c5), [C6](#c6) e [C7](#c7). É um dos rótulos mais restritivos, perdendo apenas para [C12](#c12).

#### C5 {#c5}

O direcionamento baseado em interesses, ou personalização, ocorre se as três condições a seguir forem atendidas: os dados coletados no site são (1) usados para fazer deduções sobre os interesses de um usuário, (2) usados em outro contexto, como em outro site ou aplicativo (fora do site) E (3) usados para selecionar qual conteúdo ou anúncios são veiculados com base nessas deduções.

A combinação de dados de vários sites, incluindo uma combinação de dados internos e externos ou uma combinação de dados de várias fontes externas, é chamada de dados entre sites. Sites diferentes representam contextos diferentes, de modo que o uso de dados entre sites em qualquer contexto é diferente do original. Normalmente, os dados entre sites são coletados e processados para deduzir os interesses dos usuários. Como resultado, o uso de dados entre sites para direcionar anúncios ou conteúdo normalmente se qualifica como direcionamento baseado em interesses, independentemente de o anúncio ou conteúdo aparecer no site ou fora dele. Por exemplo, se os dados no site fossem usados em combinação com os dados fora do site para selecionar qual anúncio mostrar a um usuário no site de uma organização, esse uso seria qualificado como direcionamento baseado em interesses. Como outro exemplo, o redirecionamento de anúncios para usuários fora do site também provavelmente se qualificaria como direcionamento baseado em interesses.

O uso de dados externos por si só para direcionamento provavelmente também se qualificaria como direcionamento baseado em interesses, já que os dados externos geralmente são coletados e processados para deduzir os interesses dos usuários.

No entanto, o direcionamento de conteúdo ou anúncios que usam apenas dados no site normalmente não se qualificaria como direcionamento baseado em interesses. O direcionamento no site que, de outra forma, não se qualifica como direcionamento baseado em interesses é tratado como dois rótulos distintos. Especificamente, o Rótulo C6 aborda o direcionamento e a geração de relatórios de anúncios no site e especificamente a seleção, a entrega e a geração de relatórios de anúncios, e o Rótulo C7 aborda a seleção, a entrega e a geração de relatórios de conteúdo no site (direcionamento de conteúdo no site).

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado depende de você. Para referência, as estruturas IAB e DAA são fornecidas abaixo:

IAB: Personalization A coleta e o processamento de informações sobre o uso desse serviço para personalizar subsequentemente a publicidade e/ou o conteúdo para você em outros contextos, como em outros sites ou aplicativos, ao longo do tempo. Normalmente, o conteúdo do site ou aplicativo é usado para fazer conclusões sobre seus interesses que informam a seleção futura de publicidade e/ou conteúdo.

DAA: publicidade comportamental online. Coleta de dados de um computador ou dispositivo específico sobre os comportamentos de visualização da Web ao longo do tempo e em sites não afiliados com o objetivo de usar esses dados para prever as preferências ou os interesses do usuário para fornecer publicidade a esse computador ou dispositivo com base nas preferências ou nos interesses inferidos desses comportamentos de visualização da Web.

#### C6 {#c6}

Anúncios são mensagens ou notificações, incluindo texto e imagens, que aparecem em um site ou aplicativo destinado principalmente a promover a venda de bens ou serviços. Cabe a você determinar a finalidade dessas mensagens ou notificações. Os anúncios são separados do conteúdo no site, coberto pelo rótulo [C7](#c7). Os dados com um rótulo C6 não podem ser usados para direcionamento de anúncios no site, incluindo a seleção e a entrega de anúncios nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia desses anúncios. Isso inclui o uso de dados coletados anteriormente no site sobre os interesses dos usuários para selecionar anúncios, dados de processo sobre quais anúncios foram mostrados, quando e onde foram mostrados e se os usuários tomaram alguma ação relacionada ao anúncio, como selecionar um anúncio ou fazer uma compra. Normalmente, inferir sobre as preferências de um usuário com base nas atividades dele no site e, em seguida, usar essas preferências no direcionamento de anúncios no site não se qualificaria como direcionamento com base em interesses (também chamado de personalização), já que não atenderia a todos os três requisitos necessários para o direcionamento com base em interesses. *[Consulte o rótulo C5 para estes requisitos.](#c5)*

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado depende de você. Para referência, as estruturas IAB e DAA são fornecidas abaixo:

IAB: 3. Seleção de anúncios, delivery, relatórios: a coleção de informações e a combinação com informações coletadas anteriormente, para selecionar e entregar anúncios para você e para medir o delivery e a eficácia desses anúncios. Isso inclui o uso de informações coletadas anteriormente sobre seus interesses para selecionar anúncios, processar dados sobre quais anúncios foram exibidos, com que frequência foram exibidos, quando e onde foram exibidos e se você tomou alguma ação relacionada ao anúncio, incluindo, por exemplo, selecionar um anúncio ou fazer uma compra. Isso não inclui o Personalization, que é a coleta e o processamento de informações sobre o uso desse serviço para personalizar subsequentemente a publicidade e/ou o conteúdo para você em outros contextos, como sites ou aplicativos, ao longo do tempo.

DAA: a publicidade comportamental online não inclui as atividades primárias, a entrega de anúncios ou relatórios de anúncios, ou publicidade contextual (ou seja, publicidade baseada no conteúdo da página da Web que está sendo visitada, a visita atual de um consumidor a uma página da Web ou uma consulta de pesquisa).

#### C7 {#c7}

O conteúdo no site é um texto e imagens criados para informar, educar ou divertir-se, e não são criados para promover a venda de bens ou serviços. Cabe a você determinar a finalidade do conteúdo, incluindo se o conteúdo se qualificaria como publicidade nativa. O rótulo C7 não pretende abranger anúncios no site, que são cobertos pelo rótulo [C6](#c6). Os dados com um rótulo C7 não podem ser usados para direcionamento de conteúdo no site, incluindo a seleção e a entrega de conteúdo nos sites ou aplicativos da organização, ou para medir a entrega e a eficácia desse conteúdo. Isso inclui informações coletadas anteriormente sobre os interesses dos usuários em um conteúdo selecionado, o processamento de dados sobre qual conteúdo foi mostrado, com que frequência ou por quanto tempo ele foi exibido, quando e onde foi exibido e se os usuários realizaram alguma ação relacionada ao conteúdo, incluindo, por exemplo, a seleção de conteúdo. Normalmente, inferir sobre as preferências de um usuário com base nas atividades dele no site e, em seguida, usar essas preferências no direcionamento de conteúdo no site não se qualificaria como direcionamento com base em interesses (também chamado de personalização), já que não atenderia a todos os três requisitos necessários para o direcionamento com base em interesses. *[Consulte o rótulo C5 para estes requisitos.](#c5)*

Em última análise, a interpretação do rótulo e como o uso de dados com esse rótulo é aplicado depende de você. Para referência, as estruturas IAB e DAA são fornecidas abaixo:

IAB: 4. Seleção de conteúdo, delivery, relatórios: a coleta de informações e a combinação com informações coletadas anteriormente, para selecionar e fornecer conteúdo para você e para medir o delivery e a eficácia desse conteúdo. Isso inclui o uso de informações coletadas anteriormente sobre seus interesses para selecionar o conteúdo, processar dados sobre qual conteúdo foi mostrado, com que frequência ou por quanto tempo ele foi exibido, quando e onde foi exibido e se você executou alguma ação relacionada ao conteúdo, incluindo, por exemplo, a seleção de conteúdo. Isso não inclui o Personalization, que é a coleta e o processamento de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade para você em outros contextos, como sites ou aplicativos, ao longo do tempo.

DAA: a Publicidade comportamental online não inclui as atividades de Terceiros, Entrega de anúncio ou Relatórios de anúncio, ou publicidade contextual (ou seja, publicidade baseada no conteúdo da página da Web que está sendo visitada, visita atual de um consumidor a uma página da Web ou uma consulta de pesquisa).

#### C8 {#c8}

Os dados não podem ser usados para medir, entender e relatar o uso que os usuários fazem dos sites ou aplicativos de sua organização. Isso não inclui o direcionamento com base em interesses (direcionamento entre sites), que é a coleção de informações sobre o uso desse serviço para personalizar subsequentemente o conteúdo e/ou a publicidade para você em outros contextos, ou seja, em outros serviços, como sites ou aplicativos, ao longo do tempo.

#### C9 {#c9}

Alguns contratos incluem proibições explícitas sobre o uso de dados para ciência de dados. Às vezes, esses termos são redigidos em termos que proíbem o uso de dados para Inteligência artificial (IA), aprendizado de máquina (ML) ou modelagem.

#### C10 {#c10}

Algumas políticas de governança de dados restringem o uso de dados de identidade compilados para personalização. O rótulo C10 é aplicado automaticamente a públicos se suas políticas de mesclagem usarem a opção &quot;gráfico privado&quot;.

#### C11 {#c11}

A correspondência de segmentos do Adobe Experience Platform permite combinar públicos-alvo gerados pela Experience Platform com preferências de privacidade e consentimento, facilitando a criação de perfis aprimorados e insights de downstream. O rótulo C11 indica dados que não devem ser usados em [!DNL Segment Match] processos. Depois de determinar quais conjuntos de dados e/ou campos você deseja excluir da Correspondência de segmentos e adicionar o rótulo C11 adequadamente, o rótulo é aplicado automaticamente pelo fluxo de trabalho da Correspondência de segmentos.

#### C12 {#c12}

Dados com este rótulo não podem ser exportados do Experience Platform de forma alguma. Os campos rotulados com C12 são excluídos dos downloads de CSV, do consumo de API e dos workflows de ativação.
