---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributo;;home;popular topics;access control;attribute-based access control;ABAC
title: Controle de acesso baseado em atributos Criar uma função
description: Este documento fornece informações sobre como gerenciar funções por meio da interface de Permissões no Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 23%

---

# Gerenciar funções

As funções definem o acesso que um(a) admin, especialista ou usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões, e os membros da organização podem ter uma ou mais funções atribuídas, dependendo do escopo do acesso de visualização ou gravação necessário.

## Criar uma nova função {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Criar nova função"
>abstract="Crie novas funções para categorizar melhor os usuários que interagem com sua instância da Experience Platform. Por exemplo, é possível criar uma função para uma equipe interna de marketing e aplicar o rótulo de dados de saúde regulamentados (RHD) a essa função, permitindo que sua equipe de marketing interna acesse informações de saúde protegidas (PHI). Como alternativa, também é possível criar uma função para uma agência externa e negar o acesso dela aos dados de PHI por não aplicar o rótulo RHD a essa função."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=pt-BR" text="Gerenciar uma função"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="Aplicar rótulos a uma função"

Para criar uma nova função, selecione a guia **[!UICONTROL Funções]** na barra lateral e selecione **[!UICONTROL Criar Função]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

A caixa de diálogo **[!UICONTROL Criar uma nova função]** é exibida, solicitando que você insira um nome e uma descrição opcional.

Quando terminar, selecione **[!UICONTROL Confirmar]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Em seguida, selecione as permissões de recurso que deseja incluir na função usando o menu suspenso.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Para adicionar recursos extras, selecione **[!UICONTROL Adobe Experience Platform]** no painel de navegação esquerdo, que exibe uma lista de recursos. Como alternativa, insira o nome do recurso na barra de pesquisa no painel de navegação esquerdo.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Clique e arraste o recurso relevante e solte no painel principal.

![flac-additional-resources-Added](../../images/flac-ui/flac-additional-resources-added.png)

Selecione as permissões de recurso que deseja incluir na função usando o menu suspenso. Repita isso para todos os recursos que você deseja incluir na função. Quando terminar, selecione **[!UICONTROL Salvar e sair]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

A nova função foi criada com êxito, e você será redirecionado para a página **[!UICONTROL Funções]**, onde verá que a função recém-criada aparece na lista.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Consulte as seções sobre [gerenciamento de permissões para uma função](#manage-permissions-for-a-role) para obter mais detalhes sobre como gerenciar permissões de função após sua criação.

O vídeo a seguir tem como objetivo ajudá-lo a entender a criação de uma nova função e o gerenciamento de usuários para essa função.

>[!VIDEO](https://video.tv.adobe.com/v/3475978/?captions=por_br&learn=on)

## Duplicar uma função

Para duplicar uma função existente, selecione a função na guia **[!UICONTROL Funções]**. Como alternativa, use a opção de filtro para filtrar os resultados e encontrar a função que deseja duplicar.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Em seguida, selecione **[!UICONTROL Duplicar]** na parte superior direita da tela.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

A caixa de diálogo **[!UICONTROL Duplicar função]** é exibida, solicitando que você confirme a duplicação.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Em seguida, você será levado à página de detalhes da função, na qual poderá alterar o nome e as permissões da função. Os detalhes, rótulos e sandboxes são duplicados da função anterior. Os usuários precisarão ser adicionados por meio da guia Users. Você pode exibir o documento [gerenciar permissões para uma função](permissions.md) para saber mais sobre como adicionar Detalhes, Rótulos, Sandboxes e Usuários a uma função.

Clique na seta à esquerda para retornar à guia **[!UICONTROL Funções]**.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

A nova função aparecerá na lista na página **[!UICONTROL Funções]**.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Excluir uma função

Selecione as reticências (`…`) ao lado do nome de uma função, e uma lista suspensa exibe controles para editar, excluir ou duplicar a função. Selecione Excluir na lista suspensa.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

A caixa de diálogo **[!UICONTROL Excluir função de usuário]** é exibida, solicitando que você confirme a exclusão.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Você retornará à guia **[!UICONTROL Funções]**.

## Próximas etapas

Com uma nova função criada, você pode prosseguir para a próxima etapa para [gerenciar permissões para uma função](permissions.md).
