---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributos;ABAC
title: Permissões da Função Gerenciar Controle de Acesso Baseado em Atributo
description: Este documento fornece informações sobre como configurar permissões para uma função por meio da interface de Permissões no Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c1c7a851315214e2362085d3283d144066d4dd8a
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 2%

---

# Gerenciar permissões de uma função

>[!IMPORTANT]
>
>O controle de acesso usa a ID do usuário (uma ID exclusiva interna atribuída a um usuário) para conceder permissões. Quando uma organização for migrada do Adobe ID para a Business ID, todas as permissões definidas para os usuários serão perdidas, pois as alterações na ID do usuário e o controle de acesso usarão a ID do usuário recém-gerada. Se sua organização migrou para a Business ID, entre em contato com o representante da Adobe para migrar sua ID de usuário da Adobe ID para a Business ID.

Permissões é a área do Experience Cloud em que os administradores podem definir funções de usuário e políticas de acesso para gerenciar permissões de acesso para recursos e objetos em um aplicativo de produto.

Através das Permissões, é possível criar e gerenciar funções, bem como atribuir as permissões de recurso desejadas para essas funções. As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica.

Imediatamente após [criar uma nova função](#create-a-new-role), você retornará à guia **[!UICONTROL Funções]**. Se você estiver editando permissões para uma função existente, selecione a função na guia **[!UICONTROL Funções]**. Como alternativa, use a opção de filtro para filtrar os resultados para localizar uma função.

## Filtrar funções

Selecione o ícone de funil (![Ícone de filtro](../../images/icon.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

![filtros flac](../../images/flac-ui/flac-filters.png)

Os seguintes filtros estão disponíveis para funções na interface do usuário do:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Criado entre] | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. |
| [!UICONTROL Criado por] | Filtre por criador de função selecionando um usuário na lista suspensa. |
| [!UICONTROL Modificado entre] | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. |
| [!UICONTROL Modificado por] | Filtre por modificador de função selecionando um usuário na lista suspensa. |

Para remover um filtro, selecione o &quot;X&quot; no ícone de preenchimento do filtro em questão ou selecione **[!UICONTROL Limpar tudo]** para remover todos os filtros.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## Detalhes da função

Selecione a função na guia **[!UICONTROL Funções]**, que abrirá a página de detalhes da função.

![detalhes_flac](../../images/flac-ui/flac-details.png)

A guia de detalhes fornece uma visão geral da função. A visão geral exibe o nome da função, a descrição da função, o nome do usuário que criou e modificou a função, quando a função foi criada e modificada e as permissões anexadas à função. O nome e a descrição da função podem ser modificados, se necessário.

## Gerenciar rótulos para uma função

Selecione a guia **[!UICONTROL Rótulos]** para abrir a página de rótulos de funções, em seguida, selecione **[!UICONTROL Adicionar rótulos]** para atribuir rótulos à função.

![rótulos flac](../../images/flac-ui/flac-labels.png)

Os rótulos estão listados nesta página. A lista exibe o nome do rótulo, o nome amigável, a categoria e sua descrição.

Selecione os rótulos da lista que você deseja adicionar à função e selecione **[!UICONTROL Salvar]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

Os rótulos adicionados aparecem na guia **[!UICONTROL Rótulos]**.

![flac-adds-labels](../../images/flac-ui/flac-added-labels.png)

Para remover um rótulo de uma função, selecione o ícone **X** ao lado do nome dos rótulos.

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Gerenciamento de sandboxes para a função

Selecione a guia **[!UICONTROL Sandboxes]** para abrir a página sandboxes de funções. Aqui você pode ver uma lista de sandboxes que foram adicionadas à função.

![sandboxes flac](../../images/flac-ui/flac-sandboxes.png)

Para adicionar mais sandboxes a uma função, selecione **[!UICONTROL Editar]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

A próxima tela solicita que você escolha quais permissões de recurso existem nas sandboxes para incluir na função usando a lista suspensa. Quando terminar, selecione **[!UICONTROL Salvar e sair]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Gerenciando usuários para a função

Selecione a guia **[!UICONTROL Usuários]** para abrir a página de usuários de funções e selecione **[!UICONTROL Adicionar usuários]** para atribuir usuários à função.

![flac-users](../../images/flac-ui/flac-users.png)

Selecione os usuários da lista que você deseja adicionar à função. Como alternativa, use a barra de pesquisa para procurar o usuário digitando seu nome ou endereço de email e selecione **[!UICONTROL Salvar]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

Os usuários adicionados aparecem na guia **[!UICONTROL Usuários]**.

![flac-adds-users](../../images/flac-ui/flac-added-users.png)

Para remover um usuário de uma função, selecione o ícone **X** ao lado do nome dos usuários.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

O vídeo a seguir tem como objetivo ajudá-lo a entender a criação de uma nova função e o gerenciamento de usuários para essa função.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Gerenciar credenciais de API para a função {#manage-api-credentials-for-role}

Selecione a guia **[!UICONTROL Credenciais da API]** para abrir a página de credenciais da API de funções e selecione **[!UICONTROL Adicionar credenciais da API]** para atribuir credenciais da API à função.

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Selecione as credenciais de API na lista que você deseja adicionar à função e selecione **[!UICONTROL Salvar]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

As credenciais de API adicionadas aparecem na guia **[!UICONTROL Credenciais de API]**.

![flac-adds-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Para remover credenciais de API de uma função, selecione o ícone **X** ao lado do nome da credencial da API.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

A caixa de diálogo **[!UICONTROL Remover credenciais de API]** é exibida, solicitando que você confirme a exclusão.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Você retornará à guia **[!UICONTROL Credenciais da API]**.

## Gerenciar grupos de usuários para funções

Os grupos de usuários são vários usuários que foram agrupados e têm acesso para executar as mesmas funções.

Selecione a guia **[!UICONTROL Grupos de usuários]** para abrir a página de grupos de usuários de funções e selecione **[!UICONTROL Adicionar grupos]** para atribuir grupos de usuários à função.

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

Selecione os grupos de usuários na lista que você deseja adicionar à função. Como alternativa, use a barra de pesquisa para procurar o grupo de usuários digitando o nome do grupo e selecione **[!UICONTROL Salvar]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

O grupo de usuários adicionado aparece na guia **[!UICONTROL Grupos de usuários]**.

![flac-Added-User-Groups](../../images/flac-ui/flac-added-user-groups.png)

Para remover um grupo de usuários de uma função, selecione o ícone **X** ao lado do nome do grupo de usuários.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

A caixa de diálogo **[!UICONTROL Remover grupo de usuários]** é exibida, solicitando que você confirme a exclusão.

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Você retornará à guia **[!UICONTROL Grupos de usuários]**.

## Adicionar usuários ao Experience Platform por meio de uma função

Para adicionar um usuário a uma função, faça logon no Admin Console e selecione **[!UICONTROL Adicionar usuários]**

![perfil de produto-adicionar-usuários](../../images/flac-ui/product-profile-add-users.png)

A caixa de diálogo **[!UICONTROL Adicionar usuários à sua equipe]** é exibida. Insira o endereço de email do usuário, o nome (opcional) e o sobrenome (opcional).

Selecione o ícone de lápis para selecionar produtos e grupos de usuários, selecione **[!UICONTROL Adobe Experience Platform]**, selecione **[!UICONTROL AEP-Padrão-Todos-Usuários]** e **[!UICONTROL Salvar]**.

![perfil de produto](../../images/flac-ui/product-profile.png)

## Próximas etapas

Com as permissões estabelecidas, você pode prosseguir para a próxima etapa para [gerenciar usuários](users.md).
