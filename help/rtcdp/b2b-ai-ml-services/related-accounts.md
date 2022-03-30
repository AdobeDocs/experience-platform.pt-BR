---
title: Contas relacionadas no Real-Time CDP B2B Edition
type: Documentation
description: Uma visão geral e mais informações sobre o recurso de contas relacionadas no Experience Platform Real-time CDP B2B.
source-git-commit: 09fd6c30461a4229411ce67426fdcb247661f7cb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Contas relacionadas no Real-Time CDP B2B Edition

## Visão geral {#overview}

As empresas B2B geralmente têm as informações de seus clientes armazenadas em vários sistemas, cada um incluindo apenas dados parciais ou até mesmo conflitantes para a mesma entidade de negócios real. Isto cria um enorme desafio de chegar a uma visão precisa dos seus clientes, reduzindo assim a eficiência e a eficácia dos seus esforços de marketing e vendas B2B.

| ID | Nome | Site | Setor | Estado | Telefone | Tem oportunidade aberta com valor > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |  |
| 2 | Acme | acm.com | Software | CA | 408536000 | x |
| 3 | Acme Inc |  |  | CA | (408)5366000 |  |
| 4 | Serviço Acme Consulting | `http://www.acme.com/consulting` | Consultoria em tecnologia | NY | (212)471-0904 | x |
| 5 | Acme IT |  |  | CA |  |  |

{style=&quot;table-layout:auto&quot;}

Com contas relacionadas, [!DNL Real-time CDP B2B] O agora mostra uma lista de contas semelhantes à conta que você está navegando.

![Tela mostrando contas relacionadas na interface do usuário do Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Use esse recurso para visualizar perfis de conta relacionados para um perfil de conta na interface do usuário do Experience Platform e, em seguida, incluir as contas relacionadas em suas definições de segmento para ampliar seu alcance ou aplicar critérios mais amplos em seus segmentos.

## Como funciona {#how-it-works}

Os trabalhos de aprendizado de máquina executados diariamente usam um algoritmo hierárquico para agrupar perfis de conta semelhantes em grupos com base em três fatores:

* Link da conta pai
* Domínio da Web
* Nome da conta

Após um trabalho de processamento bem-sucedido, cada membro do grupo de perfis de conta é marcado com a lista Contas Relacionadas . É possível exibir a lista na **Contas Relacionadas** na página Perfil da conta e use as contas relacionadas nas definições do segmento.

Consulte a documentação para obter mais informações sobre o [tarefas de contas relacionadas ao enriquecimento de perfil](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Como visualizar contas relacionadas {#how-to-view}

Você pode visualizar contas relacionadas de uma conta que está navegando na interface do usuário do Experience Platform.

Consulte a documentação para obter mais informações sobre o [como encontrar contas relacionadas na interface do usuário](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Como usar contas relacionadas {#how-to-use}

Você pode usar contas e contas relacionadas na segmentação. A decisão de usar contas relacionadas nas definições de segmento depende do caso de uso de marketing. Por exemplo, você pode usar contas relacionadas para campanhas de marketing por email ou publicidade, onde pode aceitar uma precisão menor em troca de um alcance maior.

Consulte um [exemplo de segmentação](/help/rtcdp/segmentation/b2b.md#related-account) que usa contas relacionadas.