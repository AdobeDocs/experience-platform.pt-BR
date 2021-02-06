---
keywords: Experience Platform;home;popular topics;controle de dados;guia do usuário da política de uso de dados
solution: Experience Platform
title: Gerenciar políticas de uso de dados na interface do usuário
topic: policies
description: O Adobe Experience Platform Data Governance fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar na área de trabalho Políticas na interface do usuário do Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# Gerenciar políticas de uso de dados na interface do usuário

O Adobe Experience Platform [!DNL Data Governance] fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar na área de trabalho **Policies** na interface do usuário [!DNL Experience Platform].

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário ativar essa política manualmente. Consulte a seção sobre [ativar políticas](#enable) para obter etapas sobre como fazer isso na interface do usuário.

## Pré-requisitos

Este guia exige uma compreensão funcional dos seguintes conceitos [!DNL Experience Platform]:

- [[!DNL Data Governance]](../home.md)
- [Políticas de uso de dados](./overview.md)

## Visualização de políticas existentes {#view-policies}

Na interface do usuário [!DNL Experience Platform], selecione **[!UICONTROL Políticas]** para abrir a área de trabalho **[!UICONTROL Políticas]**. Na guia **[!UICONTROL Procurar]**, é possível visualizar uma lista de políticas disponíveis, incluindo rótulos associados, ações de marketing e status.

![](../images/policies/browse-policies.png)

Selecione uma política listada para visualização sua descrição e tipo. Se uma política personalizada for selecionada, serão exibidos controles adicionais para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política personalizada {#create-policy}

Para criar uma nova política personalizada de uso de dados, selecione **[!UICONTROL Criar política]** no canto superior direito da guia **[!UICONTROL Procurar]** na área de trabalho **[!UICONTROL Políticas]**.

![](../images/policies/create-policy-button.png)

O fluxo de trabalho **[!UICONTROL Criar política]** é exibido. Start fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Selecione **[!UICONTROL Next]** quando terminar.

![](../images/policies/add-labels.png)

A etapa **[!UICONTROL Selecionar ações de marketing]** é exibida. Escolha as ações de marketing apropriadas na lista fornecida e selecione **[!UICONTROL Próximo]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OU&quot;. Em outras palavras, a política se aplica se **qualquer** das ações de marketing selecionadas forem executadas.

![](../images/policies/add-marketing-actions.png)

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você reveja os detalhes da nova política antes de criá-la. Quando estiver satisfeito, selecione **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

A guia **[!UICONTROL Procurar]** reaparece, que agora lista a política recém-criada no status &quot;Rascunho&quot;. Para ativar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

## Ativar ou desativar uma política {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário ativar essa política manualmente por meio da API ou da interface do usuário.

Você pode ativar ou desativar as políticas na guia **[!UICONTROL Procurar]** na área de trabalho **[!UICONTROL Políticas]**. Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Ações de marketing de visualização {#view-marketing-actions}

Na área de trabalho **[!UICONTROL Policies]**, selecione a guia **[!UICONTROL Ações de marketing]** para visualização de uma lista de ações de marketing disponíveis definidas pelo Adobe e sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, selecione **[!UICONTROL Criar ação de marketing]** no canto superior direito da guia **[!UICONTROL Ações de marketing]** na área de trabalho **[!UICONTROL Políticas]**.

![](../images/policies/create-marketing-action.png)

A caixa de diálogo **[!UICONTROL Criar ação de marketing]** é exibida. Insira um nome e uma descrição para a ação de marketing e selecione **[!UICONTROL Criar]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada é exibida na guia **[!UICONTROL Ações de marketing]**. Agora você pode usar a ação de marketing ao [criar novas políticas de uso de dados](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente as ações de marketing personalizadas definidas pela sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

Na área de trabalho **[!UICONTROL Policies]**, selecione a guia **[!UICONTROL Ações de marketing]** para visualização de uma lista de ações de marketing disponíveis definidas pelo Adobe e sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, é possível excluí-la selecionando **[!UICONTROL Excluir ação de marketing]**.

>[!NOTE]
>
>A tentativa de excluir uma ação de marketing que está sendo usada por uma política existente fará com que uma mensagem de erro seja exibida, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar políticas de uso de dados na interface do usuário [!DNL Experience Platform]. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o [guia do desenvolvedor](../api/getting-started.md). Para obter informações sobre como aplicar políticas de uso de dados, consulte a [visão geral de aplicação de política](../enforcement/overview.md).

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso na interface do usuário [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)