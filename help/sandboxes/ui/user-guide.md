---
keywords: Experience Platform;página inicial;tópicos populares;guia do usuário de sandbox;guia de sandbox
solution: Experience Platform
title: Guia da interface de usuário da sandbox
description: Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 70bbfd4e2971367c9b7b88bd4bc7985d9e6fbb1e
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 7%

---

# Guia da interface de usuário da sandbox

Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.

## Exibir sandboxes

Na interface do usuário da Platform, selecione **[!UICONTROL Sandboxes]** na navegação à esquerda e selecione **[!UICONTROL Procurar]** para abrir o [!UICONTROL Sandboxes] painel. O painel lista todas as sandboxes disponíveis para sua organização, incluindo seus respectivos tipos (produção ou desenvolvimento).

![view-sandboxes](../images/ui/view-sandboxes.png)

## Alternar entre sandboxes

O indicador da sandbox está localizado no cabeçalho superior da interface do usuário da Platform e exibe o título da sandbox em que você está no momento, sua região e seu tipo.

![sandbox-indicator](../images/ui/sandbox-indicator.png)

Para alternar entre sandboxes, selecione o indicador de sandbox e selecione a sandbox desejada na lista suspensa.

![switcher-interface](../images/ui/switcher-interface.png)

Depois que uma sandbox é selecionada, a tela é atualizada e atualizada para a sandbox selecionada.

![comutado por sandbox](../images/ui/sandbox-switched.png)

## Criar uma nova sandbbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nome da sandbox"
>abstract="O nome da sandbox é o texto usado no back-end para criar uma ID exclusiva para essa sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Título da sandbox"
>abstract="O título da sandbox é o nome de exibição que representará a sandbox em menus e menus suspensos na interface da Experience Platform."

>[!NOTE]
>
>Quando uma nova sandbox é criada, primeiro você deve adicionar essa nova sandbox ao perfil do produto no [Adobe Admin Console](https://adminconsole.adobe.com/) antes de começar a usar a nova sandbox. Consulte a documentação em [gerenciamento de permissões para um perfil de produto](../../access-control/ui/permissions.md) para obter informações sobre como provisionar uma sandbox para um perfil de produto.

Assista ao vídeo a seguir para obter uma visão geral rápida sobre como usar sandboxes no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Para criar uma nova sandbox, selecione **[!UICONTROL Criar sandbox]** no canto superior direito da tela.

![create-sandbox](../images/ui/create-sandbox.png)

A variável **[!UICONTROL Criar sandbox]** é exibida. Se estiver criando uma sandbox de desenvolvimento, selecione **[!UICONTROL Desenvolvimento]** no painel suspenso. Para criar uma nova sandbox de produção, selecione **[!UICONTROL Produção]**.

![sandbox-type](../images/ui/sandbox-type.png)

Após selecionar o tipo, forneça um nome e um título à sandbox. O título deve ser legível e descritivo o suficiente para ser facilmente identificável. O nome da sandbox é um identificador totalmente em minúsculas para uso em chamadas de API e, portanto, deve ser exclusivo e conciso. O nome da sandbox deve começar com uma letra, ter no máximo 256 caracteres e consistir apenas de caracteres alfanuméricos e hifens (-).

Quando terminar, selecione **[!UICONTROL Criar]**.

![sandbox-info](../images/ui/sandbox-info.png)

Quando terminar de criar a sandbox, atualize a página e a nova sandbox aparecerá no **[!UICONTROL Sandboxes]** painel com status &quot;[!UICONTROL Criação]&quot;. As novas sandboxes levam aproximadamente 30 segundos para serem provisionadas pelo sistema, depois disso seu status muda para &quot;[!UICONTROL Ativo]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Redefinir uma sandbox

>[!WARNING]
>
>Veja a seguir uma lista de exceções que podem impedir a redefinição da sandbox de produção padrão ou de uma sandbox de produção criada pelo usuário:
>* A sandbox de produção padrão não pode ser redefinida se o gráfico de identidade hospedado na sandbox também estiver sendo usado pelo Adobe Analytics para o [Análise entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=pt-BR) recurso.
>* A sandbox de produção padrão não pode ser redefinida se o gráfico de identidade hospedado na sandbox também estiver sendo usado pelo Adobe Audience Manager para o [Destinos com base em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=pt-BR).
>* A sandbox de produção padrão não pode ser redefinida se contiver dados para recursos CDA e PBD.
>* Uma sandbox de produção criada pelo usuário usada para compartilhamento de segmento bidirecional com o Adobe Audience Manager ou o Audience Core Service pode ser redefinida após uma mensagem de aviso.
>* Antes de iniciar uma redefinição de sandbox, será necessário excluir suas composições manualmente para garantir que os dados do público-alvo associado sejam limpos corretamente.

### Excluir composições de público

No momento, a composição do público-alvo não está integrada ao recurso de redefinição da sandbox. Portanto, os públicos-alvo precisarão ser excluídos manualmente antes de executar a redefinição da sandbox.

Selecionar **[!UICONTROL Públicos-alvo]** na navegação à esquerda e selecione **[!UICONTROL Composições]**.

![A variável [!UICONTROL Composições] na guia [!UICONTROL Públicos-alvo] espaço de trabalho.](../images/ui/audiences.png)

Em seguida, selecione as reticências (`...`) ao lado do primeiro público-alvo e selecione **[!UICONTROL Excluir]**.

![O menu de público-alvo destacando o [!UICONTROL Excluir] opção.](../images/ui/delete-composition.png)

Uma confirmação de exclusão bem-sucedida é exibida e você retorna para a **[!UICONTROL Composições]** guia.

Repita as etapas acima com todas as suas composições. Isso excluirá todos os públicos-alvo do inventário de público-alvo. Depois que todos os públicos-alvo forem removidos, você poderá continuar redefinindo a sandbox.

### Redefinição de uma sandbox

A redefinição de uma sandbox de produção ou desenvolvimento exclui todos os recursos associados a essa sandbox (esquemas, conjuntos de dados e assim por diante), enquanto mantém o nome da sandbox e as permissões associadas. Essa sandbox &quot;limpa&quot; continua disponível com o mesmo nome para os usuários que têm acesso a ela.

Selecione a sandbox que deseja redefinir na lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Redefinição de sandbox]**.

![redefinir](../images/ui/reset.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Selecionar **[!UICONTROL Continuar]** para continuar.

![redefinir-aviso](../images/ui/reset-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Redefinir]**.

![redefinir-confirmar](../images/ui/reset-confirm.png)

## Excluir uma sandbox

>[!WARNING]
>
>Não é possível excluir a sandbox de produção padrão. No entanto, qualquer sandbox de produção criada pelo usuário usada para compartilhamento de segmento bidirecional com [!DNL Audience Manager] ou [!DNL Audience Core Service] pode ser excluído após uma mensagem de aviso.

Excluir uma sandbox de produção ou desenvolvimento remove permanentemente todos os recursos associados a essa sandbox, incluindo permissões.

Selecione a sandbox que deseja excluir na lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Excluir]**.

![delete](../images/ui/delete.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Selecionar **[!UICONTROL Continuar]** para continuar.

![excluir-aviso](../images/ui/delete-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione  **[!UICONTROL Continuar]**.

![excluir-confirmar](../images/ui/delete-confirm.png)

## Próximas etapas

Este documento demonstrou como gerenciar sandboxes na interface do usuário do Experience Platform. Para obter informações sobre como gerenciar sandboxes usando a API de sandbox, consulte a [guia do desenvolvedor de sandbox](../api/getting-started.md).
