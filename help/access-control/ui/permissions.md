---
keywords: Experience Platform;página inicial;tópicos populares;perfil de produto;gerenciar permissões
solution: Experience Platform
title: Gerenciar Permissões Para Um Perfil De Produto
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos do Experience Platform usando o Adobe Admin Console. Este documento serve como um guia sobre como gerenciar permissões de um perfil de produto para o Experience Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Gerenciar permissões de um perfil de produto

Imediatamente após [criar um novo perfil de produto](#create-a-new-product-profile), você será solicitado a configurar as permissões do perfil. Se você estiver editando permissões de um perfil existente, selecione o perfil na guia **[!UICONTROL Perfis de Produto]** para abrir a página de detalhes do perfil e selecione **[!UICONTROL Permissões]**.

![permissões](../images/permissions.png)

As permissões são divididas em categorias e listadas nesta página. A lista exibe o nome da categoria, o número de permissões que ela contém (e quantas estão ativas) e sua descrição. Consulte a tabela em [Permissões de recursos](/help/access-control/home.md#permissions) para obter um detalhamento das permissões disponíveis para cada função.

Selecione qualquer categoria na lista para abrir a página **[!UICONTROL Editar Permissões]**.

![editar-permissões](../images/edit-permissions.png)

A página **[!UICONTROL Editar Permissões]** fornece um espaço de trabalho para adicionar e remover permissões do perfil de produto selecionado. O lado esquerdo da tela exibe uma lista de categorias de permissão. Selecionar uma categoria altera as permissões exibidas em **[!UICONTROL Itens de permissões disponíveis]**.

Por exemplo, para atualizar permissões para Modelagem de Dados, selecione **[!UICONTROL Modelagem de Dados]**.

![gerenciamento de perfil](../images/profile-management.png)

Para adicionar uma permissão, selecione o ícone de adição **(+)** ao lado do nome da permissão. Como alternativa, você pode selecionar **[!UICONTROL Adicionar tudo]** para adicionar todas as permissões da categoria atual ao perfil. As permissões adicionadas aparecem em **[!UICONTROL Itens de permissão incluídos]**.

![adicionar-permissão](../images/add-permission.png)

>[!NOTE]
>
>A lista **[!UICONTROL Itens de Permissões Incluídos]** exibe somente as permissões adicionadas da categoria selecionada no momento.

Para remover uma permissão, selecione o ícone **X** ao lado do nome da permissão ou selecione **[!UICONTROL Remover tudo]** para remover todas as permissões na categoria atual. As permissões removidas reaparecerão em **[!UICONTROL Itens de Permissão Disponíveis]**.

Continue percorrendo as categorias disponíveis e adicionando as permissões desejadas. Quando terminar, selecione **[!UICONTROL Salvar]**.

![remover-permissão](../images/remove-permission.png)

A guia **[!UICONTROL Permissões]** para o perfil de produto será exibida novamente e mostrará que as permissões selecionadas agora estão ativas.

![permissões-atualizadas](../images/permissions-updated.png)

## Próximas etapas

Com as permissões estabelecidas, você pode prosseguir para a próxima etapa para [gerenciar detalhes e serviços para um perfil de produto](details-and-services.md)
