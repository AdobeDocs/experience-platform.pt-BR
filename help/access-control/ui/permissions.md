---
keywords: Experience Platform;página inicial;tópicos populares;perfil de produto;gerenciar permissões
solution: Experience Platform
title: Gerenciar Permissões Para Um Perfil De Produto
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando o Adobe Admin Console. Este documento serve como um guia sobre como gerenciar permissões de um perfil de produto para a Platform.
exl-id: ca403bef-6d62-4ca9-bba6-d1280ac63171
source-git-commit: 1812af74e82f3071963177356b3cd4b23ea567f5
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Gerenciar permissões de um perfil de produto

Imediatamente após [criação de um novo perfil de produto](#create-a-new-product-profile), você será solicitado a configurar as permissões do perfil. Se você estiver editando permissões de um perfil existente, selecione o perfil na caixa suspensa **[!UICONTROL Perfis de produto]** para abrir a página de detalhes do perfil, selecione **[!UICONTROL Permissões]**.

![permissões](../images/permissions.png)

As permissões são divididas em categorias e listadas nesta página. A lista exibe o nome da categoria, o número de permissões que ela contém (e quantas estão ativas) e sua descrição. Consulte a tabela em [Permissões de recurso](/help/access-control/home.md#permissions) para obter um detalhamento das permissões disponíveis para cada função.

Selecione qualquer categoria na lista para abrir a **[!UICONTROL Editar permissões]** página.

![edit-permissions](../images/edit-permissions.png)

A variável **[!UICONTROL Editar permissões]** fornece um espaço de trabalho para adicionar e remover permissões do perfil de produto selecionado. O lado esquerdo da tela exibe uma lista de categorias de permissão. A seleção de uma categoria altera as permissões exibidas em **[!UICONTROL Itens de permissões disponíveis]**.

Por exemplo, para atualizar permissões para Modelagem de dados, selecione **[!UICONTROL Modelagem de dados]**.

![gerenciamento de perfis](../images/profile-management.png)

Para adicionar uma permissão, selecione o sinal de mais **(+)** ícone ao lado do nome da permissão. Como alternativa, você pode selecionar **[!UICONTROL Adicionar tudo]** para adicionar todas as permissões na categoria atual ao perfil. As permissões adicionadas aparecem em **[!UICONTROL Itens de permissão incluídos]**.

![add-permission](../images/add-permission.png)

>[!NOTE]
>
>A variável **[!UICONTROL Itens de permissões incluídos]** A lista só exibe as permissões adicionadas da categoria selecionada no momento.

Para remover uma permissão, selecione o **X** ícone ao lado do nome da permissão ou selecione **[!UICONTROL Remover tudo]** para remover todas as permissões na categoria atual. As permissões removidas reaparecerão em **[!UICONTROL Itens de permissão disponíveis]**.

Continue percorrendo as categorias disponíveis e adicionando as permissões desejadas. Quando terminar, selecione **[!UICONTROL Salvar]**.

![remover permissão](../images/remove-permission.png)

A variável **[!UICONTROL Permissões]** para o perfil de produto será exibida novamente e mostrará que as permissões selecionadas agora estão ativas.

![permissões atualizadas](../images/permissions-updated.png)

## Próximas etapas

Com as permissões estabelecidas, você pode prosseguir para a próxima etapa para [gerenciar detalhes e serviços para um perfil de produto](details-and-services.md)
