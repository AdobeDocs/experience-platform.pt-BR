---
keywords: Experience Platform;gerenciamento de tags;tags;
title: Gerenciamento de tags unificadas
description: Este documento fornece informações sobre o gerenciamento de tags unificadas no Adobe Experience Cloud
exl-id: 179b0618-3bd3-435c-9d17-63681177ca47
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Guia de gerenciamento de tags

As tags permitem gerenciar taxonomias de metadados para classificar objetos de negócios para facilitar a descoberta e a categorização. As tags podem ajudar a identificar atributos taxonômicos importantes para os públicos com os quais suas equipes trabalharão, para que possam encontrá-los mais rapidamente e também agrupar públicos comuns em um descritor. Você deve identificar categorias de tags comuns, como regiões geográficas, unidades de negócios, linhas de produtos, projetos, equipes, intervalos de tempo (trimestres, meses, anos) ou qualquer outra coisa que possa ajudar a aplicar significado e facilitar a descoberta de públicos-alvo para sua equipe. 

## Criar uma tag {#create-tag}

Para criar uma nova tag, selecione **[!UICONTROL tags]** na navegação à esquerda, selecione a categoria de tag desejada.

![Selecionar uma categoria de tag](./images/tag-selection.png)

Selecionar **[!UICONTROL Criar tag]** para criar uma nova tag.

![Criar uma nova tag](./images/new-tag.png)

A variável **[!UICONTROL Criar tag]** será exibida, solicitando que você insira um nome de tag exclusivo. Quando terminar, selecione **[!UICONTROL Salvar]**.

![Caixa de diálogo Criar tag com um novo nome de tag](./images/create-tag-dialog.png)

A nova tag foi criada com sucesso e você é redirecionado para a tela de tags, onde a tag recém-criada será exibida na lista.

![Tag recém-criada para a categoria de tag](./images/new-tag-listed.png)

## Editar uma tag {#edit-tag}

A edição de uma tag ajuda quando há erros ortográficos, atualizações de convenção de nomenclatura ou atualizações de terminologia. A edição de uma tag manterá a associação da tag com qualquer objeto no qual ela esteja aplicada no momento.

Para editar uma tag existente, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja editar. Uma lista suspensa exibe controles para editar, mover ou arquivar a tag. Selecionar **[!UICONTROL Editar]** na lista suspensa.

![Editar ação mostrada na lista suspensa](./images/edit-action.png)

A variável **[!UICONTROL Editar tag]** será exibida, solicitando que você edite o nome da tag. Quando terminar, selecione **[!UICONTROL Salvar]**.

![Caixa de diálogo Editar tag com nome de tag atualizado](./images/edit-dialog.png)

O nome da tag foi atualizado com sucesso e você será redirecionado para a tela tags, onde a tag atualizada aparecerá na lista.

![Tag atualizada para a categoria de tag](./images/updated-tag-listed.png)

## Mover uma tag entre categorias {#move-tag}

As tags podem ser movidas para outras categorias de tag. Mover uma tag manterá a associação da tag com qualquer objeto no qual ela esteja aplicada no momento.

Para mover uma tag existente, na lista de categorias de tag, selecione as reticências (`...`) ao lado do nome da tag que você deseja mover. Uma lista suspensa exibe controles para editar, mover ou arquivar a tag. Selecionar **[!UICONTROL Editar]** na lista suspensa.

![Ação de movimentação mostrada na lista suspensa](./images/move-action.png)

A variável **[!UICONTROL Mover tag]** será exibida, solicitando que você selecione a categoria da tag para onde a tag selecionada deve ser movida.

Você pode rolar a tela e selecionar itens na lista ou, como alternativa, usar o recurso de pesquisa para inserir o nome da categoria. Quando terminar, selecione **[!UICONTROL Mover]**.

![Mover caixa de diálogo de tag com critérios de pesquisa para localizar categoria de tag](./images/move-dialog.png)

A tag é movida com sucesso e você é redirecionado para a tela tags, onde você verá a lista de tags atualizada, onde a tag não é mais exibida.

![Lista de tags atualizada para a categoria de tag atual](./images/current-tag-category.png)

A tag agora aparecerá na categoria de tag selecionada anteriormente.

![Lista de tags da categoria de tags selecionada para mover a tag](./images/moved-to-tag-category.png)

## Arquivar uma tag {#archive-tag}

O status de uma tag pode ser alternado entre ativa e arquivada. As tags arquivadas não são removidas dos objetos nos quais já foram aplicadas, mas não podem mais ser aplicadas a novos objetos. Para cada tag, o mesmo status é refletido em todos os objetos. Isso é particularmente útil quando você deseja manter as associações atuais de objeto de tag, mas não deseja que a tag seja usada no futuro.

Para arquivar uma tag existente, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja arquivar. Uma lista suspensa exibe controles para editar, mover ou arquivar a tag. Selecionar **[!UICONTROL Arquivar]** na lista suspensa.

![Ação de arquivamento mostrada na lista suspensa](./images/archive-action.png)

A variável **[!UICONTROL Arquivar tag]** será exibida, solicitando que você confirme o arquivamento de tags. Selecionar **[!UICONTROL Arquivar]**.

![Caixa de diálogo Arquivar tag solicitando confirmação](./images/archive-dialog.png)

A tag foi arquivada com êxito e você será redirecionado para a tela de tags. Você verá que a lista de tags atualizada agora mostra o status da tag como `Archived`.

![Lista de tags atualizada para a categoria de tag atual que mostra a tag como arquivada](./images/archive-status.png)

## Restaurar uma tag arquivada {#restore-archived-tag}

Se quiser aplicar uma `Archived` para novos objetos, a tag deve estar em uma `Active` estado. Restaurar uma tag arquivada retornará uma tag a sua `Active` estado.

Para restaurar uma tag arquivada, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja restaurar. Uma lista suspensa exibe controles para restaurar ou excluir a tag. Selecionar **[!UICONTROL Restaurar]** na lista suspensa.

![Ação de restauração mostrada na lista suspensa](./images/restore-action.png)

A variável **[!UICONTROL Restaurar tag]** será exibida, solicitando que você confirme a restauração da tag. Selecionar **[!UICONTROL Restaurar]**.

![Caixa de diálogo Restaurar tag solicitando confirmação](./images/restore-dialog.png)

A tag foi restaurada com sucesso e você foi redirecionado para a tela de tags. Você verá que a lista de tags atualizada agora mostra o status da tag como `Active`.

![Lista de tags atualizada para a categoria de tag atual que mostra a tag como ativa](./images/restored-active-status.png)

## Excluir uma tag {#delete-tag}

>[!NOTE]
>
>Somente as tags que estão em um `Archived` e não estão associados a nenhum objeto podem ser excluídos.

A exclusão de uma tag a removerá completamente do sistema.

Para excluir uma tag arquivada, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja excluir. Uma lista suspensa exibe controles para restaurar ou excluir a tag. Selecionar **[!UICONTROL Excluir]** na lista suspensa.

![Excluir ação mostrada na lista suspensa](./images/delete-action.png)

A variável **[!UICONTROL Excluir tag]** será exibida, solicitando que você confirme a exclusão da tag. Clique em **[!UICONTROL Excluir]**.

![Caixa de diálogo Excluir tag solicitando confirmação](./images/delete-dialog.png)

A tag foi excluída com sucesso e você será redirecionado para a tela de tags. A tag do não aparece mais na lista e foi completamente removida.

![A lista de tags atualizada para a categoria de tag atual que mostra a tag não aparece mais na lista](./images/deleted-updated-list.png)

## Exibição de objetos marcados {#view-tagged}

Cada tag tem uma página detalhada que pode ser acessada no inventário de tags. Esta página lista todos os objetos que atualmente têm essa tag aplicada, permitindo que os usuários vejam objetos relacionados de diferentes aplicativos e recursos em uma única visualização.

Para exibir a lista de objetos com marcas de formatação, localize a marca de formatação em uma categoria de marca de formatação e selecione-a.

![Seleção de tag na categoria de tag](./images/view-tag-selection.png)

A variável [!UICONTROL Objetos marcados] será exibida, mostrando um inventário de objetos marcados.

![Inventário de objetos marcados](./images/tagged-objects.png)

## Próximas etapas

Agora você aprendeu a gerenciar tags. Para obter uma visão geral de alto nível das tags no Experience Platform, consulte o [documentação da visão geral das tags](../overview.md).
