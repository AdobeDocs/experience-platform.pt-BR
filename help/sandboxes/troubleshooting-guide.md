---
keywords: Experience Platform;home;popular topics;sandbox troubleshooting
solution: Experience Platform
title: Guia de solução de problemas de caixas de proteção
topic: troubleshooting guide
description: Este documento fornece respostas para perguntas frequentes sobre caixas de proteção no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Guia de solução de problemas de caixas de proteção

Este documento fornece respostas para perguntas frequentes sobre caixas de proteção no Adobe Experience Platform. Para questões e solução de problemas relacionados a outros serviços da plataforma, consulte o guia [de solução de problemas do](../landing/troubleshooting.md)Experience Platform.

Os Sandboxes dividem uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital. See the [sandboxes overview](home.md) for more information.

## O que é uma caixa de areia?

As caixas de proteção são partições virtuais em uma única instância do Experience Platform. Cada caixa de proteção mantém sua própria biblioteca independente de recursos da plataforma (incluindo schemas, conjuntos de dados, perfis etc.). Todo o conteúdo e as ações realizadas em uma caixa de proteção estão confinados apenas a essa caixa de proteção e não afetam nenhuma outra caixa de proteção. See the [sandboxes overview](home.md) for more information.

## Que tipos de caixas de proteção estão disponíveis e quais são as suas diferenças?

Há dois tipos de sandbox disponíveis no Experience Platform:

* Caixa de proteção de produção
* Caixa de proteção de não produção

Experience Platform fornece uma única caixa de proteção de produção, que não pode ser excluída ou redefinida. Somente uma caixa de proteção de produção pode existir para uma única instância da Plataforma.

Por outro lado, várias caixas de proteção de não produção podem ser criadas por administradores de caixa de proteção para uma única instância da Plataforma. As caixas de proteção de não-produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua caixa de proteção de produção. Além disso, as caixas de proteção de não produção têm um recurso de redefinição que remove todos os recursos criados pelo cliente da caixa de proteção. As caixas de proteção de não produção não podem ser convertidas em caixas de proteção de produção. Uma licença padrão de Experience Platform concede cinco caixas de proteção (uma produção e quatro não-produção). Você pode adicionar pacotes de dez caixas de proteção de não produção até um máximo de 75 caixas de proteção no total. Entre em contato com seu administrador de organização IMS ou seu representante de vendas de Adobe para obter mais detalhes.

See the [sandboxes overview](./home.md) for more information.

## Posso acessar um recurso de mais de uma caixa de proteção?

As caixas de proteção são partições isoladas de uma única instância da Plataforma, com cada caixa de proteção mantendo sua própria biblioteca independente de recursos. Um recurso que existe em uma caixa de proteção não pode ser acessado de nenhuma outra caixa de proteção, independentemente do tipo de caixa de proteção (produção ou não).

## Quantas caixas de areia de produção eu posso ter?

O Experience Platform suporta apenas uma caixa de proteção de produção por Organização IMS, que é fornecida prontamente. Embora a caixa de proteção de produção possa ser renomeada, ela não pode ser excluída ou redefinida. Usuários com permissões de Administração de caixa de proteção podem criar, redefinir e excluir apenas caixas de proteção de não produção.

## Quantas caixas de areia de não produção eu posso ter?

Atualmente, o Experience Platform permite que até 15 caixas de proteção de não produção estejam ativas em uma única Organização IMS.

## Acabei de criar uma caixa de areia. Como faço para definir permissões para os usuários que trabalharão com essa caixa de proteção?

O Adobe Admin Console vincula os usuários a caixas de proteção e permissões por meio do uso de perfis de produtos. Depois de criar uma nova caixa de proteção, navegue até a guia **Permissões** do perfil do produto ao qual você deseja conceder acesso e clique em **Caixas de proteção**. Aqui, você pode adicionar ou remover o acesso à nova caixa de proteção da mesma forma que outras permissões.

Se desejar adicionar permissões exclusivas aos usuários de uma área de segurança específica, talvez seja necessário criar um novo perfil de produto com as caixas de proteção e permissões apropriadas aplicadas e atribuir esses usuários a esse perfil.

Consulte o guia [do usuário do](../access-control/ui/overview.md) controle de acesso para obter mais informações sobre como gerenciar caixas de proteção e permissões no Admin Console.