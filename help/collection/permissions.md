---
title: Gerenciamento de permissões para coleta de dados no Experience Platform
description: Uma visão geral de alto nível de como gerenciar permissões e controlar o acesso aos recursos de coleta de dados no Adobe Experience Platform.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 7%

---

# Gerenciamento de permissões para coleta de dados no Experience Platform

[Coleta de dados no Adobe Experience Platform](./home.md) O é composto por várias tecnologias diferentes que trabalham juntas para coletar e transferir seus dados. O acesso a essas tecnologias é controlado por meio de permissões granulares baseadas em funções no Adobe Admin Console.

Este guia mostra como gerenciar permissões para recursos de coleção de dados.

## Introdução

Para configurar o controle de acesso para a coleta de dados, você deve ter privilégios de administrador para uma organização que tenha uma integração de produto com a Coleta de dados da Adobe Experience Platform. A função mínima que pode conceder ou retirar permissões é um administrador de perfil de produto. Outras funções de administrador que podem gerenciar permissões são administradores de produtos (podem gerenciar todos os perfis em um produto) e administradores de sistema (sem restrições). Veja o artigo sobre [funções administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) no guia de administração do Adobe Enterprise para obter mais informações.

Este guia pressupõe que você esteja familiarizado com os conceitos básicos do Admin Console, como perfis de produtos e como eles concedem permissões de produto a usuários e grupos individuais. Para obter mais informações, consulte o [Guia do usuário do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

## Permissões disponíveis

As permissões relevantes para a coleta de dados são fornecidas por meio de duas designações de produto no Admin Console: **Adobe Experience Platform** e **Coleta de dados do Adobe Experience Platform**. As seções abaixo destacam as permissões fornecidas em cada produto, juntamente com descrições dos recursos específicos aos quais elas concedem acesso.

### Permissões do Adobe Experience Platform

As permissões no Adobe Experience Platform incluem acesso a conjuntos de dados, identidades, esquemas e sandboxes. Para obter etapas sobre como configurar permissões do Adobe Experience Platform, consulte o [guia do usuário de controle de acesso](../access-control/ui/overview.md).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| Sandboxes | (N/D) | Dependendo do [sandboxes](../sandboxes/home.md) que foram criadas em sua organização, você pode controlar o acesso a cada um deles por meio desta categoria de permissão no Admin Console. |
| Modelagem de dados | Gerenciar esquemas | Concede a capacidade de visualizar, criar e editar [Schemas do Experience Data Model (XDM)](../xdm/home.md). |
| Modelagem de dados | Visualizar esquemas | Concede acesso somente leitura a esquemas. |
| Gerenciamento de identidade | Gerenciar namespaces de identidade | Concede a capacidade de visualizar, criar e editar [namespaces de identidade](../identity-service/namespaces.md). |
| Gerenciamento de identidade | Exibir namespaces de identidade | Concede acesso somente leitura a namespaces de identidade. |
| Coleção de dados | Gerenciar datastreams | Concede a capacidade de visualizar, criar e editar [datastreams](../edge/datastreams/overview.md). |
| Coleção de dados | Visualizar fluxos de dados | Concede acesso somente leitura a conjuntos de dados. |

{style=&quot;table-layout:auto&quot;}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Permissões para Coleta de dados do Adobe Experience Platform

As permissões no Adobe Experience Platform Data Collection controlam o acesso a tags e recursos de encaminhamento de eventos, incluindo propriedades, extensões e ambientes. Para obter etapas sobre como configurar as permissões de Coleta de dados do Adobe Experience Platform, consulte [seção abaixo](#manage).

| Categoria | Permissão | Descrição |
| --- | --- | --- |
| Plataformas | Web | Concede acesso a [propriedades da web](../tags/ui/administration/companies-and-properties.md) quando combinado com outros direitos de propriedade. |
| Plataformas | Dispositivo móvel | Concede acesso a [propriedades móveis](../tags/ui/administration/companies-and-properties.md) quando combinado com outros direitos de propriedade. |
| Propriedades | (N/D) | Dependendo das propriedades que foram criadas em sua organização, você pode controlar o acesso a cada uma delas por meio dessa categoria de permissão no Admin Console.<br><br>Os direitos de propriedade atribuídos a um usuário se aplicam apenas às propriedades às quais ele recebeu acesso por meio desta categoria de permissão. |
| Direitos de propriedade | Aprovar | Concede a capacidade de aprovar uma build de biblioteca como parte do [fluxo de publicação](../tags/ui/publishing/publishing-flow.md). |
| Direitos de propriedade | Desenvolver | Concede a capacidade de desenvolver uma build de biblioteca como parte do [fluxo de publicação](../tags/ui/publishing/publishing-flow.md). |
| Direitos de propriedade | Editar propriedade | Concede a capacidade de editar a configuração básica das propriedades às quais um usuário tem acesso. |
| Direitos de propriedade | Gerenciar ambientes | Concede a capacidade de gerenciar o [ambientes](../tags/ui/publishing/environments.md) para as propriedades às quais um usuário tem acesso. |
| Direitos de propriedade | Gerenciar extensões | Concede a capacidade de gerenciar o [extensões](../tags/ui/managing-resources/extensions/overview.md) para as propriedades às quais um usuário tem acesso. |
| Direitos de propriedade | Publicar | Concede a capacidade de publicar uma build de biblioteca como parte do [fluxo de publicação](../tags/ui/publishing/publishing-flow.md). |
| Direitos da empresa | Desenvolver extensões | Concede a capacidade de criar e modificar pacotes de extensão da propriedade de sua organização, incluindo versões privadas e solicitações de lançamento de versão pública. |
| Direitos da empresa | Gerenciar extensões | Essa permissão só se aplica se você tiver uma licença do Adobe Journey Optimizer ou outra solução que conceda acesso a mensagens por push e no aplicativo móvel. Isso permite gerenciar os aplicativos que a Adobe Experience Cloud conhece, juntamente com as credenciais de push necessárias para se comunicar com o serviço de Firebase Cloud Messaging e o serviço de Notificação por push da Apple. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Para obter mais informações sobre como essas permissões afetam os recursos nas tags, incluindo estratégias de administração para cenários comuns, consulte a documentação das tags em [permissões do usuário](../tags/ui/administration/user-permissions.md).

## Gerenciar permissões para a coleta de dados do Adobe Experience Platform {#manage}

>[!IMPORTANT]
>
>Esta seção só aborda como gerenciar permissões para o produto Adobe Experience Platform Data Collection no Admin Console. No entanto, as etapas para gerenciar permissões no produto Adobe Experience Platform são semelhantes.
>
>Consulte a [guia da interface do usuário de controle de acesso](../access-control/ui/overview.md) para obter instruções detalhadas sobre como gerenciar permissões da plataforma. Dependendo dos SKUs de produtos aos quais sua organização tem acesso, talvez você não tenha todas as permissões disponíveis.

Para gerenciar permissões para a Coleta de dados, faça logon no [Admin Console](https://adminconsole.adobe.com/) e selecione **[!UICONTROL Produtos]** no início da navegação. Aqui, selecione o cartão para **[!UICONTROL Coleta de dados do Adobe Experience Platform]**.

![Imagem que mostra o cartão de produto Coleta de dados no Admin Console](./images/permissions/data-collection-card.png)

### Selecionar ou criar um perfil de produto

A próxima tela mostra uma lista de perfis de produto disponíveis para a Coleta de dados em sua organização, com o perfil padrão sendo **[!DNL Default Data Collection All Access]**. Você pode optar por editar o perfil de produto padrão, se desejar, ou pode selecionar **[!UICONTROL Novo perfil]** para criar um. Se você tiver várias funções ou grupos de usuários em sua organização que exigem diferentes níveis de acesso, deverá criar um perfil de produto separado para cada um deles.

![Imagem que mostra os perfis de produto para a Coleta de dados no Admin Console](./images/permissions/new-profile.png)

Após selecionar ou criar um perfil de produto, você pode usar a variável **[!UICONTROL Editar]** ícones para iniciar [edição de permissões](#edit-permissions) para o perfil, ou selecione o **[!UICONTROL Usuários]** guia para iniciar [atribuição de usuários](#assign-users) ao perfil.

![Imagem que mostra a guia de permissões para um Admin Console de perfil de produto](./images/permissions/edit-permission-categories.png)

### Editar permissões para o perfil de produto {#edit-permissions}

Ao editar permissões para um perfil, as permissões disponíveis são listadas na coluna da esquerda, enquanto as permissões incluídas no perfil são listadas na coluna da direita. Selecione as permissões listadas para movê-las entre qualquer uma das colunas.

![Imagem que mostra as permissões adicionadas sob a coluna incluída](./images/permissions/added-permissions.png)

As permissões são organizadas em categorias. Para alternar entre categorias, selecione a categoria desejada no painel de navegação esquerdo.

![Imagem que mostra a seção de direitos da empresa em permissões](./images/permissions/switch-category.png)

Selecionar **[!UICONTROL Salvar]** após concluir a configuração das permissões.

![Imagem que mostra a configuração de permissão sendo salva para o perfil do produto](./images/permissions/save-permissions.png)

A exibição do perfil do produto é exibida novamente com as permissões adicionadas refletidas.

![Imagem que mostra as permissões adicionadas para o perfil do produto](./images/permissions/permissions-added.png)

### Atribuir usuários ao perfil de produto {#assign-users}

Para atribuir usuários ao perfil do produto (e conceder a eles as permissões configuradas do perfil), selecione o **[!UICONTROL Usuários]** , seguido por **[!UICONTROL Adicionar usuário]**.

![Imagem que mostra a guia usuários para um perfil de produto no Admin Console](./images/permissions/manage-users.png)

Para obter mais informações sobre como gerenciar usuários para um perfil de produto, consulte [Documentação do Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## Próximas etapas

Este guia cobriu as permissões disponíveis para a interface do usuário da Coleta de dados e como gerenciá-las por meio do Admin Console. Para obter mais informações sobre gerenciamento de permissões para outros recursos do Adobe Experience Platform, consulte [documentação de controle de acesso](../access-control/home.md).
