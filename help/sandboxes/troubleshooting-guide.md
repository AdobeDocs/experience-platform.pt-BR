---
keywords: Experience Platform, home, tópicos populares, solução de problemas da sandbox
solution: Experience Platform
title: Guia de solução de problemas de sandboxes
topic-legacy: troubleshooting guide
description: Este documento fornece respostas a perguntas frequentes sobre sandboxes no Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 2a7b2040c221ff039f17f78d9ca712032d9fc02c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Guia de solução de problemas de sandboxes

Este documento fornece respostas a perguntas frequentes sobre sandboxes no Adobe Experience Platform. Para dúvidas e solução de problemas relacionados a outros serviços da plataforma, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

As sandboxes particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital. Consulte a [visão geral das sandboxes](home.md) para obter mais informações.

## O que é uma sandbox?

As sandboxes são partições virtuais em uma única instância do Experience Platform. Cada sandbox mantém sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados, perfis e assim por diante). Todo o conteúdo e as ações realizadas em uma sandbox são restritas apenas a essa sandbox e não afetam nenhuma outra sandbox. Consulte a [visão geral das sandboxes](home.md) para obter mais informações.

## Que tipos de sandboxes estão disponíveis e quais são as suas diferenças?

Há dois tipos de sandbox disponíveis no Experience Platform:

* **Sandbox de produção**: Uma sandbox de produção deve ser usada com perfis no ambiente de produção. A Platform permite criar várias sandboxes de produção para fornecer a funcionalidade correta para os dados, mantendo o isolamento operacional. Esse recurso permite dedicar sandboxes de produção específicas a linhas distintas de negócios, marcas, projetos ou regiões. As sandboxes de produção oferecem suporte a um volume de perfis de produção até o seu [!DNL Profile] compromisso (medido cumulativamente em todas as sandboxes de produção autorizadas). Você tem direito a usar o perfil médio licenciado por autorizado [!DNL Profile] (medido cumulativamente em todas as sandboxes de produção autorizadas).
* **sandbox de desenvolvimento**: Uma sandbox de desenvolvimento é uma sandbox que pode ser usada exclusivamente para desenvolvimento e testes com perfis não relacionados à produção. As sandboxes de desenvolvimento oferecem suporte a um volume de perfis de não produção de até 10% de seu [!DNL Profile] compromisso (medido cumulativamente em todas as sandboxes de desenvolvimento autorizadas). Você tem direito a até:
   * Uma riqueza média de perfis de não produção de 75 quilobytes por perfil de não produção autorizado (medida cumulativamente em todas as sandboxes de desenvolvimento autorizadas);
   * Um trabalho de segmentação em lote por dia, por sandbox de desenvolvimento;
   * Uma média de 120 [!DNL Profile] chamadas de API, por [!DNL Profile], por ano (medido cumulativamente em todas as sandboxes de desenvolvimento autorizadas.

Consulte a [visão geral das sandboxes](./home.md) para obter mais informações.

## Posso acessar um recurso de mais de uma sandbox?

As sandboxes são partições isoladas de uma única instância da Platform, com cada sandbox mantendo sua própria biblioteca independente de recursos. Um recurso que existe em uma sandbox não pode ser acessado de nenhuma outra sandbox, independentemente do tipo de sandbox (produção ou não produção).

## Qual é a sandbox de produção padrão?

A sandbox de produção padrão é a primeira sandbox de produção criada quando uma Organização IMS é provisionada pela primeira vez. A sandbox de produção padrão permite assimilar ou consumir dados da Platform, bem como aceitar solicitações que não incluem valores para um nome de sandbox ou ID de sandbox. A sandbox de produção padrão pode ser redefinida, mas não excluída.

## Quantas sandboxes de produção posso ter?

Uma instância do Experience Platform suporta várias sandboxes de produção e desenvolvimento, com cada sandbox mantendo sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados e perfis).

Uma licença Experience Platform padrão concede um total de cinco sandboxes, que podem ser classificadas como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total.

As sandboxes de produção podem ser redefinidas ou excluídas, exceto as sandboxes de produção que também estão sendo usadas pela Adobe Analytics para a [Análise entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=pt-BR) ou se o gráfico de identidade hospedado nele também estiver sendo usado pela Adobe Audience Manager para o [Destinos com base em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) recurso.

Você pode atualizar o título de uma sandbox de produção. No entanto, uma sandbox de produção não pode ser renomeada.

>[!NOTE]
>
>O nome da sandbox é usado para fins de pesquisa em chamadas de API, enquanto o título da sandbox é usado como o nome de exibição.

## Quantas sandboxes de desenvolvimento posso ter?

Atualmente, o Experience Platform permite que no máximo 75 sandboxes (produção e desenvolvimento) estejam ativas em uma única Organização IMS.

As sandboxes de desenvolvimento são compatíveis com as funcionalidades de redefinição e exclusão.

## Acabei de criar uma sandbox. Como faço para definir permissões para os usuários que trabalharão com esta sandbox?

O Adobe Admin Console vincula usuários a sandboxes e permissões por meio do uso de perfis de produtos. Depois de criar uma nova sandbox, navegue até o **Permissões** guia do perfil de produto ao qual você deseja conceder acesso e clique em **Sandboxes**. A partir daqui, você pode adicionar ou remover o acesso à nova sandbox da mesma forma que outras permissões.

Se quiser adicionar permissões exclusivas aos usuários de uma sandbox específica, pode ser necessário criar um novo perfil de produto com as sandboxes e permissões apropriadas aplicadas e atribuir esses usuários a esse perfil.

Consulte a [guia do usuário de controle de acesso](../access-control/ui/overview.md) para obter mais informações sobre gerenciamento de sandboxes e permissões no Admin Console.
