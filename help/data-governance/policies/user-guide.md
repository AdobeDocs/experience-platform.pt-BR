---
keywords: Experience Platform, home, tópicos populares, governança de dados, guia do usuário da política de uso de dados
solution: Experience Platform
title: Gerenciar políticas de uso de dados na interface do usuário
topic-legacy: policies
description: A Governança de dados do Adobe Experience Platform fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que podem ser executadas no espaço de trabalho Políticas na interface do usuário do Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# Gerenciar políticas de uso de dados na interface do usuário

A Governança de dados do Adobe Experience Platform fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que podem ser executadas na **Políticas** na área de trabalho do [!DNL Experience Platform] interface do usuário.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, é necessário habilitar manualmente essa política. Consulte a seção sobre [como ativar políticas](#enable) para obter etapas sobre como fazer isso na interface do usuário do .

## Pré-requisitos

Este guia requer uma compreensão funcional do seguinte [!DNL Experience Platform] conceitos:

- [Governança de dados](../home.md)
- [Políticas de uso de dados](./overview.md)

## Exibir políticas existentes {#view-policies}

No [!DNL Experience Platform] UI, selecione **[!UICONTROL Políticas]** para abrir o **[!UICONTROL Políticas]** espaço de trabalho. No **[!UICONTROL Procurar]** , você pode ver uma lista de políticas disponíveis, incluindo seus rótulos associados, ações de marketing e status.

![](../images/policies/browse-policies.png)

Selecione uma política listada para exibir sua descrição e tipo. Se uma política personalizada for selecionada, serão exibidos controles adicionais para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política personalizada {#create-policy}

Para criar uma nova política de uso de dados personalizada, selecione **[!UICONTROL Criar política]** no canto superior direito do **[!UICONTROL Procurar]** na guia no **[!UICONTROL Políticas]** espaço de trabalho.

![](../images/policies/create-policy-button.png)

O **[!UICONTROL Criar política]** workflow é exibido. Comece fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Selecionar **[!UICONTROL Próximo]** quando terminar.

![](../images/policies/add-labels.png)

O **[!UICONTROL Selecionar ações de marketing]** será exibida. Escolha as ações de marketing apropriadas na lista fornecida e selecione **[!UICONTROL Próximo]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OU&quot;. Por outras palavras, a política aplica-se se **any** As ações de marketing selecionadas são executadas.

![](../images/policies/add-marketing-actions.png)

O **[!UICONTROL Revisão]** será exibida, permitindo que você revise os detalhes da nova política antes de criá-la. Depois de satisfeito, selecione **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

O **[!UICONTROL Procurar]** A guia será exibida novamente, listando agora a política recém-criada no status &quot;Rascunho&quot;. Para ativar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

## Ativar ou desativar uma política {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, você deve habilitar manualmente essa política por meio da API ou da interface do usuário.

Você pode ativar ou desativar as políticas da **[!UICONTROL Procurar]** na guia no **[!UICONTROL Políticas]** espaço de trabalho. Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Exibir ações de marketing {#view-marketing-actions}

No **[!UICONTROL Políticas]** na área de trabalho, selecione o **[!UICONTROL Ações de marketing]** para exibir uma lista das ações de marketing disponíveis definidas pelo Adobe e sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, selecione **[!UICONTROL Criar ação de marketing]** no canto superior direito do **[!UICONTROL Ações de marketing]** na guia no **[!UICONTROL Políticas]** espaço de trabalho.

![](../images/policies/create-marketing-action.png)

O **[!UICONTROL Criar ação de marketing]** será exibida. Insira um nome e uma descrição para a ação de marketing e selecione **[!UICONTROL Criar]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada é exibida no **[!UICONTROL Ações de marketing]** guia . Agora você pode usar a ação de marketing ao [criação de novas políticas de uso de dados](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente as ações de marketing personalizadas definidas pela sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

No **[!UICONTROL Políticas]** na área de trabalho, selecione o **[!UICONTROL Ações de marketing]** para exibir uma lista das ações de marketing disponíveis definidas pelo Adobe e sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, você poderá excluí-la selecionando **[!UICONTROL Excluir ação de marketing]**.

>[!NOTE]
>
>A tentativa de excluir uma ação de marketing que está sendo usada por uma política existente causará a exibição de uma mensagem de erro, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar políticas de uso de dados no [!DNL Experience Platform] IU. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o [guia do desenvolvedor](../api/getting-started.md). Para obter informações sobre como aplicar políticas de uso de dados, consulte [visão geral da aplicação de políticas](../enforcement/overview.md).

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso no [!DNL Experience Platform] IU:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
