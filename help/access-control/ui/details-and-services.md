---
keywords: Experience Platform;página inicial;tópicos populares;perfil de produto
solution: Experience Platform
title: Gerenciar detalhes e serviços adicionais para um Perfil de produto
description: Este documento aborda as etapas necessárias para gerenciar detalhes e serviços adicionais para um perfil de produto no Adobe Admin Console. Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais no menu Configurações do perfil.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Gerenciar detalhes e serviços adicionais para um perfil de produto

Você pode configurar os detalhes de um perfil e o acesso a serviços adicionais no **[!UICONTROL Configurações do perfil]** menu. Para acessar o menu, selecione **[!UICONTROL Configurações]** do **[!UICONTROL Perfil do produto]** página.

![configurações](../images/settings.png)

A variável **[!UICONTROL Editar perfil de produto]** é exibido, iniciando no **[!UICONTROL Editar detalhes do perfil]** guia. Esta guia permite inserir e editar o nome e a descrição do perfil. Você também pode modificar o nome para exibição, bem como as configurações de notificação por email da sua conta.

![edit-product-profile](../images/edit-product-profile.png)

Selecionar **[!UICONTROL Próxima]** para acessar o **[!UICONTROL Habilitar serviços]** página.

A variável **[!UICONTROL Habilitar serviços]** permite modificar o acesso de um perfil a informações adicionais [!DNL Platform] serviços que foram configurados inicialmente quando o perfil foi criado. Dependendo do [!DNL Platform] assinatura, esses serviços podem incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Adobe Real-Time Customer Data Platform] Interface do usuário (somente para Real-Time CDP)
- IU B2B

Clique no botão de alternância no lado direito de um serviço específico para ativá-lo ou desativá-lo. Você também pode selecionar a variável **[!UICONTROL Todos em]** para ativar ou desativar todos os serviços listados.

Quando terminar, selecione **[!UICONTROL Salvar]**.

![enable-services](../images/enable-services.png)

Os clientes com direito ao B2B ou B2P Edition têm acesso à interface do usuário B2B. A interface B2B pode ser provisionada para usuários por meio do [!UICONTROL Ativar menu de serviços]. Selecione a alternância ao lado [!UICONTROL IU B2B] para habilitar o serviço para um perfil de produto específico e selecione **[!UICONTROL Salvar]**.

A alternância da interface do usuário B2B permite que os usuários visualizem fluxos de trabalho B2B em torno do gerenciamento de contas e oportunidades, bem como criem segmentos relacionados a B2B. Para obter mais informações, consulte a documentação em [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)