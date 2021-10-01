---
keywords: Experience Platform, home, tópicos populares, perfil de produto
solution: Experience Platform
title: Gerenciar detalhes e serviços adicionais para um perfil de produto
topic-legacy: user guide
description: Este documento aborda as etapas necessárias para gerenciar detalhes e serviços adicionais para um perfil de produto no Adobe Admin Console. Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais no menu Configurações do perfil .
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 2844ffd7270ffcc2fba4da08dda1aea238cf6c9f
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Gerenciar detalhes e serviços adicionais para um perfil de produto

Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais no menu **[!UICONTROL Configurações do perfil]**. Para acessar o menu, selecione **[!UICONTROL Settings]** na página **[!UICONTROL Product Profile]**.

![configurações](../images/settings.png)

O menu **[!UICONTROL Editar perfil de produto]** é exibido, começando na guia **[!UICONTROL Editar detalhes do perfil]**. Essa guia permite inserir e editar o nome e a descrição do perfil. Você também pode modificar seu nome de exibição, bem como as configurações de notificação por email para sua conta.

![edit-product-profile](../images/edit-product-profile.png)

Selecione **[!UICONTROL Next]** para acessar a página **[!UICONTROL Ativar serviços]**.

O menu **[!UICONTROL Ativar serviços]** permite modificar o acesso de um perfil a serviços [!DNL Platform] adicionais que foram configurados inicialmente quando o perfil foi criado. Dependendo da sua assinatura [!DNL Platform], esses serviços podem incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Real-Time Customer Data Platform] Interface do usuário (somente para CDP em tempo real)
- Interface do usuário B2B

Clique no botão de alternância no lado direito de um serviço específico para ativá-lo ou desativá-lo. Você também pode marcar a caixa de seleção **[!UICONTROL Todos em]** para ativar ou desativar todos os serviços listados.

Quando terminar, selecione **[!UICONTROL Save]**.

![enable-services](../images/enable-services.png)

Os clientes autorizados para a B2B ou B2P Edition têm acesso à interface B2B. A interface B2B pode ser provisionada para usuários por meio do [!UICONTROL Ativar menu de serviços]. Selecione a alternância ao lado de [!UICONTROL B2B UI] para habilitar o serviço para um perfil de produto específico e selecione **[!UICONTROL Salvar]**.

A alternância da interface B2B permite que os usuários visualizem workflows B2B ao gerenciar Contas e Oportunidades, bem como criem segmentos relacionados a B2B. Para obter mais informações, consulte a documentação em [[!DNL Real-time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)