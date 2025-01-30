---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributos;ABAC
title: Permissões da Função Gerenciar Controle de Acesso Baseado em Atributo
description: Este documento fornece informações sobre como configurar permissões para uma função por meio da interface de Permissões no Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 0c275dc18dac101455f77aa58d33f0808122b77f
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 1%

---

# Gerenciar permissões de uma função

>[!IMPORTANT]
>
>O controle de acesso usa a ID do usuário (uma ID exclusiva interna atribuída a um usuário) para conceder permissões. Quando uma organização for migrada do Adobe ID para a Business ID, todas as permissões definidas para os usuários serão perdidas, pois as alterações na ID do usuário e o controle de acesso usarão a ID do usuário recém-gerada. Se sua organização migrou para a Business ID, entre em contato com o representante da Adobe para migrar sua ID de usuário da Adobe ID para a Business ID.

Permissões é a área do Experience Cloud em que os administradores podem definir funções de usuário e políticas de acesso para gerenciar permissões de acesso para recursos e objetos em um aplicativo de produto.

Através das Permissões, é possível criar e gerenciar funções, bem como atribuir as permissões de recurso desejadas para essas funções. As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica.

Imediatamente após [criar uma nova função](#create-a-new-role), você retornará à guia **[!UICONTROL Funções]**. Se você estiver editando permissões para uma função existente, selecione a função na guia **[!UICONTROL Funções]**. Como alternativa, use a opção de filtro para filtrar os resultados para localizar uma função.

## Filtrar funções

Selecione o ícone de funil (![Ícone de filtro](/help/images/icons/filter.png)) para exibir uma lista de controles de filtro para ajudar a limitar os resultados.

![O painel Funções na interface de Permissões com a seção de funções de filtro realçada.](../../images/flac-ui/flac-filters.png)

Os seguintes filtros estão disponíveis para funções na interface do usuário do:

| Filtro | Descrição |
| --- | --- |
| [!UICONTROL Criado entre] | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. |
| [!UICONTROL Criado por] | Filtre por criador de função selecionando um usuário na lista suspensa. |
| [!UICONTROL Modificado entre] | Selecione uma data inicial e/ou final para definir um intervalo de datas para filtrar os resultados. |
| [!UICONTROL Modificado por] | Filtre por modificador de função selecionando um usuário na lista suspensa. |

Para remover um filtro, selecione o &quot;X&quot; no ícone de preenchimento do filtro em questão ou selecione **[!UICONTROL Limpar tudo]** para remover todos os filtros.

![O painel Funções na interface de Permissões com o X e Limpar todas as seleções realçadas nos filtros escolhidos.](../../images/flac-ui/flac-clear-filters.png)

## Detalhes da função

Selecione a função na guia **[!UICONTROL Funções]**, que abrirá o painel [!UICONTROL Detalhes] da função.

![O espaço de trabalho Detalhes da função selecionada é exibido com as informações de visão geral destacadas.](../../images/flac-ui/flac-details.png)

O painel [!UICONTROL Detalhes] fornece uma visão geral da função. A visão geral exibe o nome da função, a descrição, o criador e o último modificador, juntamente com as datas de criação e modificação. Ele também mostra as permissões anexadas à função e a lista de sandboxes atribuídas. O nome e a descrição da função podem ser modificados, se necessário.

## Gerenciar rótulos para uma função

Selecione a guia **[!UICONTROL Rótulos]** para abrir o espaço de trabalho de rótulos de funções e selecione **[!UICONTROL Adicionar rótulos]** para atribuir rótulos à função.

![O espaço de trabalho de Rótulos da função é exibido com a guia Rótulos e o botão Adicionar Rótulos destacados.](../../images/flac-ui/flac-labels.png)

A caixa de diálogo **[!UICONTROL Aplicar rótulos de acesso e governança de dados]** é exibida, apresentando uma lista de rótulos. A lista exibe o nome do rótulo, o nome amigável, a categoria e sua descrição.

Selecione os rótulos da lista que você deseja adicionar à função e selecione **[!UICONTROL Salvar]**

![A caixa de diálogo Aplicar Rótulos de Acesso e Governança de Dados com um rótulo selecionado.](../../images/flac-ui/flac-add-labels.png)

Os rótulos adicionados aparecem na guia **[!UICONTROL Rótulos]**.

![O espaço de trabalho de Rótulos da função com o rótulo adicionado realçado.](../../images/flac-ui/flac-added-labels.png)

Para remover um rótulo de uma função, selecione o rótulo e, em seguida, selecione **[!UICONTROL Remover Rótulos]**.

![O espaço de trabalho de Rótulos da função com uma função selecionada e a opção Remover rótulos realçada.](../../images/flac-ui/flac-delete-labels.png)

## Gerenciar sandboxes para uma função

Selecione a guia **[!UICONTROL Detalhes]** e navegue até a seção **[!UICONTROL Sandboxes]**. Selecione **[!UICONTROL Exibir tudo]** para ver a lista completa de sandboxes adicionadas à função.

![O espaço de trabalho Detalhes da função com a seção Sandboxes realçada.](../../images/flac-ui/flac-sandboxes.png)

Para adicionar mais sandboxes a uma função, selecione **[!UICONTROL Editar]** na parte superior direita da interface.

![O espaço de trabalho Detalhes da função com a opção Editar realçada.](../../images/flac-ui/flac-add-sandboxes.png)

A próxima tela solicita que você escolha quais recursos de sandboxes incluir na função usando a lista suspensa. Quando terminar, selecione **[!UICONTROL Salvar]** e depois **[!UICONTROL Fechar]**.

![O painel de Recursos da função com o menu suspenso de recursos da sandbox foi realçado.](../../images/flac-ui/flac-add-role-permission.png)

## Gerenciar usuários para uma função

Selecione a guia **[!UICONTROL Usuários]** para abrir o espaço de trabalho de funções [!UICONTROL Usuários] e selecione **[!UICONTROL Adicionar Usuários]** para atribuir usuários à função.

![O espaço de trabalho Usuários da função é exibido com a guia Usuários e a opção Adicionar Usuários realçada.](../../images/flac-ui/flac-users.png)

A caixa de diálogo **[!UICONTROL Adicionar usuários]** é exibida. Selecione os usuários da lista que você deseja adicionar à função. Como alternativa, use a barra de pesquisa para procurar o usuário digitando seu nome ou endereço de email e selecione **[!UICONTROL Salvar]**

![A caixa de diálogo Adicionar Usuários com um usuário selecionado e a barra de pesquisa e a opção de gravação destacadas.](../../images/flac-ui/flac-add-users.png)

Os usuários adicionados aparecem na guia **[!UICONTROL Usuários]**.

![O espaço de trabalho Usuários da função mostrando os usuários adicionados à função.](../../images/flac-ui/flac-added-users.png)

Para remover um usuário de uma função, selecione o ícone **X** ao lado do nome do usuário.

![O espaço de trabalho Usuários da função mostrando um usuário com a opção X realçada.](../../images/flac-ui/flac-remove-users.png)

O vídeo a seguir tem como objetivo ajudá-lo a entender a criação de uma nova função e o gerenciamento de usuários para essa função.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Gerenciar credenciais de API para uma função {#manage-api-credentials-for-role}

>[!IMPORTANT]
>
> Para usar e gerenciar credenciais de API em [!UICONTROL Permissões], os usuários devem ter privilégios de administrador do sistema.

Para usar APIs Experience Platform como um usuário ou desenvolvedor, um administrador do sistema precisa adicionar credenciais de API, além de um conjunto de permissões fornecido por uma função. Para obter um guia completo sobre como criar e atribuir credenciais de API, bem como as permissões necessárias, consulte o tutorial passo a passo em [autenticar e acessar APIs de Experience Platform](../../../landing/api-authentication.md#generate-credentials).

Selecione a guia **[!UICONTROL Credenciais de API]** para abrir o espaço de trabalho de credenciais de API de funções e selecione **[!UICONTROL Adicionar credenciais de API]** para atribuir credenciais de API à função.

![O espaço de trabalho de credenciais de API da função com a opção Adicionar credenciais foi realçado.](../../images/flac-ui/flac-api-credentials.png)

A caixa de diálogo **[!UICONTROL Adicionar credenciais de API]** é exibida. Selecione as credenciais de API na lista para adicionar à função e selecione **[!UICONTROL Salvar]**

![A caixa de diálogo Adicionar credenciais de API com uma credencial selecionada e a opção Salvar realçada.](../../images/flac-ui/flac-add-api-credentials.png)

As credenciais de API adicionadas aparecem na guia **[!UICONTROL Credenciais de API]**.

![O espaço de trabalho de credenciais de API da função com as credenciais adicionadas exibidas.](../../images/flac-ui/flac-added-api-credentials.png)

Para remover uma credencial de API de uma função, selecione o ícone **X** ao lado do nome da credencial de API.

![O espaço de trabalho de credenciais de API da função com a opção X para remover uma credencial realçada.](../../images/flac-ui/flac-remove-api-credentials.png)

A caixa de diálogo **[!UICONTROL Remover credenciais de API]** é exibida, solicitando que você confirme a exclusão. Selecione **[!UICONTROL Confirmar]** para concluir a remoção da credencial selecionada.

![O popover Remover Credencial solicitando que você confirme a remoção da credencial está realçado.](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Você retornará à guia **[!UICONTROL Credenciais da API]**.

## Gerenciar grupos de usuários para uma função

Os grupos de usuários são vários usuários que foram agrupados e têm acesso para executar as mesmas funções.

Selecione a guia **[!UICONTROL Grupos de usuários]** para abrir o espaço de trabalho dos grupos de usuários da função e selecione **[!UICONTROL Adicionar grupos]** para atribuir grupos de usuários à função.

![O espaço de trabalho dos grupos de usuários da função com a opção Adicionar Grupos](../../images/flac-ui/flac-user-groups.png)

A caixa de diálogo **[!UICONTROL Adicionar grupos]** é exibida. Selecione os grupos de usuários na lista que você deseja adicionar à função. Como alternativa, use a barra de pesquisa para procurar o grupo de usuários digitando o nome do grupo e selecione **[!UICONTROL Salvar]**

![A caixa de diálogo Adicionar Grupos com um grupo de usuários selecionado e a opção Pesquisar e Salvar realçada.](../../images/flac-ui/flac-add-user-groups.png)

O grupo de usuários adicionado aparece na guia **[!UICONTROL Grupos de usuários]**.

![O espaço de trabalho dos grupos de usuários da função exibindo a lista de grupos de usuários adicionados.](../../images/flac-ui/flac-added-user-groups.png)

Para remover um grupo de usuários de uma função, selecione o ícone **X** ao lado do nome do grupo de usuários.

![O espaço de trabalho dos grupos de usuários da função com a opção X para remover um grupo de usuários específico realçado.](../../images/flac-ui/flac-remove-user-groups.png)

A caixa de diálogo **[!UICONTROL Remover grupo de usuários]** é exibida, solicitando que você confirme a exclusão. Selecione **[!UICONTROL Confirmar]** para remover o grupo de usuários selecionado.

![O pop-over para remover um grupo de usuários é exibido e realçado.](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Você retornará à guia **[!UICONTROL Grupos de usuários]**.

## Adicionar usuários ao Experience Platform

Como administrador do sistema, você pode conceder acesso de desenvolvedor a um usuário para que ele possa [criar integrações](../../../landing/api-authentication.md#generate-credentials) na Adobe Developer Console.

Para adicionar um Experience Platform de usuário, faça logon no [Admin Console](https://adminconsole.adobe.com) e selecione **[!UICONTROL Adicionar usuários]**.

![O painel do Adobe Admin Console com a opção Adicionar usuários foi realçado.](../../images/flac-ui/product-profile-add-users.png)

A caixa de diálogo **[!UICONTROL Adicionar usuários à sua equipe]** será exibida. Insira o endereço de email do usuário, o nome (opcional) e o sobrenome (opcional). Em seguida, selecione **[!UICONTROL Produtos]**.

![A caixa de diálogo Adicionar usuários à equipe com os campos de usuário e a opção Produtos foi realçada.](../../images/flac-ui/product-profile-add-users-to-your-team.png)

A caixa de diálogo **[!UICONTROL Selecionar produtos]** é exibida. Selecione **[!UICONTROL Adobe Experience Platform]**.

![A caixa de diálogo Selecionar produtos com o Adobe Experience Platform foi realçada.](../../images/flac-ui/product-profile-select-product.png)

A caixa de diálogo **[!UICONTROL Selecionar perfis de produto]** é exibida. Selecione **[!UICONTROL AEP-Default-All-Users]** e **[!UICONTROL Salvar]**.

![A caixa de diálogo Selecionar perfis de produto com AEP-Padrão-Todos-Usuários foi selecionada e Aplicar foi realçada.](../../images/flac-ui/product-profile-select-product-profiles.png)

Revise as informações e selecione **[!UICONTROL Salvar]** para adicionar o usuário.

![A caixa de diálogo Adicionar usuários à equipe com as informações do usuário e as seleções escolhidas, e a opção Salvar realçada.](../../images/flac-ui/product-profile-save-user.png)

## Próximas etapas

Com as permissões estabelecidas, você pode prosseguir para a próxima etapa para [gerenciar usuários](users.md).
