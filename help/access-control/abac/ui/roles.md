---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributos;ABAC
title: Controle de acesso baseado em atributos Criar uma função
description: Este documento fornece informações sobre como gerenciar funções por meio da interface de Permissões no Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Gerenciar funções

As funções definem o acesso que um administrador, um especialista ou um usuário final tem aos recursos em sua organização. Em um ambiente de controle de acesso baseado em funções, o provisionamento de acesso do usuário é agrupado por meio de responsabilidades e necessidades comuns. Uma função tem um determinado conjunto de permissões e os membros da organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de visualização ou acesso de gravação de que precisam.

## Criar uma nova função

Para criar uma nova função, selecione o **[!UICONTROL Funções]** na barra lateral e selecione **[!UICONTROL Criar Função]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

A variável **[!UICONTROL Criar uma nova função]** será exibida, solicitando que você insira um nome e uma descrição opcional.

Quando terminar, selecione **[!UICONTROL Confirmar o]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Em seguida, selecione as permissões de recurso que deseja incluir na função usando o menu suspenso.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Para adicionar recursos extras, selecione **[!UICONTROL Adobe Experience Platform]** no painel de navegação esquerdo, que exibe uma lista de recursos. Como alternativa, insira o nome do recurso na barra de pesquisa no painel de navegação esquerdo.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Clique e arraste o recurso relevante e solte no painel principal.

![flac-additional-resources-Added](../../images/flac-ui/flac-additional-resources-added.png)

Selecione as permissões de recurso que deseja incluir na função usando o menu suspenso. Repita isso para todos os recursos que você deseja incluir na função. Quando terminar, selecione **[!UICONTROL Salvar e sair]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

A nova função foi criada com sucesso e você será redirecionado para a **[!UICONTROL Funções]** página, onde você verá que a função recém-criada aparece na lista.

![flac-função-salva](../../images/flac-ui/flac-role-saved.png)

Consulte as seções sobre [gerenciando permissões para uma função](#manage-permissions-for-a-role) para obter mais detalhes sobre como gerenciar permissões de função depois de criadas.

## Duplicar uma função

Para duplicar uma função existente, selecione a função na **[!UICONTROL Funções]** guia. Como alternativa, use a opção de filtro para filtrar os resultados e encontrar a função que deseja duplicar.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Em seguida, selecione **[!UICONTROL Duplicar]** na parte superior direita da tela.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

A variável **[!UICONTROL Duplicar função]** será exibida, solicitando que você confirme a duplicação.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Em seguida, você será levado à página de detalhes da função, na qual poderá alterar o nome e as permissões da função. Os detalhes, rótulos e sandboxes são duplicados da função anterior. Os usuários precisarão ser adicionados por meio da guia Users. É possível exibir a [gerenciar permissões para uma função](permissions.md) documento para saber mais sobre como adicionar Detalhes, Rótulos, Sandboxes e Usuários a uma função.

Clique na seta à esquerda para retornar à **[!UICONTROL Funções]** guia.

![flac-retorno-para-funções](../../images/flac-ui/flac-return-to-roles.png)

A nova função aparecerá na lista da **[!UICONTROL Funções]** página.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Excluir uma função

Selecione as reticências (`…`) ao lado do nome de uma função, e uma lista suspensa exibe controles para editar, excluir ou duplicar a função. Selecione Excluir na lista suspensa.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

A variável **[!UICONTROL Excluir função de usuário]** será exibida, solicitando que você confirme a exclusão.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Você será redirecionado para a **[!UICONTROL Funções]** guia.

## Próximas etapas

Com uma nova função criada, você pode prosseguir para a próxima etapa para [gerenciar permissões para uma função](permissions.md).
