---
keywords: Experience Platform; gerenciamento de tags; tags;
title: Gerenciamento de tags administrativas
description: Este documento fornece informações sobre o gerenciamento de tags administrativas no Adobe Experience Cloud
hide: true
hidefromtoc: true
source-git-commit: 7f0572af2d582353a0dde12bdb6692f342463312
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Guia de gerenciamento de tags

As tags permitem gerenciar taxonomias de metadados para classificar objetos de negócios para facilitar a detecção e a categorização. As tags podem ajudar a identificar atributos taxonômicos importantes para os públicos-alvo com os quais as equipes vão trabalhar, para que possam encontrá-los mais rapidamente e agrupar públicos-alvo comuns em um descritor. Você deve identificar categorias de tags comuns, como regiões geográficas, unidades comerciais, linhas de produtos, projetos, equipes, intervalos de tempo (trimestres, meses, anos) ou qualquer outra coisa que possa ajudar a aplicar significado e facilitar a descoberta de público-alvo para sua equipe. 

## Criar uma tag {#create-tag}

Para criar uma nova tag, selecione **[!UICONTROL tags]** no painel de navegação esquerdo, selecione a categoria de tag desejada.

![Selecionar uma categoria de tag](./images/tag-selection.png)

Selecionar **[!UICONTROL Criar tag]** para criar uma nova tag.

![Criar uma nova tag](./images/new-tag.png)

O **[!UICONTROL Criar tag]** for exibida, solicitando a inserção de um nome de tag exclusivo. Quando terminar, selecione **[!UICONTROL Salvar]**.

![Criar caixa de diálogo de tag com o novo nome de tag](./images/create-tag-dialog.png)

A nova tag foi criada com êxito e você é redirecionado para a tela de tags, onde a tag recém-criada será exibida na lista.

![Tag recém-criada para a categoria de tag](./images/new-tag-listed.png)

## Editar uma tag {#edit-tag}

A edição de uma tag ajuda quando há erros ortográficos, atualizações de convenção de nomenclatura ou atualizações de terminologia. A edição de uma tag manterá a associação da tag a quaisquer objetos nos quais elas estão atualmente aplicadas.

Para editar uma tag existente, na lista de categoria de tag, selecione as reticências (`...`) ao lado do nome da tag que você deseja editar. Uma lista suspensa exibe controles para editar, mover ou arquivar a tag. Selecionar **[!UICONTROL Editar]** na lista suspensa.

![Editar ação mostrada na lista suspensa](./images/edit-action.png)

O **[!UICONTROL Editar tag]** for exibida, solicitando a edição do nome da tag. Quando terminar, selecione **[!UICONTROL Salvar]**.

![Editar caixa de diálogo de tag com nome de tag atualizado](./images/edit-dialog.png)

O nome da tag é atualizado com êxito e você é redirecionado para a tela de tags, onde a tag atualizada será exibida na lista.

![Tag atualizada para a categoria de tag](./images/updated-tag-listed.png)

## Mover uma tag entre categorias {#move-tag}

As tags podem ser movidas para outras categorias de tags. Mover uma tag manterá a associação da tag a quaisquer objetos nos quais ela está sendo aplicada no momento.

Para mover uma tag existente, na lista de categoria de tag, selecione as reticências (`...`) ao lado do nome da tag que você deseja mover. Uma lista suspensa exibe controles para editar, mover ou arquivar a tag. Selecionar **[!UICONTROL Editar]** na lista suspensa.

![Mover ação mostrada na lista suspensa](./images/move-action.png)

O **[!UICONTROL Mover tag]** for exibida, solicitando que você selecione a categoria de tag na qual a tag selecionada deve ser movida.

Você pode rolar e selecionar na lista ou, alternativamente, usar o recurso de pesquisa para inserir o nome da categoria. Quando terminar, selecione **[!UICONTROL Mover]**.

![Mover caixa de diálogo de tag com critérios de pesquisa para localizar a categoria de tag](./images/move-dialog.png)

A tag foi movida com êxito e você é redirecionado para a tela de tags, onde você verá a lista de tags atualizada, onde a tag não será mais exibida.

![Lista de tags atualizada para a categoria de tag atual](./images/current-tag-category.png)

A tag agora aparecerá na categoria de tag selecionada anteriormente.

![Lista de tags para a categoria de tag selecionada para mover a tag](./images/moved-to-tag-category.png)

## Arquivar uma tag {#archive-tag}

O status de uma tag pode ser alternado entre ativa e arquivada. As tags arquivadas não são removidas de objetos em que já foram aplicadas, mas não podem mais ser aplicadas a novos objetos. Para cada tag, o mesmo status é refletido em todos os objetos. Isso é particularmente útil quando você deseja manter as associações de objeto de tag atuais, mas não quer que a tag seja usada no futuro.

Para arquivar uma tag existente, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja arquivar. Uma lista suspensa exibe controles para editar, mover ou arquivar a tag. Selecionar **[!UICONTROL Arquivar]** na lista suspensa.

![Ação de arquivamento mostrada na lista suspensa](./images/archive-action.png)

O **[!UICONTROL Arquivar tag]** for exibida, solicitando que você confirme o arquivo de tags. Selecionar **[!UICONTROL Arquivar]**.

![Caixa de diálogo da tag de arquivamento solicitando confirmação](./images/archive-dialog.png)

A tag é arquivada com êxito e você é redirecionado para a tela da tag. Você verá a lista de tags atualizada mostrando o status da tag como `Archived`.

![Lista de tags atualizada para a categoria de tag atual que mostra a tag como arquivada](./images/archive-status.png)

## Restaurar uma tag arquivada {#restore-archived-tag}

Se quiser aplicar um `Archived` para novos objetos, a tag deve estar em um `Active` estado. A restauração de uma tag arquivada retornará uma tag ao `Active` estado.

Para restaurar uma tag arquivada, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja restaurar. Uma lista suspensa exibe controles para restaurar ou excluir a tag . Selecionar **[!UICONTROL Restaurar]** na lista suspensa.

![Ação de restauração mostrada na lista suspensa](./images/restore-action.png)

O **[!UICONTROL Restaurar tag]** for exibida, solicitando que você confirme a restauração da tag. Selecionar **[!UICONTROL Restaurar]**.

![Caixa de diálogo Restaurar tag solicitando confirmação](./images/restore-dialog.png)

A tag foi restaurada com êxito e você é redirecionado para a tela da tag . Você verá a lista de tags atualizada mostrando o status da tag como `Active`.

![Lista de tags atualizada para a categoria de tag atual que mostra a tag como ativa](./images/restored-active-status.png)

## Excluir uma tag {#delete-tag}

>[!NOTE]
>
>Somente tags que estão em um `Archived` e não estão associados a nenhum objeto pode ser excluído.

A exclusão de uma tag a removerá completamente do sistema.

Para excluir uma tag arquivada, na lista de categorias de tags, selecione as reticências (`...`) ao lado do nome da tag que você deseja excluir. Uma lista suspensa exibe controles para restaurar ou excluir a tag . Selecionar **[!UICONTROL Excluir]** na lista suspensa.

![Excluir ação mostrada na lista suspensa](./images/delete-action.png)

O **[!UICONTROL Excluir tag]** for exibida, solicitando que você confirme a exclusão da tag. Clique em **[!UICONTROL Excluir]**.

![Caixa de diálogo Excluir tag solicitando confirmação](./images/delete-dialog.png)

A tag foi excluída com êxito e você é redirecionado para a tela da tag. A tag não aparece mais na lista e foi completamente removida.

![A lista de tags atualizada para a categoria de tag atual que mostra a tag não aparece mais na lista](./images/deleted-updated-list.png)

## Como visualizar objetos marcados {#view-tagged}

Cada tag tem uma página de detalhes que pode ser acessada do inventário de tags. Esta página lista todos os objetos que têm essa tag aplicada no momento, permitindo que os usuários vejam objetos relacionados de aplicativos e recursos diferentes em uma única visualização.

Para exibir a lista de objetos marcados, encontre a tag em uma categoria de tag e selecione a tag .

![Seleção de tag na categoria de tag](./images/view-tag-selection.png)

O [!UICONTROL Objetos marcados] for exibida, mostrando um inventário dos objetos marcados.

![Inventário de objetos marcados](./images/tagged-objects.png)

## Próximas etapas

Agora você aprendeu a gerenciar tags. Para obter uma visão geral de alto nível das tags no Experience Platform, consulte [documentação de visão geral das tags](../overview.md).
