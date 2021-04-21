---
keywords: Experience Platform, home, tópicos populares, solução de problemas da sandbox
solution: Experience Platform
title: Guia de solução de problemas de sandboxes
topic-legacy: troubleshooting guide
description: Este documento fornece respostas a perguntas frequentes sobre sandboxes no Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Guia de solução de problemas de sandboxes

Este documento fornece respostas a perguntas frequentes sobre sandboxes no Adobe Experience Platform. Para dúvidas e solução de problemas relacionados a outros serviços da plataforma, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

As sandboxes particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital. Consulte a [visão geral das sandboxes](home.md) para obter mais informações.

## O que é uma sandbox?

As sandboxes são partições virtuais em uma única instância do Experience Platform. Cada sandbox mantém sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados, perfis e assim por diante). Todo o conteúdo e as ações realizadas em uma sandbox são restritas apenas a essa sandbox e não afetam nenhuma outra sandbox. Consulte a [visão geral das sandboxes](home.md) para obter mais informações.

## Que tipos de sandboxes estão disponíveis e quais são as suas diferenças?

Há dois tipos de sandbox disponíveis no Experience Platform:

* Sandbox de produção
* Caixa de proteção de não produção

O Experience Platform fornece uma única sandbox de produção, que não pode ser excluída ou redefinida. Somente uma sandbox de produção pode existir para uma única instância da Platform.

Por outro lado, várias sandboxes de não produção podem ser criadas por administradores de sandbox para uma única instância da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar a sandbox de produção. Além disso, as sandboxes de não produção têm um recurso de redefinição que remove todos os recursos criados pelo cliente da sandbox. As sandboxes de não produção não podem ser convertidas em sandboxes de produção. Uma licença padrão do Experience Platform concede cinco sandboxes (uma produção e quatro não produção). É possível adicionar pacotes de dez sandboxes de não produção até um máximo de 75 sandboxes totais. Entre em contato com o administrador de organização IMS ou o representante de vendas de Adobe para obter mais detalhes.

Consulte a [visão geral das sandboxes](./home.md) para obter mais informações.

## Posso acessar um recurso de mais de uma sandbox?

As sandboxes são partições isoladas de uma única instância da Platform, com cada sandbox mantendo sua própria biblioteca independente de recursos. Um recurso que existe em uma sandbox não pode ser acessado de nenhuma outra sandbox, independentemente do tipo de sandbox (produção ou não produção).

## Quantas sandboxes de produção posso ter?

O Experience Platform suporta apenas uma sandbox de produção por Organização IMS, que é fornecida pronta para uso. Embora a sandbox de produção possa ser renomeada, ela não pode ser excluída ou redefinida. Os usuários com permissões de Administração de sandbox só podem criar, redefinir e excluir sandboxes que não sejam de produção.

## Quantas sandboxes de não produção eu posso ter?

Atualmente, o Experience Platform permite que até 15 sandboxes de não produção estejam ativas em uma única Organização IMS.

## Acabei de criar uma sandbox. Como faço para definir permissões para os usuários que trabalharão com esta sandbox?

O Adobe Admin Console vincula usuários a sandboxes e permissões por meio do uso de perfis de produtos. Depois de criar uma nova sandbox, navegue até a guia **Permissões** do perfil de produto ao qual deseja conceder acesso e clique em **Sandboxes**. A partir daqui, você pode adicionar ou remover o acesso à nova sandbox da mesma forma que outras permissões.

Se quiser adicionar permissões exclusivas aos usuários de uma sandbox específica, pode ser necessário criar um novo perfil de produto com as sandboxes e permissões apropriadas aplicadas e atribuir esses usuários a esse perfil.

Consulte o [guia do usuário de controle de acesso](../access-control/ui/overview.md) para obter mais informações sobre o gerenciamento de sandboxes e permissões no Admin Console.
