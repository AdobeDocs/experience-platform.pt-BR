---
keywords: Experience Platform;página inicial;tópicos populares;guia do usuário de sandbox;guia de sandbox
solution: Experience Platform
title: Guia da interface de usuário da sandbox
description: Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 4%

---

# Guia da interface de usuário da sandbox

Este documento fornece etapas sobre como executar várias operações relacionadas a sandboxes na interface do usuário do Adobe Experience Platform.

## Exibir sandboxes

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Sandboxes]** na navegação à esquerda e selecione a guia **[!UICONTROL Browse]** para abrir o painel [!UICONTROL Sandboxes]. O painel lista todas as sandboxes disponíveis para sua organização, incluindo seus respectivos tipos (produção ou desenvolvimento).

![O painel de sandboxes com a guia procurar selecionada, que exibe uma lista de sandboxes disponíveis.](../images/ui/view-sandboxes.png)

## Alternar entre sandboxes

O indicador da sandbox está localizado no cabeçalho superior da interface do usuário do Experience Platform e exibe o título da sandbox em que você está no momento, sua região e seu tipo.

![O painel de sandboxes com o indicador de sandbox realçado.](../images/ui/sandbox-indicator.png)

Para alternar entre sandboxes, selecione o indicador de sandbox e selecione a sandbox desejada na lista suspensa. Como alternativa, procure a sandbox desejada usando o recurso de pesquisa no menu suspenso.

![O menu suspenso do indicador de sandbox é exibido, mostrando uma lista de sandboxes às quais você tem acesso.](../images/ui/switcher-interface.png)

Depois que uma sandbox é selecionada, a tela é atualizada e atualizada para a sandbox selecionada.

![O painel de sandbox com o indicador de sandbox alterado realçado.](../images/ui/sandbox-switched.png)

## Criar uma nova sandbbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nome da sandbox"
>abstract="O nome da sandbox é o texto usado no back-end para criar uma ID exclusiva para essa sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Título da sandbox"
>abstract="O título da sandbox é o nome de exibição que representará a sandbox em menus e menus suspensos na interface da Experience Platform."

>[!WARNING]
>
>A criação de uma nova sandbox exige que você a adicione a uma função em [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) antes de começar a usá-la. Para saber como provisionar uma sandbox para uma função, consulte a documentação [gerenciamento de sandboxes para uma função](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role).

Assista ao vídeo a seguir para obter uma visão geral rápida sobre como usar sandboxes na Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3430295/?captions=por_br&quality=12&learn=on)

Para criar uma nova sandbox, selecione **[!UICONTROL Create sandbox]** no canto superior direito da tela.

![criar-sandbox](../images/ui/create-sandbox.png)

A caixa de diálogo **[!UICONTROL Create sandbox]** é exibida. Selecione a lista suspensa **[!UICONTROL Type]** e escolha o tipo de sandbox [!UICONTROL Development] ou [!UICONTROL Production].

![A caixa de diálogo Criar sandbox com o seletor de tipo de sandbox realçado.](../images/ui/sandbox-type.png)

Após selecionar o tipo, forneça um nome para sua sandbox no campo **[!UICONTROL Name]**. O nome da sandbox é um identificador totalmente em minúsculas para uso em chamadas de API e, portanto, deve ser exclusivo e conciso. O nome da sandbox deve começar com uma letra, ter no máximo 256 caracteres e consistir apenas de caracteres alfanuméricos e hifens (-). Em seguida, forneça um título para sua sandbox no campo **[!UICONTROL Title]**. O título deve ser legível e descritivo o suficiente para ser facilmente identificável.

Quando terminar, selecione **[!UICONTROL Create]**.

![A caixa de diálogo Criar sandbox com o Nome e o Título preenchido e a opção Criar realçada.](../images/ui/sandbox-info.png)

Quando terminar de criar a sandbox, atualize a página e a nova sandbox aparecerá no painel **[!UICONTROL Sandboxes]** com o status &quot;[!UICONTROL Creating]&quot;. As novas sandboxes levam aproximadamente 30 segundos para serem provisionadas pelo sistema, depois disso seu status muda para &quot;[!UICONTROL Active]&quot;.

![O painel de sandboxes com a sandbox recém-criada está realçado.](../images/ui/new-sandbox.png)

## Redefinir uma sandbox

>[!WARNING]
>
>Veja a seguir uma lista de exceções que podem impedir a redefinição da sandbox de produção padrão ou de uma sandbox de produção criada pelo usuário:
>
>* Uma sandbox de produção criada pelo usuário usada para compartilhamento de segmento bidirecional com o Adobe Audience Manager ou o Audience Core Service pode ser redefinida após uma mensagem de aviso.
>* Antes de iniciar uma redefinição de sandbox, será necessário excluir suas composições manualmente para garantir que os dados do público-alvo associado sejam limpos corretamente.
>* A ID da sandbox será alterada após a conclusão da redefinição.
>* Para o [Journey Optimizer B2B edition](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/guide-overview), a redefinição da sandbox é **não suportada no momento**. Redefinir ou excluir uma sandbox mapeada para o Journey Optimizer B2B edition pode resultar em perda permanente de dados no Journey Optimizer B2B edition e exigir o provisionamento de uma nova instância do Journey Optimizer B2B edition.

### Excluir composições de público

No momento, a composição do público-alvo não está integrada ao recurso de redefinição da sandbox. Portanto, os públicos-alvo precisarão ser excluídos manualmente antes de executar a redefinição da sandbox.

Selecione **[!UICONTROL Audiences]** na seção **[!UICONTROL Customers]** na navegação à esquerda e selecione a guia **[!UICONTROL Compositions]**.

![O painel Públicos-alvo com a guia Composições selecionada e realçada.](../images/ui/audiences.png)

Em seguida, selecione as reticências (`...`) ao lado do primeiro público e selecione **[!UICONTROL Delete]**.

![O menu de público-alvo destacando a opção [!UICONTROL Delete].](../images/ui/delete-composition.png)

Uma confirmação de exclusão bem-sucedida é exibida e você retorna à guia **[!UICONTROL Compositions]**.

Repita as etapas acima com todas as suas composições. Isso excluirá todos os públicos-alvo do inventário de público-alvo. Depois que todos os públicos-alvo forem removidos, você poderá continuar redefinindo a sandbox.

### Redefinição de uma sandbox

A redefinição de uma sandbox de produção ou desenvolvimento exclui todos os recursos associados a essa sandbox (esquemas, conjuntos de dados e assim por diante), enquanto mantém o nome da sandbox e as permissões associadas. Essa sandbox &quot;limpa&quot; continua disponível com o mesmo nome para os usuários que têm acesso a ela.

Selecione a sandbox que deseja redefinir na lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Sandbox reset]**.

![O painel de sandbox com a sandbox escolhida selecionada e a opção Redefinição de sandbox realçada.](../images/ui/reset.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Selecione **[!UICONTROL Continue]** para continuar.

![A caixa de diálogo de redefinição é exibida com a opção de continuação realçada.](../images/ui/reset-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Reset]**.

![A caixa de diálogo de redefinição com o campo de nome de confirmação e a opção de redefinição foi realçada.](../images/ui/reset-confirm.png)

## Excluir uma sandbox

>[!WARNING]
>
>Não é possível excluir a sandbox de produção padrão. No entanto, qualquer sandbox de produção criada pelo usuário usada para compartilhamento de segmento bidirecional com [!DNL Audience Manager] ou [!DNL Audience Core Service] pode ser excluída após uma mensagem de aviso.

Excluir uma sandbox de produção ou desenvolvimento remove permanentemente todos os recursos associados a essa sandbox, incluindo permissões.

Selecione a sandbox que deseja excluir na lista de sandboxes. No painel de navegação direito exibido, selecione **[!UICONTROL Delete]**.

![O painel de sandbox com a sandbox escolhida selecionada e a opção Excluir realçada.](../images/ui/delete.png)

Uma caixa de diálogo é exibida solicitando que você confirme sua escolha. Selecione **[!UICONTROL Continue]** para continuar.

![A caixa de diálogo de exclusão é exibida com a opção de continuação realçada.](../images/ui/delete-warning.png)

Na janela de confirmação final, digite o nome da sandbox na caixa de diálogo e selecione **[!UICONTROL Continue]**.

![A caixa de diálogo de exclusão com a opção de confirmação de nome e continuar foi realçada.](../images/ui/delete-confirm.png)

## Próximas etapas

Este documento demonstrou como gerenciar sandboxes na interface do usuário do Experience Platform. Agora que você sabe como gerenciar sandboxes, saiba como melhorar a precisão da configuração em sandboxes e exportar e importar facilmente configurações de sandbox entre sandboxes com o guia [recurso de ferramenta de sandbox](./sandbox-tooling.md).

Para obter informações sobre como gerenciar sandboxes usando a API de sandbox, consulte o [guia do desenvolvedor de sandbox](../api/getting-started.md).
