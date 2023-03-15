---
keywords: Experience Platform;página inicial;tópicos populares;solução de problemas de sandbox
solution: Experience Platform
title: Guia de solução de problemas de sandboxes
description: Este documento fornece respostas a perguntas frequentes sobre sandboxes na Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# Guia de solução de problemas de sandboxes

Este documento fornece respostas a perguntas frequentes sobre sandboxes na Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros serviços da Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

As sandboxes dividem uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital. Consulte a [visão geral das sandboxes](home.md) para obter mais informações.

## O que é uma sandbox?

As sandboxes são partições virtuais dentro de uma única instância do Experience Platform. Cada sandbox mantém sua própria biblioteca independente de recursos da Platform (incluindo esquemas, conjuntos de dados, perfis e assim por diante). Todo o conteúdo e as ações realizadas em uma sandbox estão confinados somente a essa sandbox e não afetam outras sandboxes. Consulte a [visão geral das sandboxes](home.md) para obter mais informações.

## Quais tipos de sandboxes estão disponíveis e quais são suas diferenças? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Tipo de sandbox"
>abstract="O tipo de sandbox indica se é uma sandbox de produção ou desenvolvimento. As sandboxes de produção incluem dados em tempo real e as sandboxes de desenvolvimento são usadas para teste e desenvolvimento."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="Criar uma sandbox na interface do"

Há dois tipos de sandbox disponíveis no Experience Platform:

* **Sandbox de produção**: uma sandbox de produção deve ser usada com perfis em seu ambiente de produção. A Platform permite criar várias sandboxes de produção para fornecer a funcionalidade certa para os dados e, ao mesmo tempo, manter o isolamento operacional. Esse recurso permite dedicar sandboxes de produção específicas a linhas de negócios, marcas, projetos ou regiões distintas. As sandboxes de produção aceitam um volume de perfis de produção até o limite do [!DNL Profile] compromisso (medido cumulativamente em todas as sandboxes de produção autorizadas). Você está autorizado a usar o perfil médio licenciado por pessoa autorizada [!DNL Profile] (medido cumulativamente em todas as sandboxes de produção autorizadas).
* **Sandbox de desenvolvimento**: uma sandbox de desenvolvimento é uma sandbox que pode ser usada exclusivamente para desenvolvimento e testes com perfis de não produção. As sandboxes de desenvolvimento são compatíveis com um volume de perfis de não produção até 10% do volume de [!DNL Profile] compromisso (medido cumulativamente em todas as sandboxes de desenvolvimento autorizadas). Você tem direito a até:
   * Uma riqueza média de perfil de não produção de 75 quilobytes por perfil de não produção autorizado (medida cumulativamente em todas as sandboxes de desenvolvimento autorizadas);
   * Um trabalho de segmentação em lote por dia, por sandbox de desenvolvimento;
   * Uma média de 120 [!DNL Profile] Chamadas de API, por [!DNL Profile], por ano (medido cumulativamente em todas as sandboxes de desenvolvimento autorizadas.

Consulte a [visão geral das sandboxes](./home.md) para obter mais informações.

## Posso acessar um recurso de mais de uma sandbox?

As sandboxes são partições isoladas de uma única instância da Platform, com cada sandbox mantendo sua própria biblioteca de recursos independente. Um recurso que existe em uma sandbox não pode ser acessado de outra sandbox, independentemente do tipo de sandbox (produção ou não produção).

## Qual é a sandbox de produção padrão?

A sandbox de produção padrão é a primeira sandbox de produção criada quando uma Organização IMS é provisionada pela primeira vez. A sandbox de produção padrão permite assimilar ou consumir dados da Platform, bem como aceitar solicitações que não incluem valores para um nome de sandbox ou uma ID de sandbox. A sandbox de produção padrão pode ser redefinida, mas não excluída.

## Quantas sandboxes de produção posso ter?

Uma instância do Experience Platform é compatível com várias sandboxes de produção e desenvolvimento, com cada sandbox mantendo sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados e perfis).

Uma licença de Experience Platform padrão concede um total de cinco sandboxes, que você pode classificar como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total.

As sandboxes de produção podem ser redefinidas ou excluídas, exceto para sandboxes de produção que também estão sendo usadas pela Adobe Analytics para o [Análise entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=pt-BR) ou se o gráfico de identidade hospedado nele também estiver sendo usado pelo Adobe Audience Manager para a [Destinos com base em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=pt-BR) recurso.

Você pode atualizar o título de uma sandbox de produção. No entanto, uma sandbox de produção não pode ser renomeada.

>[!NOTE]
>
>O nome da sandbox é usado para fins de pesquisa em chamadas de API, enquanto o título da sandbox é usado como o nome de exibição.

## Quantas sandboxes de desenvolvimento posso ter?

Atualmente, o Experience Platform permite que um máximo de 75 sandboxes totais (produção e desenvolvimento) estejam ativas em uma única Organização IMS.

As sandboxes de desenvolvimento são compatíveis com as funcionalidades de redefinição e exclusão.

## Acabei de criar uma caixa de areia. Como defino permissões para os usuários que trabalharão com essa sandbox?

O Adobe Admin Console vincula usuários a sandboxes e permissões por meio do uso de perfis de produto. Depois de criar uma nova sandbox, navegue até a **Permissões** do perfil de produto ao qual deseja conceder acesso e clique em **Sandboxes**. Aqui, você pode adicionar ou remover o acesso à nova sandbox da mesma maneira que outras permissões.

Se quiser adicionar permissões exclusivas aos usuários de uma sandbox específica, talvez seja necessário criar um novo perfil de produto com as sandboxes e permissões apropriadas aplicadas e atribuir esses usuários a esse perfil.

Consulte a [guia do usuário de controle de acesso](../access-control/ui/overview.md) para obter mais informações sobre como gerenciar sandboxes e permissões no Admin Console.
