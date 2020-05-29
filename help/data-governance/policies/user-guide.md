---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do usuário das políticas de uso de dados
topic: policies
translation-type: tm+mt
source-git-commit: af7fa6048fa60392a98975fe6fc36e8302355a05
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 2%

---


# Guia do usuário das políticas de uso de dados

O Adobe Experience Platform Data Governance fornece uma interface de usuário que permite criar e gerenciar políticas de uso de dados. Este documento fornece uma visão geral das ações que você pode executar na área de trabalho _Políticas_ na interface do usuário da plataforma de experiência.

## Pré-requisitos

Este guia exige uma compreensão funcional dos seguintes conceitos da plataforma de experiência:

- [Governança de dados](../home.md)
- [Políticas de uso de dados](./overview.md)

## Políticas de uso de dados de Visualização

Na interface do usuário da plataforma de experiência, clique em **[!UICONTROL Políticas]** para abrir a área de trabalho *[!UICONTROL Políticas]* . Na guia **[!UICONTROL Procurar]** , é possível visualizar uma lista de políticas disponíveis, incluindo seus rótulos, ações de marketing e status associados.

![](../images/policies/browse-policies.png)

Clique em uma política listada para visualização sua descrição e tipo. Se uma política personalizada for selecionada, serão exibidos controles adicionais para editar, excluir ou [ativar/desativar a política](#enable).

![](../images/policies/policy-details.png)

## Criar uma política de uso de dados personalizada

Para criar uma nova política de uso de dados personalizada, clique em **[!UICONTROL Criar política]** no canto superior direito da área de trabalho *Políticas* .

![](../images/policies/create-policy-button.png)

O fluxo de trabalho *[!UICONTROL Criar política]* é exibido. Start fornecendo um nome e uma descrição para a nova política.

![](../images/policies/create-policy-description.png)

Em seguida, selecione os rótulos de uso de dados nos quais a política será baseada. Ao selecionar vários rótulos, você tem a opção de escolher se os dados devem conter todos os rótulos ou apenas um deles para que a política seja aplicada. Clique em **[!UICONTROL Avançar]** ao concluir.

![](../images/policies/add-labels.png)

A etapa *[!UICONTROL Selecionar ações]* de marketing é exibida. Escolha as ações de marketing apropriadas na lista fornecida e clique em **[!UICONTROL Avançar]** para continuar.

>[!NOTE] Ao selecionar várias ações de marketing, a política as interpreta como uma regra &quot;OU&quot;. Em outras palavras, a política se aplica se _qualquer_ uma das ações de marketing selecionadas for executada.

![](../images/policies/add-marketing-actions.png)

A etapa *[!UICONTROL Revisar]* é exibida, permitindo que você analise os detalhes da nova política antes de criá-la. Quando estiver satisfeito, clique em **[!UICONTROL Concluir]** para criar a política.

![](../images/policies/policy-review.png)

A guia *[!UICONTROL Procurar]* reaparece, que agora lista a política recém-criada no status &quot;Rascunho&quot;. Para ativar a política, consulte a próxima seção.

![](../images/policies/created-policy.png)

## Ativar ou desativar uma política de uso de dados {#enable}

É possível ativar ou desativar políticas de uso de dados personalizadas na guia *[!UICONTROL Procurar]* na área de trabalho *[!UICONTROL Políticas]* . Selecione uma política personalizada na lista para exibir seus detalhes à direita. Em *[!UICONTROL Status]*, selecione o botão de alternância para ativar ou desativar a política.

![](../images/policies/enable-policy.png)

## Próximas etapas

Este documento forneceu uma visão geral de como gerenciar as políticas de uso de dados na interface do usuário da plataforma Experience. Para obter etapas sobre como gerenciar políticas usando a DULE Policy API, consulte o guia [do](../api/getting-started.md)desenvolvedor. Para obter informações sobre como aplicar políticas de uso de dados, consulte a visão geral [da aplicação de](../enforcement/overview.md)políticas.

O vídeo a seguir fornece uma demonstração de como trabalhar com políticas de uso na interface do usuário da plataforma de experiência:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)