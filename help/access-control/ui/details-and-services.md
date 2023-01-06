---
keywords: Experience Platform, home, tópicos populares, perfil de produto
solution: Experience Platform
title: Gerenciar detalhes e serviços adicionais para um perfil de produto
description: Este documento aborda as etapas necessárias para gerenciar detalhes e serviços adicionais para um perfil de produto no Adobe Admin Console. Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais no menu Configurações do perfil .
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Gerenciar detalhes e serviços adicionais para um perfil de produto

Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais na **[!UICONTROL Configurações do perfil]** menu. Para acessar o menu, selecione **[!UICONTROL Configurações]** do **[!UICONTROL Perfil de produto]** página.

![configurações](../images/settings.png)

O **[!UICONTROL Editar perfil de produto]** for exibido, começando no **[!UICONTROL Editar detalhes do perfil]** guia . Essa guia permite inserir e editar o nome e a descrição do perfil. Você também pode modificar seu nome de exibição, bem como as configurações de notificação por email para sua conta.

![edit-product-profile](../images/edit-product-profile.png)

Selecionar **[!UICONTROL Próximo]** para acessar o **[!UICONTROL Ativar serviços]** página.

O **[!UICONTROL Ativar serviços]** permite modificar o acesso de um perfil a [!DNL Platform] serviços que foram configurados inicialmente quando o perfil foi criado. Dependendo do [!DNL Platform] por assinatura, esses serviços podem incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Adobe Real-Time Customer Data Platform] Interface do usuário (somente para Real-Time CDP)
- Interface do usuário B2B

Clique no botão de alternância no lado direito de um serviço específico para ativá-lo ou desativá-lo. Também é possível selecionar a variável **[!UICONTROL Tudo em]** caixa de seleção para ativar ou desativar todos os serviços listados.

Quando terminar, selecione **[!UICONTROL Salvar]**.

![enable-services](../images/enable-services.png)

Os clientes autorizados para a B2B ou B2P Edition têm acesso à interface B2B. A interface B2B pode ser provisionada para usuários por meio do [!UICONTROL Ativar menu de serviços]. Selecione a alternância ao lado [!UICONTROL Interface do usuário B2B] para ativar o serviço para um perfil de produto específico e, em seguida, selecione **[!UICONTROL Salvar]**.

A alternância da interface B2B permite que os usuários visualizem workflows B2B ao gerenciar Contas e Oportunidades, bem como criem segmentos relacionados a B2B. Para obter mais informações, consulte a documentação em [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)