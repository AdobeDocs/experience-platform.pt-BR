---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: Guia do usuário do Sandbox
topic: user guide
description: Este documento fornece etapas sobre como executar várias operações relacionadas a caixas de proteção na interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: fb60e11b9502c31e654d3fbe5dc240ace9429332
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Guia do usuário do Sandbox

Este documento fornece etapas sobre como executar várias operações relacionadas a caixas de proteção na interface do usuário do Adobe Experience Platform.

## Caixas de proteção de visualização

Na interface do usuário do Experience Platform, clique em **[!UICONTROL Caixas]** de proteção na navegação esquerda para abrir o painel **[!UICONTROL Caixas de proteção]** . O painel lista todas as caixas de proteção disponíveis para sua organização, incluindo o tipo e o estado da caixa de proteção (produção ou desenvolvimento) (ativo, criação, excluído ou com falha).

![](../images/ui/sandboxes-tab.png)

## Alternar entre caixas de proteção

O controle do alternador **de** sandbox na parte superior esquerda da tela exibe a caixa de proteção ativa no momento.

![](../images/ui/sandbox-selector.png)

Para alternar entre caixas de proteção, clique no alternador da caixa de proteção e selecione a caixa de proteção desejada na lista suspensa.

![](../images/ui/switch-sandbox.png)

Depois que uma caixa de proteção é selecionada, a tela é atualizada com a caixa de proteção selecionada e agora aparece no alternador da caixa de proteção.

![](../images/ui/sandbox-switched.png)

## Criar uma nova caixa de proteção

Use o vídeo a seguir para obter uma visão geral rápida sobre como usar caixas de proteção no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para criar uma nova caixa de proteção na interface do usuário, clique em **[!UICONTROL Caixas de proteção]** na navegação esquerda e, em seguida, clique em **[!UICONTROL Criar caixa de proteção]**.

![](../images/ui/create-sandbox-button.png)

A caixa de diálogo **[!UICONTROL Criar caixa de proteção]** é exibida, solicitando que você forneça um título de exibição e um nome para a caixa de proteção. O título **de** exibição deve ser legível por humanos e deve ser suficientemente descritivo para ser facilmente identificável. O **[!UICONTROL Nome]** da caixa de proteção é um identificador em letras minúsculas para uso em chamadas de API e, portanto, deve ser exclusivo e conciso.

When finished, click **[!UICONTROL Create]**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>Como você está restrito à criação de tipos de caixa de proteção que não sejam de produção, a opção de **[!UICONTROL tipo]** está bloqueada em &quot;Não-produção&quot; e não pode ser manipulada.

Quando terminar de criar a caixa de proteção, atualize a página e a nova caixa de proteção será exibida no painel **[!UICONTROL Sandboxes]** com um status de &quot;[!UICONTROL Criação]&quot;. As novas caixas de proteção levam aproximadamente 15 minutos para serem provisionadas pelo sistema, após o que seu status muda para &quot;[!UICONTROL Ativo]&quot;.

![](../images/ui/sandbox-created.png)

## Redefinir uma caixa de proteção

>[!NOTE]
>
>Essa funcionalidade só está disponível para caixas de proteção que não sejam de produção. As caixas de proteção de produção não podem ser redefinidas.

A redefinição de uma caixa de proteção que não seja de produção exclui todos os recursos associados a essa caixa de proteção (schemas, conjuntos de dados etc.), mantendo o nome da caixa de proteção e as permissões associadas. Essa caixa de proteção &quot;limpa&quot; continua disponível com o mesmo nome para usuários que têm acesso a ela.

Para redefinir uma caixa de proteção na interface do usuário, clique em **[!UICONTROL Caixas de proteção]** no navegador esquerdo e clique na caixa de proteção que deseja redefinir. Na caixa de diálogo exibida no lado direito da tela, clique em **[!UICONTROL Redefinir caixa de proteção]**.

![](../images/ui/reset-sandbox-button.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Click **[!UICONTROL Reset]** to continue.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

Uma mensagem de confirmação é exibida e o estado da caixa de proteção muda para &quot;[!UICONTROL Redefinindo]&quot;. Depois de provisionado pelo sistema, seu estado será atualizado para &quot;[!UICONTROL Ativo]&quot; ou &quot;[!UICONTROL Falha]&quot;.

![](../images/ui/sandbox-resetting.png)

## Excluir uma caixa de proteção

>[!NOTE]
>
>Essa funcionalidade só está disponível para caixas de proteção que não sejam de produção. As caixas de proteção de produção não podem ser excluídas.

A exclusão de uma caixa de proteção que não seja de produção remove permanentemente todos os recursos associados a essa caixa de proteção, incluindo permissões.

Para excluir uma caixa de proteção na interface do usuário, clique em **[!UICONTROL Caixas de proteção]** no navegador esquerdo e clique na caixa de proteção que deseja excluir. Na caixa de diálogo exibida no lado direito da tela, clique em **[!UICONTROL Excluir caixa de proteção]**.

![](../images/ui/delete-sandbox-button.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Click **[!UICONTROL Delete]** to continue.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Uma mensagem de confirmação é exibida e a caixa de proteção é removida da área de trabalho **[!UICONTROL Caixas de proteção]** .

## Próximas etapas

Este documento demonstrou como gerenciar caixas de proteção na interface do usuário do Experience Platform. Para obter informações sobre como gerenciar caixas de proteção usando a API Sandbox, consulte o guia [do desenvolvedor da](../api/getting-started.md)caixa de proteção.