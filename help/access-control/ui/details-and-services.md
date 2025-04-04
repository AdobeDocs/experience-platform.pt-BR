---
keywords: Experience Platform;página inicial;tópicos populares;perfil de produto
solution: Experience Platform
title: Gerenciar detalhes e serviços adicionais para um Perfil de produto
description: Este documento aborda as etapas necessárias para gerenciar detalhes e serviços adicionais para um perfil de produto no Adobe Admin Console. Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais no menu Configurações do perfil.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Gerenciar detalhes e serviços adicionais para um perfil de produto

Você pode configurar os detalhes de um perfil e acessar serviços adicionais no menu **[!UICONTROL Configurações de perfil]**. Para acessar o menu, selecione **[!UICONTROL Configurações]** na página **[!UICONTROL Perfil de Produto]**.

![configurações](../images/settings.png)

O menu **[!UICONTROL Editar perfil de produto]** é exibido, iniciando na guia **[!UICONTROL Editar detalhes do perfil]**. Esta guia permite inserir e editar o nome e a descrição do perfil. Você também pode modificar o nome para exibição, bem como as configurações de notificação por email da sua conta.

![editar-perfil-produto](../images/edit-product-profile.png)

Selecione **[!UICONTROL Avançar]** para acessar a página **[!UICONTROL Habilitar serviços]**.

O menu **[!UICONTROL Habilitar serviços]** permite modificar o acesso de um perfil a serviços [!DNL Experience Platform] adicionais que foram configurados inicialmente quando o perfil foi criado. Dependendo da sua assinatura do [!DNL Experience Platform], esses serviços podem incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- Interface do usuário do [!DNL Adobe Real-Time Customer Data Platform] (somente para Real-Time CDP)
- IU B2B

Clique no botão de alternância no lado direito de um serviço específico para ativá-lo ou desativá-lo. Você também pode marcar a caixa de seleção **[!UICONTROL Tudo em]** para habilitar ou desabilitar todos os serviços listados.

Quando terminar, selecione **[!UICONTROL Salvar]**.

![habilitar-serviços](../images/enable-services.png)

Os clientes com direito ao B2B ou B2P Edition têm acesso à interface do usuário B2B. A interface B2B pode ser provisionada para usuários por meio do [!UICONTROL menu Habilitar serviços]. Selecione a alternância ao lado da [!UICONTROL Interface B2B] para habilitar o serviço para um perfil de produto específico e selecione **[!UICONTROL Salvar]**.

A alternância da interface do usuário B2B permite que os usuários visualizem fluxos de trabalho B2B em torno do gerenciamento de contas e oportunidades, bem como criem segmentos relacionados a B2B. Para obter mais informações, consulte a documentação sobre [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![habilitar-b2b](../images/enable-b2b.png)