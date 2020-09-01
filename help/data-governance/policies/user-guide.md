---
keywords: Experience Platform;home;popular topics;data governance;data usage policy user guide
solution: Experience Platform
title: Guia do usuário das políticas de uso de dados
topic: policies
description: O Adobe Experience Platform Data Governance fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar na área de trabalho Políticas na interface do usuário do Experience Platform.
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---


# Guia do usuário das políticas de uso de dados

A Adobe Experience Platform [!DNL Data Governance] fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar na área de trabalho _Políticas_ na interface do [!DNL Experience Platform] usuário.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário ativar essa política manualmente. Consulte a seção sobre como [ativar políticas](#enable) para obter etapas sobre como fazer isso na interface do usuário.

## Pré-requisitos

Este guia exige um entendimento prático dos seguintes [!DNL Experience Platform] conceitos:

- [[!DNL Data Governance]](../home.md)
- [Políticas de uso de dados](./overview.md)

## Políticas de uso de dados de visualização {#view-policies}

Na [!DNL Experience Platform] interface do usuário, clique em **[!UICONTROL Políticas]** para abrir a área de trabalho **[!UICONTROL Políticas]** . Na guia **[!UICONTROL Procurar]** , é possível visualizar uma lista de políticas disponíveis, incluindo seus rótulos, ações de marketing e status associados.

![](../images/policies/browse-policies.png)

Clique em uma política listada para visualização sua descrição e tipo. Se uma política personalizada for selecionada, serão exibidos controles adicionais para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política de uso de dados personalizada {#create-policy}

Para criar uma nova política de uso de dados personalizada, clique em **[!UICONTROL Criar política]** no canto superior direito da guia **[!UICONTROL Procurar]** na área de trabalho **[!UICONTROL Políticas]** .

![](../images/policies/create-policy-button.png)

O fluxo de trabalho **[!UICONTROL Criar política]** é exibido. Start fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Clique em **[!UICONTROL Avançar]** ao concluir.

![](../images/policies/add-labels.png)

A etapa **[!UICONTROL Selecionar ações]** de marketing é exibida. Escolha as ações de marketing apropriadas na lista fornecida e clique em **[!UICONTROL Avançar]** para continuar.

>[!NOTE]
>
>Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OU&quot;. Em outras palavras, a política se aplica se _qualquer_ uma das ações de marketing selecionadas for executada.

![](../images/policies/add-marketing-actions.png)

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você analise os detalhes da nova política antes de criá-la. Quando estiver satisfeito, clique em **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

A guia **[!UICONTROL Procurar]** reaparece, que agora lista a política recém-criada no status &quot;Rascunho&quot;. Para ativar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

## Ativar ou desativar uma política de uso de dados {#enable}

Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário ativar essa política manualmente por meio da API ou da interface do usuário.

Você pode ativar ou desativar as políticas na guia **[!UICONTROL Procurar]** na área de trabalho **[!UICONTROL Políticas]** . Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em **[!UICONTROL Status]**, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Ações de marketing de visualização {#view-marketing-actions}

Na área de trabalho **[!UICONTROL Políticas]** , selecione a guia Ações **[!UICONTROL de]** marketing para visualização de uma lista de ações de marketing disponíveis definidas pelo Adobe e sua própria organização.

![](../images/policies/marketing-actions.png)

## Criar uma ação de marketing {#create-marketing-action}

Para criar uma nova ação de marketing personalizada, clique em **[!UICONTROL Criar ação]** de marketing no canto superior direito da guia Ações **[!UICONTROL de]** marketing na área de trabalho **[!UICONTROL Políticas]** .

![](../images/policies/create-marketing-action.png)

A caixa de diálogo **[!UICONTROL Criar ação]** de marketing é exibida. Insira um nome e uma descrição para a ação de marketing e clique em **[!UICONTROL Criar]**.

![](../images/policies/create-marketing-action-details.png)

A ação recém-criada é exibida na guia Ações **[!UICONTROL de]** marketing. Agora você pode usar a ação de marketing ao [criar novas políticas](#create-policy)de uso de dados.

![](../images/policies/created-marketing-action.png)

## Editar ou excluir uma ação de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Somente as ações de marketing personalizadas definidas pela sua organização podem ser editadas. As ações de marketing definidas pelo Adobe não podem ser alteradas ou excluídas.

Na área de trabalho **[!UICONTROL Políticas]** , selecione a guia Ações **[!UICONTROL de]** marketing para visualização de uma lista de ações de marketing disponíveis definidas pelo Adobe e sua própria organização. Selecione uma ação de marketing personalizada na lista e, em seguida, use os campos fornecidos na seção à direita para editar os detalhes da ação de marketing.

![](../images/policies/edit-marketing-action.png)

Se a ação de marketing não estiver sendo usada por nenhuma política de uso existente, você poderá excluí-la clicando em **[!UICONTROL Excluir ação]** de marketing.

>[!NOTE]
>
>A tentativa de excluir uma ação de marketing que está sendo usada por uma política existente fará com que uma mensagem de erro seja exibida, indicando que a tentativa de exclusão falhou.

![](../images/policies/delete-marketing-action.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar políticas de uso de dados na [!DNL Experience Platform] interface do usuário. Para obter etapas sobre como gerenciar políticas usando o [!DNL Policy Service API], consulte o guia [do](../api/getting-started.md)desenvolvedor. Para obter informações sobre como aplicar políticas de uso de dados, consulte a visão geral [da aplicação de](../enforcement/overview.md)políticas.

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso na [!DNL Experience Platform] interface do usuário:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)