---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia de solução de problemas de caixas de proteção
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Guia de solução de problemas de caixas de proteção

Este documento fornece respostas para perguntas frequentes sobre caixas de proteção no Adobe Experience Platform. Para questões e solução de problemas relacionados a outros serviços da Platform, consulte o guia [de solução de problemas do](../landing/troubleshooting.md)Experience Platform.

As caixas de proteção particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital. Consulte a visão geral [das](home.md) caixas de proteção para obter mais informações.

## O que é uma caixa de areia?

As caixas de proteção são partições virtuais em uma única instância do Experience Platform. Cada caixa de proteção mantém sua própria biblioteca independente de recursos da Platform (incluindo schemas, conjuntos de dados, perfis etc.). Todo o conteúdo e as ações realizadas em uma caixa de proteção estão confinados apenas a essa caixa de proteção e não afetam nenhuma outra caixa de proteção. Consulte a visão geral [das](home.md) caixas de proteção para obter mais informações.

## Que tipos de caixas de proteção estão disponíveis e quais são as suas diferenças?

Há dois tipos de sandbox disponíveis no Experience Platform:

* Caixa de proteção de produção
* Caixa de proteção de não produção

Experience Platform fornece uma única caixa de proteção **de produção**, que não pode ser excluída ou redefinida. Somente uma caixa de proteção de produção pode existir para uma única instância do Platform.

Por outro lado, várias caixas de proteção **de** não produção podem ser criadas por administradores de caixa de proteção para uma única instância do Platform. As caixas de proteção de não-produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua caixa de proteção de produção. Além disso, as caixas de proteção de não produção têm um recurso de redefinição que remove todos os recursos criados pelo cliente da caixa de proteção. As caixas de proteção de não produção não podem ser convertidas em caixas de proteção de produção.

Consulte a visão geral [das](./home.md) caixas de proteção para obter mais informações.

## Posso acessar um recurso de mais de uma caixa de proteção?

As caixas de proteção são partições isoladas de uma única instância do Platform, com cada caixa de proteção mantendo sua própria biblioteca independente de recursos. Um recurso que existe em uma caixa de proteção não pode ser acessado de nenhuma outra caixa de proteção, independentemente do tipo de caixa de proteção (produção ou não).

## Quantas caixas de areia de produção eu posso ter?

O Experience Platform suporta apenas uma caixa de proteção de produção por Organização IMS, que é fornecida prontamente. Embora a caixa de proteção de produção possa ser renomeada, ela não pode ser excluída ou redefinida. Usuários com permissões de Administração de caixa de proteção podem criar, redefinir e excluir apenas caixas de proteção de não produção.

## Quantas caixas de areia de não produção eu posso ter?

Atualmente, o Experience Platform permite que até 15 caixas de proteção de não produção estejam ativas em uma única Organização IMS.

## Acabei de criar uma caixa de areia. Como faço para definir permissões para os usuários que trabalharão com essa caixa de proteção?

O Adobe Admin Console vincula os usuários a caixas de proteção e permissões por meio do uso de perfis **de** produtos. Depois de criar uma nova caixa de proteção, navegue até a guia _Permissões_ do perfil do produto ao qual você deseja conceder acesso e clique em **Caixas de proteção**. Aqui, você pode adicionar ou remover o acesso à nova caixa de proteção da mesma forma que outras permissões.

Se desejar adicionar permissões exclusivas aos usuários de uma área de segurança específica, talvez seja necessário criar um novo perfil de produto com as caixas de proteção e permissões apropriadas aplicadas e atribuir esses usuários a esse perfil.

Consulte o guia [do usuário do](../access-control/ui/overview.md) controle de acesso para obter mais informações sobre como gerenciar caixas de proteção e permissões no Admin Console.