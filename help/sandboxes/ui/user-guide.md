---
keywords: Experience Platform, home, tópicos populares, guia do usuário da sandbox, guia da sandbox
solution: Experience Platform
title: Guia da interface do usuário do Sandbox
topic-legacy: user guide
description: Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 2fb972b0ec8d1f679c6ce104a439265b5cc4d535
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# Guia da interface do usuário do Sandbox

Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.

## Exibir sandboxes

Na interface do usuário da plataforma, selecione **[!UICONTROL Sandboxes]** na navegação à esquerda e selecione **[!UICONTROL Procurar]** para abrir o [!UICONTROL Sandboxes] painel. O painel lista todas as sandboxes disponíveis para sua organização, incluindo seus respectivos tipos (produção ou desenvolvimento).

![sandboxes de exibição](../images/ui/view-sandboxes.png)

## Alternar entre sandboxes

O indicador da sandbox está localizado no cabeçalho superior da interface do usuário da plataforma e exibe o título da sandbox em que você está, sua região e seu tipo.

![indicador da caixa de proteção](../images/ui/sandbox-indicator.png)

Para alternar entre sandboxes, selecione o indicador sandbox e selecione a sandbox desejada na lista suspensa.

![interface do alternador](../images/ui/switcher-interface.png)

Depois que uma sandbox é selecionada, a tela é atualizada e atualizada para a sandbox selecionada.

![troca de sandbox](../images/ui/sandbox-switched.png)

## Criar uma nova sandbox

>[!NOTE]
>
>Quando uma nova sandbox é criada, você deve primeiro adicionar essa nova sandbox ao perfil do produto em [Adobe Admin Console](https://adminconsole.adobe.com/) antes de começar a usar a nova sandbox. Consulte a documentação em [gerenciamento de permissões para um perfil de produto](../../access-control/ui/permissions.md) para obter informações sobre como provisionar uma sandbox para um perfil de produto.

Use o vídeo a seguir para obter uma visão geral rápida sobre como usar sandboxes no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para criar uma nova sandbox, selecione **[!UICONTROL Criar sandbox]** no canto superior direito da tela.

![create-sandbox](../images/ui/create-sandbox.png)

O **[!UICONTROL Criar sandbox]** será exibida. Se estiver criando uma sandbox de desenvolvimento, selecione **[!UICONTROL Desenvolvimento]** no painel suspenso. Para criar uma nova sandbox de produção, selecione **[!UICONTROL Produção]**.

![tipo sandbox](../images/ui/sandbox-type.png)

Depois de selecionar o tipo, forneça um nome e um título à sua sandbox. O título destina-se a ser legível por seres humanos e deve ser suficientemente descritivo para ser facilmente identificável. O nome da sandbox é um identificador em letras minúsculas para uso em chamadas de API e, portanto, deve ser exclusivo e conciso. O nome da sandbox deve começar com uma letra, ter no máximo 256 caracteres e consistir apenas em caracteres alfanuméricos e hifens (-).

Quando terminar, selecione **[!UICONTROL Criar]**.

![sandbox-info](../images/ui/sandbox-info.png)

Quando terminar de criar a sandbox, atualize a página e a nova sandbox aparecerá no **[!UICONTROL Sandboxes]** painel com status &quot;[!UICONTROL Criação]&quot;. As novas sandboxes levam aproximadamente 30 segundos para serem provisionadas pelo sistema, após o que o status muda para &quot;[!UICONTROL Ativo]&quot;.

![sandbox nova](../images/ui/new-sandbox.png)

## Redefinir uma sandbox

>[!WARNING]
>
>Esta é uma lista de exceções que podem impedir a redefinição da sandbox de produção padrão ou de uma sandbox de produção criada pelo usuário: <ul><li>A sandbox de produção padrão não poderá ser redefinida se o gráfico de identidade hospedado na sandbox também estiver sendo usado pela Adobe Analytics para a variável [Análise entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=pt-BR) recurso.</li><li>A sandbox de produção padrão não poderá ser redefinida se o gráfico de identidade hospedado na sandbox também estiver sendo usado pela Adobe Audience Manager para a variável [Destinos com base em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).</li><li>A sandbox de produção padrão não pode ser redefinida se contiver dados para os recursos CDA e PBD.</li><li>Uma sandbox de produção criada pelo usuário e usada para o compartilhamento bidirecional de segmentos com o Adobe Audience Manager ou o Audience Core Service pode ser redefinida após uma mensagem de aviso.</li></ul>

A redefinição de uma sandbox de produção ou desenvolvimento exclui todos os recursos associados a ela (esquemas, conjuntos de dados e assim por diante), mantendo o nome da sandbox e as permissões associadas. Essa sandbox &quot;limpa&quot; continua disponível com o mesmo nome para usuários que têm acesso a ela.

Selecione a sandbox que deseja redefinir na lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Redefinição de sandbox]**.

![redefinir](../images/ui/reset.png)

Uma caixa de diálogo é exibida, solicitando que você confirme sua escolha. Selecionar **[!UICONTROL Continuar]** para continuar.

![reset-warning](../images/ui/reset-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Redefinir]**.

![redefinir confirmação](../images/ui/reset-confirm.png)

## Excluir uma sandbox

>[!WARNING]
>
>Não é possível excluir a sandbox de produção padrão. No entanto, qualquer sandbox de produção criada pelo usuário que seja usada para o compartilhamento de segmentos bidirecionais com a [!DNL Audience Manager] ou [!DNL Audience Core Service] pode ser excluída após uma mensagem de aviso.

A exclusão de uma sandbox de produção ou desenvolvimento remove permanentemente todos os recursos associados a essa sandbox, incluindo permissões.

Selecione a sandbox que deseja excluir da lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Excluir]**.

![excluir](../images/ui/delete.png)

Uma caixa de diálogo é exibida, solicitando que você confirme sua escolha. Selecionar **[!UICONTROL Continuar]** para continuar.

![aviso de exclusão](../images/ui/delete-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione  **[!UICONTROL Continuar]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Próximas etapas

Este documento demonstrou como gerenciar sandboxes na interface do usuário do Experience Platform. Para obter informações sobre como gerenciar sandboxes usando a API Sandbox, consulte o [guia do desenvolvedor do sandbox](../api/getting-started.md).
