---
keywords: Experience Platform, home, tópicos populares, guia do usuário da sandbox, guia da sandbox
solution: Experience Platform
title: Guia da interface do usuário do Sandbox
topic-legacy: user guide
description: Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: a43dd851a5c7ec722e792a0f43d1bb42777f0c15
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---

# Guia da interface do usuário do Sandbox

Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.

## Exibir sandboxes

Na interface do usuário da plataforma, selecione **[!UICONTROL Sandboxes]** no painel de navegação esquerdo para abrir o painel [!UICONTROL Sandboxes]. O painel lista todas as sandboxes disponíveis para sua organização, incluindo o tipo de sandbox (produção ou desenvolvimento) e o estado (ativo, criação, excluído ou com falha).

![](../images/ui/view-sandboxes.png)

## Alternar entre sandboxes

O controle **sandbox switcher** na parte superior esquerda da tela exibe a sandbox atualmente ativa.

![](../images/ui/sandbox-switcher.png)

Para alternar entre sandboxes, selecione o alternador de sandbox e selecione a sandbox desejada na lista suspensa.

![](../images/ui/switcher-menu.png)

Depois que uma sandbox é selecionada, a tela é atualizada com a sandbox selecionada e agora aparece no alternador de sandbox.

![](../images/ui/switched.png)

## Pesquisar por uma sandbox

Você pode navegar pela lista de sandboxes disponíveis usando a função de pesquisa do menu sandbox switcher. Digite o nome da sandbox que deseja acessar para filtrar por meio de todas as sandboxes disponíveis para a organização.

![](../images/ui/sandbox-search.png)

## Criar uma nova sandbox

>[!NOTE]
>
>Quando uma nova sandbox é criada, você deve primeiro adicionar essa nova sandbox ao perfil do produto em [Adobe Admin Console](https://adminconsole.adobe.com/) antes de começar a usar a nova sandbox. Consulte a documentação sobre [gerenciamento de permissões para um perfil de produto](../../access-control/ui/permissions.md) para obter informações sobre como provisionar uma sandbox para um perfil de produto.

Use o vídeo a seguir para obter uma visão geral rápida sobre como usar sandboxes no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para criar uma nova sandbox, selecione **[!UICONTROL Criar sandbox]** no canto superior direito da tela.

![criar](../images/ui/create.png)

A caixa de diálogo **[!UICONTROL Criar sandbox]** é exibida. Se estiver criando uma sandbox de desenvolvimento, selecione **[!UICONTROL Desenvolvimento]** no painel suspenso. Para criar uma nova sandbox de produção, selecione **[!UICONTROL Produção]**.

![type](../images/ui/type.png)

Depois de selecionar o tipo, forneça um nome e um título à sua sandbox. O título destina-se a ser legível por seres humanos e deve ser suficientemente descritivo para ser facilmente identificável. O nome da sandbox é um identificador em letras minúsculas para uso em chamadas de API e, portanto, deve ser exclusivo e conciso. O nome da sandbox deve começar com uma letra, ter no máximo 256 caracteres e consistir apenas em caracteres alfanuméricos e hifens (-).

Quando terminar, selecione **[!UICONTROL Criar]**.

![informações](../images/ui/info.png)

Quando terminar de criar a sandbox, atualize a página e a nova sandbox aparecerá no painel **[!UICONTROL Sandboxes]** com o status &quot;[!UICONTROL Criação]&quot;. As novas sandboxes levam aproximadamente 30 segundos para serem provisionadas pelo sistema, depois disso seu status muda para &quot;[!UICONTROL Ative]&quot;.

## Redefinir uma sandbox

>[!IMPORTANT]
>
>A sandbox de produção padrão não poderá ser redefinida se o gráfico de identidade hospedado nela também estiver sendo usado pelo Adobe Analytics para o recurso [Análise entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=pt-BR) ou se o gráfico de identidade hospedado nele também estiver sendo usado pelo Adobe Audience Manager para o recurso [Destinos baseados em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).

A redefinição de uma sandbox de produção ou desenvolvimento exclui todos os recursos associados a ela (esquemas, conjuntos de dados e assim por diante), mantendo o nome da sandbox e as permissões associadas. Essa sandbox &quot;limpa&quot; continua disponível com o mesmo nome para usuários que têm acesso a ela.

Selecione a sandbox que deseja redefinir na lista de sandboxes. No painel de navegação à direita exibido, selecione **[!UICONTROL Sandbox reset]**.

![redefinir](../images/ui/reset.png)

Uma caixa de diálogo é exibida, solicitando que você confirme sua escolha. Selecione **[!UICONTROL Continuar]** para prosseguir.

![reset-warning](../images/ui/reset-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Reset]**

![redefinir confirmação](../images/ui/reset-confirm.png)

Após alguns instantes, uma caixa de confirmação aparecerá na parte inferior da tela para confirmar uma redefinição bem-sucedida.

![success](../images/ui/success.png)

### Avisos

Uma sandbox de produção padrão que contém dados CDA não pode ser redefinida e retorna o seguinte aviso.

![cda](../images/ui/cda.png)

Uma sandbox de produção padrão que contém dados PBD também não pode ser redefinida e retorna o seguinte aviso.

![pbd](../images/ui/pbd.png)

Uma sandbox de produção padrão que contém dados para CDA e PBD também não pode ser redefinida e retorna o seguinte aviso.

![both](../images/ui/both.png)

Você pode redefinir uma sandbox de produção que é usada para o compartilhamento de segmentos bidirecionais com [!DNL Audience Manager] ou [!DNL Audience Core Service]. Selecione [!UICONTROL Continuar] para prosseguir com a redefinição.

![both](../images/ui/seg.png)

## Excluir uma sandbox

>[!IMPORTANT]
>
>A sandbox de produção padrão não pode ser excluída.

A exclusão de uma sandbox de produção ou desenvolvimento remove permanentemente todos os recursos associados a essa sandbox, incluindo permissões.

Selecione a sandbox que deseja excluir da lista de sandboxes. No painel de navegação à direita exibido, selecione **[!UICONTROL Delete]**.

![excluir](../images/ui/delete.png)

Uma caixa de diálogo é exibida, solicitando que você confirme sua escolha. Selecione **[!UICONTROL Continuar]** para prosseguir.

![aviso de exclusão](../images/ui/delete-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Continuar]**

![delete-confirm](../images/ui/delete-confirm.png)

Uma sandbox de produção criada pelo usuário e usada para o compartilhamento de segmentos bidirecionais com [!DNL Audience Manager] ou [!DNL Audience Core Service] ainda pode ser excluída após o seguinte aviso.

![seg](../images/ui/delete-seg.png)

## Próximas etapas

Este documento demonstrou como gerenciar sandboxes na interface do usuário do Experience Platform. Para obter informações sobre como gerenciar sandboxes usando a API Sandbox, consulte o [guia do desenvolvedor sandbox](../api/getting-started.md).
