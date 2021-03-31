---
keywords: Experience Platform, home, tópicos populares, guia do usuário da sandbox, guia da sandbox
solution: Experience Platform
title: Guia da interface do usuário do Sandbox
topic: Guia do usuário
description: Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Guia da interface do usuário do Sandbox

Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.

## Exibir sandboxes

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Sandboxes]** na navegação à esquerda para abrir o painel **[!UICONTROL Sandboxes]**. O painel lista todas as sandboxes disponíveis para sua organização, incluindo o tipo de sandbox (produção ou desenvolvimento) e o estado (ativo, criação, excluído ou com falha).

![](../images/ui/view-sandboxes.png)

## Alternar entre sandboxes

O controle **sandbox switcher** na parte superior esquerda da tela exibe a sandbox atualmente ativa.

![](../images/ui/sandbox-switcher.png)

Para alternar entre sandboxes, selecione o alternador de sandbox e selecione a sandbox desejada na lista suspensa.

![](../images/ui/switcher-menu.png)

Depois que uma sandbox é selecionada, a tela é atualizada com a sandbox selecionada e agora aparece no alternador de sandbox.

![](../images/ui/switched.png)

## Procurar uma sandbox

Você pode navegar pela lista de sandboxes disponíveis usando a função de pesquisa do menu sandbox switcher. Digite o nome da sandbox que deseja acessar para filtrar por meio de todas as sandboxes disponíveis para a organização.

![](../images/ui/sandbox-search.png)

## Criar uma nova sandbox

>[!NOTE]
>
>O recurso Várias sandboxes de produção está na versão beta.

Use o vídeo a seguir para obter uma visão geral rápida sobre como usar sandboxes no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para criar uma nova sandbox, selecione o botão **[!UICONTROL Create Sandbox]** no lado superior direito da tela.

![](../images/ui/create-sandbox.png)

A caixa de diálogo **[!UICONTROL Create Sandbox]** é exibida, solicitando que você forneça um tipo, um título e um nome para a sandbox. Se estiver criando uma sandbox de desenvolvimento, selecione **[!UICONTROL Development]** no painel suspenso exibido. Se estiver criando uma sandbox de produção, selecione **[!UICONTROL Production]**.

O título destina-se a ser legível por seres humanos e deve ser suficientemente descritivo para ser facilmente identificável. O nome da sandbox é um identificador em letras minúsculas para uso em chamadas de API e, portanto, deve ser exclusivo e conciso. O nome da sandbox deve consistir apenas em caracteres alfanuméricos e hífens (`-`), deve começar com uma letra e tem no máximo 256 caracteres.

Quando terminar, selecione **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

Quando terminar de criar a sandbox, atualize a página e a nova sandbox aparecerá no painel **[!UICONTROL Sandboxes]** com o status &quot;[!UICONTROL Creating]&quot;. As novas sandboxes levam aproximadamente 15 minutos para serem provisionadas pelo sistema, depois o status muda para &quot;[!UICONTROL Active]&quot;.

## Redefinir uma sandbox

>[!NOTE]
>
>É possível redefinir as sandboxes de produção ou desenvolvimento na organização, exceto a sandbox de produção padrão.

A redefinição de uma sandbox de produção ou desenvolvimento exclui todos os recursos associados a ela (esquemas, conjuntos de dados e assim por diante), mantendo o nome da sandbox e as permissões associadas. Essa sandbox &quot;limpa&quot; continua disponível com o mesmo nome para usuários que têm acesso a ela.

Selecione a sandbox que deseja redefinir na lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Sandbox reset]**.

![](../images/ui/reset-sandbox.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Selecione **[!UICONTROL Continue]** para continuar.

![](../images/ui/reset-confirm.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Reset]**

![](../images/ui/reset-final-confirm.png)

## Excluir uma sandbox

>[!NOTE]
>
>É possível excluir sandboxes de produção ou desenvolvimento na organização, exceto a sandbox de produção padrão.

A exclusão de uma sandbox de produção ou desenvolvimento remove permanentemente todos os recursos associados a essa sandbox, incluindo permissões.

Selecione a sandbox que deseja excluir da lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Delete]**.

![](../images/ui/delete-sandbox.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Selecione **[!UICONTROL Continue]** para continuar.

![](../images/ui/delete-confirm.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Delete]**

![](../images/ui/delete-final-confirm.png)

## Próximas etapas

Este documento demonstrou como gerenciar sandboxes na interface do usuário do Experience Platform. Para obter informações sobre como gerenciar sandboxes usando a API Sandbox, consulte o [guia do desenvolvedor sandbox](../api/getting-started.md).