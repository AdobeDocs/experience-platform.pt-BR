---
title: Gerenciamento de permissões para coleta de dados no Experience Platform
description: Uma visão geral de alto nível sobre como gerenciar permissões e controlar o acesso aos recursos de coleção de dados no Adobe Experience Platform.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 29%

---

# Gerenciamento de permissões para coleta de dados no Experience Platform

[Coleta de dados no Adobe Experience Platform](./home.md) O é composto por várias tecnologias diferentes que trabalham juntas para coletar e transferir seus dados. O acesso a essas tecnologias é controlado por meio de permissões granulares baseadas em funções no Adobe Admin Console.

Este guia mostra como gerenciar permissões para recursos de coleção de dados.

## Introdução

Para configurar o controle de acesso para a coleta de dados, é necessário ter privilégios de administrador para uma organização que tenha uma integração de produto com a Coleção de dados da Adobe Experience Platform. A função mínima que pode conceder ou suspender permissões é a de **administrador de perfil de produto**. Outras funções de administrador que podem gerenciar permissões são **administradores de produtos** (pode gerenciar todos os perfis em um produto) e **administradores de sistema** (sem restrições). Consulte o artigo sobre [funções administrativas](https://helpx.adobe.com/br/enterprise/using/admin-roles.html), no manual de administração do Adobe Enterprise, para obter mais informações.

Este manual supõe que você já esteja familiarizado com conceitos básicos do Admin Console, como perfis de produtos, e como eles concedem permissões de produto a usuários individuais e grupos. Para obter mais informações, consulte o [Manual do usuário do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

## Permissões disponíveis

As permissões relevantes para a Coleção de dados são fornecidas por meio de duas designações de produto no Admin Console: **Adobe Experience Platform** e **Coleta de dados do Adobe Experience Platform**. As seções abaixo descrevem as permissões fornecidas em cada produto, juntamente com descrições dos recursos específicos aos quais eles concedem acesso.

### Permissões do Adobe Experience Platform

As permissões no Adobe Experience Platform incluem acesso a sequências de dados, identidades, esquemas e sandboxes. Para obter etapas sobre como configurar permissões do Adobe Experience Platform, consulte a [guia do usuário de controle de acesso](../access-control/ui/overview.md).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| Sandboxes | (N/D) | Dependendo do [sandboxes](../sandboxes/home.md) que foram criadas em sua organização, você pode controlar o acesso a cada uma delas por meio desta categoria de permissão no Admin Console. |
| Modelagem de dados | Gerenciar esquemas | Concede a capacidade de exibir, criar e editar [Esquemas do Experience Data Model (XDM)](../xdm/home.md). |
| Modelagem de dados | Visualizar esquemas | Concede acesso somente leitura a esquemas. |
| Gerenciamento de identidade | Gerenciar namespaces de identidade | Concede a capacidade de exibir, criar e editar [namespaces de identidade](../identity-service/namespaces.md). |
| Gerenciamento de identidade | Exibir namespaces de identidade | Concede acesso somente leitura a namespaces de identidade. |
| Coleção de dados | Gerenciar fluxos de dados | Concede a capacidade de exibir, criar e editar [sequências de dados](../datastreams/overview.md). |
| Coleção de dados | Exibir fluxos de dados | Concede acesso somente leitura a sequências de dados. |

{style="table-layout:auto"}

### Permissões de coleção de dados do Adobe Experience Platform

As permissões em Coleta de dados da Adobe Experience Platform controlam o acesso a recursos de encaminhamento de tags e eventos, incluindo propriedades, extensões e ambientes. Para obter etapas sobre como configurar permissões de Coleta de dados do Adobe Experience Platform, consulte a [seção abaixo](#manage).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| Plataformas | Web | Concede acesso a [propriedades da web](../tags/ui/administration/companies-and-properties.md) quando combinado com outros direitos de propriedade. |
| Plataformas | Dispositivo móvel | Concede acesso a [propriedades móveis](../tags/ui/administration/companies-and-properties.md) quando combinado com outros direitos de propriedade. |
| Plataformas | Edge | Concede acesso a [Propriedades da borda de encaminhamento de eventos](../tags/ui/event-forwarding/getting-started.md) quando combinado com outros direitos de propriedade. |
| Propriedades | (N/D) | Dependendo das propriedades que foram criadas em sua organização, você pode controlar o acesso a cada uma delas por meio desta categoria de permissão no Admin Console.<br><br>Os direitos de propriedade atribuídos de um usuário se aplicam apenas às propriedades às quais ele recebeu acesso por meio desta categoria de permissão. |
| Direitos de propriedade | Aprovar | Concede a capacidade de aprovar um build de biblioteca como parte da [fluxo de publicação](../tags/ui/publishing/publishing-flow.md). |
| Direitos de propriedade | Desenvolver | Concede a capacidade de desenvolver um build de biblioteca como parte da [fluxo de publicação](../tags/ui/publishing/publishing-flow.md). |
| Direitos de propriedade | Editar propriedade | Concede a capacidade de editar a configuração básica das propriedades às quais um usuário tem acesso. |
| Direitos de propriedade | Gerenciamento de ambientes | Concede a capacidade de gerenciar o [ambientes](../tags/ui/publishing/environments.md) para as propriedades às quais um usuário tem acesso. |
| Direitos de propriedade | Gerenciar extensões | Concede a capacidade de gerenciar o [extensões](../tags/ui/managing-resources/extensions/overview.md) para as propriedades às quais um usuário tem acesso. |
| Direitos de propriedade | Publicar | Concede a capacidade de publicar um build de biblioteca como parte da [fluxo de publicação](../tags/ui/publishing/publishing-flow.md). |
| Direitos da empresa | Desenvolver extensões | Concede a capacidade de criar e modificar pacotes de extensão de propriedade de sua organização, incluindo versões privadas e solicitações de lançamento de versão pública. |
| Direitos da empresa | Gerenciar extensões | Essa permissão só é aplicável se você tiver uma licença do Adobe Journey Optimizer ou outra solução que conceda acesso a mensagens móveis no aplicativo e por push. Isso permite gerenciar os aplicativos que o Adobe Experience Cloud conhece, juntamente com as credenciais de push necessárias para se comunicar com o serviço Firebase Cloud Messaging e o serviço Apple Push Notification. |

{style="table-layout:auto"}

>[!NOTE]
>
>Para obter mais informações sobre como essas permissões afetam os recursos nas tags, incluindo estratégias administrativas para cenários comuns, consulte a documentação das tags em [permissões de usuário](../tags/ui/administration/user-permissions.md).

## Gerenciar permissões {#manage}

As permissões para coleta de dados são gerenciadas por meio de duas designações de produto: **Adobe Experience Platform** e **Coleta de dados do Adobe Experience Platform**.

Consulte as subseções abaixo para ver as etapas sobre como gerenciar as permissões relevantes em cada produto do Admin Console:

* [Permissões do Adobe Experience Platform](#manage-platform)
* [Permissões de coleção de dados do Adobe Experience Platform](#manage-collection)

### Gerenciar permissões no Adobe Experience Platform {#manage-platform}

No **[!UICONTROL Permissões]** no Adobe Experience Platform selecione a função que deseja editar.

Para acessar os recursos de coleção de dados, é necessário habilitar todas as permissões no **[!UICONTROL Sandboxes]**, **[!UICONTROL Modelagem de dados]**, **[!UICONTROL Identity Management]**, e **[!UICONTROL Coleta de dados]** categorias.

![Imagem mostrando o cartão de produto Coleta de dados no Admin Console](./images/permissions/platform-permission-card.png)

Consulte a [guia da interface do usuário de controle de acesso](../access-control/ui/overview.md) para obter instruções detalhadas sobre o gerenciamento de permissões da Platform.

>[!NOTE]
>
>Dependendo das SKUs do produto às quais sua organização tem acesso, talvez você não tenha todas as permissões da Platform disponíveis.

### Gerenciar permissões na Coleção de dados da Adobe Experience Platform {#manage-collection}

Para gerenciar essas permissões, faça logon no Admin Console e selecione **[!UICONTROL Produtos]** no início da navegação, selecione **[!UICONTROL Coleta de dados do Adobe Experience Platform]**.

![Imagem mostrando o cartão de produto Coleta de dados no Admin Console](./images/permissions/data-collection-card.png)

#### Selecionar ou criar um perfil de produto

A próxima tela mostra uma lista de perfis de produto disponíveis para a Coleção de dados na sua organização, sendo o perfil padrão **[!DNL Default Data Collection All Access]**. Se desejar, é possível editar o perfil de produto padrão ou selecionar **[!UICONTROL Novo perfil]** para criar um. Se possuir várias funções ou grupos de usuários em sua organização que precisam de diferentes níveis de acesso, crie um perfil de produto separado para cada um deles.

![Imagem que mostra os perfis de produto para a coleta de dados no Admin Console](./images/permissions/new-profile.png)

Após selecionar ou criar um perfil de produto, você pode usar o **[!UICONTROL Editar]** ícones para iniciar [editar permissões](#edit-permissions) para o perfil, ou selecione o **[!UICONTROL Usuários]** guia para iniciar [atribuição de usuários](#assign-users) ao perfil.

![Imagem mostrando a guia de permissões de um perfil de produto no Admin Console](./images/permissions/edit-permission-categories.png)

#### Editar permissões para o perfil de produto {#edit-permissions}

Ao editar as permissões de um perfil, as permissões disponíveis são listadas na coluna à esquerda e as permissões incluídas no perfil são listadas na coluna à direita. Selecione as permissões listadas para movê-las entre as duas colunas.

![Imagem mostrando permissões adicionadas abaixo da coluna incluída](./images/permissions/added-permissions.png)

As permissões são organizadas em categorias. Para alternar entre categorias, selecione a categoria desejada na painel de navegação à esquerda.

![Imagem mostrando a seção de direitos da empresa em permissões](./images/permissions/switch-category.png)

Clique em **[!UICONTROL Salvar]** quando terminar de configurar as permissões.

![Imagem mostrando a configuração de permissão sendo salva para o perfil do produto](./images/permissions/save-permissions.png)

A visualização do perfil de produto será exibida novamente com as permissões adicionadas.

![Imagem mostrando as permissões adicionadas no perfil do produto](./images/permissions/permissions-added.png)

#### Atribuir usuários ao perfil de produto {#assign-users}

Para atribuir usuários ao perfil de produto (e conceder a eles as permissões configuradas nele), selecione a guia **[!UICONTROL Usuários]** e, em seguida, **[!UICONTROL Adicionar usuário]**.

![Imagem mostrando a guia Usuários em um perfil de produto no Admin Console](./images/permissions/manage-users.png)

Para obter mais informações sobre como gerenciar usuários em um perfil de produto, consulte a [Documentação do Admin Console](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html).

## Próximas etapas

Este guia abordou as permissões disponíveis para Coleta de dados e como gerenciá-las por meio do Admin Console. Para obter mais informações sobre como gerenciar as permissões para outros recursos da Adobe Experience Platform, consulte a [documentação de controle de acesso](../access-control/home.md).
