---
title: Gerenciar permissões do Privacy Service
description: Saiba como gerenciar permissões de usuário do Adobe Experience Platform Privacy Service usando o Adobe Admin Console.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Gerenciar permissões do Privacy Service

Acesso ao [Adobe Experience Platform Privacy Service](./home.md) O é controlado por meio de permissões granulares baseadas em funções no Adobe Admin Console. Ao criar perfis de produto que atribuem permissões a grupos de usuários, é possível determinar quem tem acesso a quais recursos no Privacy Service [interface](./ui/overview.md) e [API](./api/overview.md).

>[!NOTE]
>
>Ao criar uma integração para a API do Privacy Service, você deve selecionar um perfil de produto existente para determinar quais recursos ou ações essa integração tem permissões. Consulte o guia sobre [introdução à API do Privacy Service](./api/getting-started.md) para obter mais informações.

Este guia mostra como gerenciar permissões para o Privacy Service.

## Introdução

Para configurar o controle de acesso para o Privacy Service, você deve ter privilégios de administrador para uma organização que tenha uma integração de produto com o Adobe Experience Platform Privacy Service. A função mínima que pode conceder ou retirar permissões é uma **administrador de perfil de produto**. Outras funções de administrador que podem gerenciar permissões são **administradores de produtos** (pode gerenciar todos os perfis em um produto) e **administradores de sistema** (sem restrições). Veja o artigo sobre [funções administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) no guia de administração do Adobe Enterprise para obter mais informações.

Este guia pressupõe que você esteja familiarizado com os conceitos básicos do Admin Console, como perfis de produtos e como eles concedem permissões de produto a usuários e grupos individuais. Para obter mais informações, consulte o [Guia do usuário do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

## Permissões disponíveis

A tabela a seguir descreve as permissões disponíveis para o Privacy Service com descrições dos recursos específicos aos quais ele concede acesso:

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| [!UICONTROL Permissões de Privacy Service] | [!UICONTROL Permissão de leitura de privacidade] | Determina se o usuário pode exibir solicitações de acesso e exclusão existentes, juntamente com seus detalhes. |
| [!UICONTROL Permissões de Privacy Service] | [!UICONTROL Permissão de gravação de privacidade] | Determina se um usuário pode criar novas solicitações de acesso e exclusão. |
| [!UICONTROL Permissões de Privacy Service] | [!UICONTROL Permissão para entrega de conteúdo de leitura (acesso)] | Quando uma solicitação de acesso é processada pelo Privacy Service, um arquivo ZIP contendo os dados do cliente é enviado para esse cliente. Ao pesquisar os detalhes de uma solicitação de acesso, essa permissão determina se o usuário pode acessar o link de download do arquivo ZIP da solicitação. |
| [!UICONTROL Permissões de cancelamento da venda] | [!UICONTROL Permissão de leitura - Recusar venda] | Determina se o usuário pode visualizar solicitações de não participação na venda, juntamente com seus detalhes. |
| [!UICONTROL Permissões de cancelamento da venda] | [!UICONTROL Permissão de gravação - Recusar a venda] | Determina se um usuário pode criar novas solicitações de recusa de venda. |

{style=&quot;table-layout:auto&quot;}

## Gerenciar permissões {#manage}

Para gerenciar permissões do Privacy Service, faça logon no [Admin Console](https://adminconsole.adobe.com/) e selecione **[!UICONTROL Produtos]** no início da navegação. Aqui, selecione **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Imagem que mostra a placa de produto Privacy Service no Admin Console](./images/permissions/privacy-service-card.png)

### Selecionar ou criar um perfil de produto

A próxima tela mostra uma lista de perfis de produto disponíveis para o Privacy Service em sua organização. Se não houver perfis de produto, selecione **[!UICONTROL Novo perfil]** para criar um. Se você tiver várias funções ou grupos de usuários em sua organização que exigem diferentes níveis de acesso, deverá criar um perfil de produto separado para cada um deles.

![Imagem que mostra os perfis de produto do Privacy Service no Admin Console](./images/permissions/select-or-create-profile.png)

Após selecionar um perfil de produto, você pode usar a variável **[!UICONTROL Permissões]** guia para iniciar [edição de permissões](#edit-permissions) para o perfil, ou selecione o **[!UICONTROL Usuários]** guia para iniciar [atribuição de usuários](#assign-users) ao perfil.

![Imagem que mostra a guia de permissões para um Admin Console de perfil de produto](./images/permissions/users-permissions-tabs.png)

### Editar permissões para o perfil {#edit-permissions}

No **[!UICONTROL Permissões]** selecione qualquer uma das categorias de permissão exibidas para acessar a exibição de edição de permissões.

Ao editar permissões para um perfil, as permissões disponíveis são listadas na coluna da esquerda, enquanto as permissões incluídas no perfil são listadas na coluna da direita. Selecione as permissões listadas para movê-las entre qualquer uma das colunas.

![Imagem que mostra as colunas de permissão disponíveis e incluídas](./images/permissions/edit-permissions.png)

As permissões são organizadas em categorias. Para alternar entre categorias, selecione a categoria desejada no painel de navegação esquerdo.

![Imagem que mostra o [!UICONTROL Recusar venda] seção em permissões](./images/permissions/switch-category.png)

Selecionar **[!UICONTROL Salvar]** após concluir a configuração das permissões.

![Imagem que mostra a configuração de permissão sendo salva para o perfil do produto](./images/permissions/save-permissions.png)

A exibição do perfil do produto é exibida novamente com as permissões adicionadas refletidas.

![Imagem que mostra as permissões adicionadas para o perfil do produto](./images/permissions/permissions-added.png)

### Atribuir usuários ao perfil {#assign-users}

Para atribuir usuários ao perfil do produto (e conceder a eles as permissões configuradas do perfil), selecione o **[!UICONTROL Usuários]** , seguido por **[!UICONTROL Adicionar usuário]**.

![Imagem que mostra a guia usuários para um perfil de produto no Admin Console](./images/permissions/manage-users.png)

Para obter mais informações sobre como gerenciar usuários para um perfil de produto, consulte [Documentação do Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### Migrar credenciais da API herdada para o perfil {#migrate-tech-accounts}

>[!NOTE]
>
>Esta seção se aplica somente às credenciais de API existentes que foram criadas antes de as permissões do Privacy Service serem integradas ao Adobe Admin Console. Para novas credenciais, os perfis de produto (e suas permissões) são atribuídos por meio de [Projetos do Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/projects/) em vez disso.<br><br>Consulte a seção sobre [atribuição de perfis de produto a um projeto](./api/getting-started.md#product-profiles) no guia de introdução à API do Privacy Service para obter mais informações.

Para migrar credenciais da API herdada para o perfil do produto, selecione **[!UICONTROL Credenciais da API]**, seguida de **[!UICONTROL Adicionar credenciais de API]**.

![[!UICONTROL Adicionar credenciais de API] sendo selecionado no Admin Console, em [!UICONTROL Credenciais da API] guia para um perfil de produto](./images/permissions/api-credentials.png)

Escolha os projetos desejados do Console do desenvolvedor na lista e selecione **[!UICONTROL Salvar]** para adicioná-las ao perfil de produto. Todas as chamadas de API que usam as credenciais desses projetos herdarão as permissões granulares concedidas pelo perfil do produto.

## Próximas etapas

Este guia cobriu as permissões disponíveis para o Privacy Service e como gerenciá-las por meio do Admin Console.

Para obter etapas sobre como criar uma nova integração de API após configurar perfis de produto, consulte [guia de introdução à API do Privacy Service](./api/getting-started.md). Para obter mais informações sobre gerenciamento de permissões para outros recursos do Adobe Experience Platform, consulte [documentação de controle de acesso](../access-control/home.md).
