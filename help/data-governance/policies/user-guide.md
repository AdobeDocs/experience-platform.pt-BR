---
keywords: Experience Platform, home, tópicos populares, governança de dados, guia do usuário da política de uso de dados
solution: Experience Platform
title: Gerenciar políticas de uso de dados na interface do usuário
topic-legacy: policies
description: A Governança de dados do Adobe Experience Platform fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que podem ser executadas no espaço de trabalho Políticas na interface do usuário do Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# Gerenciar políticas de uso de dados na interface do usuário

O Adobe Experience Platform [!DNL Data Governance] fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que podem ser executadas no espaço de trabalho **Policies** na interface do usuário [!DNL Experience Platform].

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, é necessário habilitar manualmente essa política. Consulte a seção [ativando políticas](#enable) para obter etapas sobre como fazer isso na interface do usuário.

## Pré-requisitos

Este guia requer uma compreensão funcional dos seguintes conceitos [!DNL Experience Platform]:

- [[!DNL Data Governance]](../home.md)
- [Políticas de uso de dados](./overview.md)

## Exibir políticas existentes {#view-policies}

Na interface [!DNL Experience Platform], selecione **[!UICONTROL Policies]** para abrir o espaço de trabalho **[!UICONTROL Policies]**. Na guia **[!UICONTROL Browse]**, é possível ver uma lista de políticas disponíveis, incluindo rótulos, ações de marketing e status associados.

![](../images/policies/browse-policies.png)

Selecione uma política listada para exibir sua descrição e tipo. Se uma política personalizada for selecionada, controles adicionais serão exibidos para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política personalizada {#create-policy}

Para criar uma nova política de uso de dados personalizada, selecione **[!UICONTROL Create policy]** no canto superior direito da guia **[!UICONTROL Browse]** no espaço de trabalho **[!UICONTROL Policies]**.

![](../images/policies/create-policy-button.png)

O workflow **[!UICONTROL Create policy]** é exibido. Comece fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Selecione **[!UICONTROL Next]** quando terminar.

![](../images/policies/add-labels.png)

A etapa **[!UICONTROL Select marketing actions]** é exibida. Escolha as ações de marketing apropriadas na lista fornecida e selecione **[!UICONTROL Next]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OU&quot;. Em outras palavras, a política se aplica se **any** das ações de marketing selecionadas for executado.

![](../images/policies/add-marketing-actions.png)

A etapa **[!UICONTROL Review]** é exibida, permitindo que você revise os detalhes da nova política antes de criá-la. Quando estiver satisfeito, selecione **[!UICONTROL Finish]** para criar a política.

![](../images/policies/policy-review.png)

A guia **[!UICONTROL Browse]** é exibida novamente, listando agora a política recém-criada no status &quot;Rascunho&quot;. Para ativar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

## Ativar ou desativar uma política {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, você deve habilitar manualmente essa política por meio da API ou da interface do usuário.

Você pode ativar ou desativar as políticas na guia **[!UICONTROL Browse]** no espaço de trabalho **[!UICONTROL Policies]**. Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Exibir ações de marketing {#view-marketing-actions}

No espaço de trabalho **[!UICONTROL Policies]**, selecione a guia **[!UICONTROL Marketing actions]** para visualizar uma lista de ações de marketing disponíveis definidas pelo Adobe e sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, selecione **[!UICONTROL Create marketing action]** no canto superior direito da guia **[!UICONTROL Marketing actions]** no espaço de trabalho **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

A caixa de diálogo **[!UICONTROL Create marketing action]** é exibida. Insira um nome e uma descrição para a ação de marketing e selecione **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada é exibida na guia **[!UICONTROL Marketing actions]**. Agora você pode usar a ação de marketing ao [criar novas políticas de uso de dados](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente as ações de marketing personalizadas definidas pela sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

No espaço de trabalho **[!UICONTROL Policies]**, selecione a guia **[!UICONTROL Marketing actions]** para visualizar uma lista de ações de marketing disponíveis definidas pelo Adobe e sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, é possível excluí-la selecionando **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>A tentativa de excluir uma ação de marketing que está sendo usada por uma política existente causará a exibição de uma mensagem de erro, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar políticas de uso de dados na interface do usuário [!DNL Experience Platform]. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o [guia do desenvolvedor](../api/getting-started.md). Para obter informações sobre como aplicar políticas de uso de dados, consulte a [visão geral de aplicação de política](../enforcement/overview.md).

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso na interface do usuário [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
