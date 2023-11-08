---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributos;
title: Guia completo do controle de acesso baseado em atributos
description: Este documento fornece um guia completo sobre o controle de acesso baseado em atributos no Adobe Experience Platform
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 19%

---

# Guia completo do controle de acesso baseado em atributos

O controle de acesso baseado em atributos é um recurso da Adobe Experience Platform que oferece a clientes com várias marcas e preocupados com a privacidade maior flexibilidade para gerenciar o acesso dos usuários. O acesso a objetos individuais, como campos de esquema e segmentos, pode ser concedido/negado com políticas baseadas nos atributos e na função do objeto. Esse recurso permite conceder ou revogar o acesso a objetos individuais para usuários específicos da Platform em sua organização.

Essa funcionalidade permite categorizar campos de esquema, segmentos e outros com rótulos que definem escopos organizacionais ou de uso de dados. Você pode aplicar esses mesmos rótulos a jornadas, Ofertas e outros objetos no Adobe Journey Optimizer. Em paralelo, os administradores podem definir políticas de acesso em torno dos campos de esquema do Experience Data Model (XDM) e gerenciar melhor quais usuários ou grupos (usuários internos, externos ou de terceiros) podem acessar esses campos.

>[!NOTE]
>
>Este documento se concentra no caso de uso de políticas de controle de acesso. Se você estiver tentando configurar políticas para controlar a **use** de dados em vez de quais usuários da Platform têm acesso a eles, consulte o manual completo sobre [governança de dados](../../data-governance/e2e.md) em vez disso.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes da Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md): o mecanismo de segmentação dentro do [!DNL Platform] usado para criar segmentos de público-alvo a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.

### Visão geral do caso de uso

Você passará por um exemplo de fluxo de trabalho de controle de acesso baseado em atributos, em que você criará e atribuirá funções, rótulos e políticas para configurar se os usuários podem ou não acessar recursos específicos na organização. Este guia usa um exemplo de restrição de acesso a dados confidenciais para demonstrar o fluxo de trabalho. Este caso de uso é descrito abaixo:

Você é um provedor de assistência médica e deseja configurar o acesso aos recursos em sua organização.

* Sua equipe interna de marketing deve poder acessar **[!UICONTROL PHI/ Dados de saúde regulamentados]** dados.
* Sua agência externa não deve poder acessar **[!UICONTROL PHI/ Dados de saúde regulamentados]** dados.

Para fazer isso, você deve configurar funções, recursos e políticas.

Você vai:

* [Rotular as funções para seus usuários](#label-roles): Use o exemplo de um provedor de serviços de saúde (ACME Business Group) cujo grupo de marketing trabalha com agências externas.
* [Rotular os recursos (campos e segmentos de esquema)](#label-resources): atribua a **[!UICONTROL PHI/ Dados de saúde regulamentados]** rótulo para recursos e segmentos de esquema.
* 
   * [Ative a política que os vinculará:](#policy): ative a política padrão para impedir o acesso a campos e segmentos de esquema conectando os rótulos dos seus recursos aos rótulos na sua função. Os usuários com rótulos correspondentes receberão acesso ao campo de esquema e ao segmento em todas as sandboxes.

## Permissões

[!UICONTROL Permissões] é a área do Experience Cloud em que os administradores podem definir funções e políticas de usuário para gerenciar permissões de recursos e objetos em um aplicativo de produto do.

Até [!UICONTROL Permissões], você pode criar e gerenciar funções e atribuir as permissões de recurso desejadas para essas funções. [!UICONTROL As permissões também permitem gerenciar rótulos, sandboxes e usuários associados a uma função específica.]

Entre em contato com o administrador do sistema para obter acesso se você não tiver privilégios de administrador.

Quando tiver privilégios de administrador, acesse [Adobe Experience Cloud](https://experience.adobe.com/) e faça logon usando suas credenciais de Adobe. Depois de conectado, a variável **[!UICONTROL Visão geral]** é exibida para sua organização para a qual você tem privilégios de administrador. Esta página mostra os produtos nos quais sua organização está inscrita, juntamente com outros controles para adicionar usuários e administradores à organização. Selecionar **[!UICONTROL Permissões]** para abrir o espaço de trabalho para sua integração com a Platform.

![Imagem mostrando o produto de Permissões que está sendo selecionado no Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

O espaço de trabalho de Permissões para a interface do usuário da Platform é exibido, abrindo na **[!UICONTROL Funções]** página.

## Aplicar rótulos a uma função {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="O que são rótulos?"
>abstract="Os rótulos permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. A Platform fornece vários rótulos de uso de dados “principais” definidos pela Adobe, que abrangem uma grande variedade de restrições comuns aplicáveis à governança de dados. Por exemplo, rótulos sensíveis “S”, como RHD (Regulated Health Data, dados de saúde regulamentados), permitem categorizar dados que se referem a PHI (Protected Health Information, informações de saúde protegidas). Também é possível definir seus próprios rótulos personalizados que atendam às necessidades de sua organização."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=pt-BR#understanding-data-usage-labels" text="Visão geral dos rótulos de uso de dados"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Criar novo rótulo"
>abstract="É possível criar seus próprios rótulos personalizados para atender às necessidades de sua organização. Os rótulos personalizados podem ser usados para aplicar configurações de governança de dados e controle de acesso aos seus dados."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=pt-BR#manage-labels" text="Gerenciar rótulos personalizados"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="O que são funções?"
>abstract="Funções são maneiras de categorizar os tipos de usuários que estão interagindo com sua instância da Platform. São os pilares das políticas de controle de acesso. Uma função tem um determinado conjunto de permissões, e os membros da organização podem ter uma ou mais funções atribuídas, dependendo do escopo do acesso de visualização ou gravação necessário."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=pt-BR" text="Gerenciar funções"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Criar nova função"
>abstract="É possível criar uma nova função para categorizar melhor os usuários que estão acessando sua instância da Platform. Por exemplo, você pode criar uma função para uma equipe interna de marketing e aplicar o rótulo RHD a essa função, permitindo que sua equipe interna de marketing acesse as informações de saúde protegidas (PHI). Como alternativa, você também pode criar uma função para uma agência externa e negar acesso a essa função para dados PHI ao não aplicar o rótulo RHD a essa função."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=pt-BR#create-a-new-role" text="Criar uma nova função"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Visão geral da função"
>abstract="A caixa de diálogo de visão geral da função exibe os recursos e as sandbox que uma determinada função tem permissão para acessar."

Funções são maneiras de categorizar os tipos de usuários que interagem com sua instância da Platform e são blocos fundamentais das políticas de controle de acesso. Uma função tem determinado conjunto de permissões, e os membros da sua organização podem ser atribuídos a uma ou mais funções, dependendo do escopo de acesso de que precisam.

Para começar, selecione **[!UICONTROL Grupo Funcional ACME]** do do **[!UICONTROL Funções]** página.

![Imagem mostrando a Função comercial ACME que está sendo selecionada nas Funções](../images/abac-end-to-end-user-guide/abac-select-role.png)

Em seguida, selecione **[!UICONTROL Rótulos]** e selecione **[!UICONTROL Adicionar rótulos]**.

![Imagem mostrando Adicionar rótulos sendo selecionados na guia Rótulos](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Uma lista de todos os rótulos na sua organização é exibida. Selecionar **[!UICONTROL RHD]** para adicionar o rótulo a **[!UICONTROL PHI/Dados de saúde regulamentados]**. Aguarde alguns momentos para que uma marca de seleção azul apareça ao lado do rótulo e selecione **[!UICONTROL Salvar]**.

![Imagem que mostra o rótulo RHD selecionado e salvo](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Ao adicionar um grupo de organizações a uma função, todos os usuários nesse grupo serão adicionados à função. Quaisquer alterações no grupo de organizações (usuários removidos ou adicionados) serão automaticamente atualizadas na função.

## Aplicar rótulos a campos de esquema {#label-resources}

Agora que você configurou uma função de usuário com o [!UICONTROL RHD] rótulo, a próxima etapa é adicionar esse mesmo rótulo aos recursos que você deseja controlar para essa função.

Selecionar **[!UICONTROL Esquemas]** na navegação à esquerda e selecione **[!UICONTROL ACME Healthcare]** na lista de schemas exibidos.

![Imagem mostrando o esquema do ACME Healthcare que está sendo selecionado na guia Esquemas](../images/abac-end-to-end-user-guide/abac-select-schema.png)

Em seguida, selecione **[!UICONTROL Rótulos]** para ver uma lista que exibe os campos associados ao esquema. Aqui, é possível atribuir rótulos a um ou vários campos de uma só vez. Selecione o **[!UICONTROL Glicose no sangue]** e **[!UICONTROL Nível de insulina]** e selecione **[!UICONTROL Aplicar rótulos de acesso e governança de dados]**.

![Imagem que mostra os rótulos BloodGlucose e InsulinLevel sendo selecionados e aplicar acesso e governança de dados sendo selecionados](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

A variável **[!UICONTROL Editar rótulos]** será exibida, permitindo que você escolha os rótulos que deseja aplicar aos campos do esquema. Para esse caso de uso, selecione a variável **[!UICONTROL PHI/ Dados de saúde regulamentados]** rótulo e selecione **[!UICONTROL Salvar]**.

![Imagem que mostra o rótulo RHD selecionado e salvo](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Quando um rótulo é adicionado a um campo, esse rótulo é aplicado ao recurso principal desse campo (uma classe ou um grupo de campos). Se a classe pai ou o grupo de campos for empregado por outros esquemas, esses esquemas herdarão o mesmo rótulo.

## Aplicar rótulos a segmentos

Depois de concluir a rotulagem dos campos de esquema, você pode começar a rotular os segmentos.

Selecionar **[!UICONTROL Segmentos]** no painel de navegação esquerdo. Uma lista de segmentos disponíveis em sua organização é exibida. Neste exemplo, os dois segmentos a seguir devem ser rotulados como se contivessem dados confidenciais de integridade:

* Glicose no Sangue >100
* Insulina &lt;50

Selecionar **[!UICONTROL Glicose no Sangue >100]** para começar a rotular o segmento.

![Imagem mostrando a glicose >100 sendo selecionada na guia Segmentos](../images/abac-end-to-end-user-guide/abac-select-segment.png)

O segmento **[!UICONTROL Detalhes]** é exibida. Selecionar **[!UICONTROL Gerenciar acesso]**.

![Imagem mostrando a seleção do acesso Gerencia](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

A variável **[!UICONTROL Editar rótulos]** será exibida, permitindo que você escolha os rótulos que deseja aplicar ao segmento. Para esse caso de uso, selecione a variável **[!UICONTROL PHI/ Dados de saúde regulamentados]** rótulo e selecione **[!UICONTROL Salvar]**.

![Imagem mostrando a seleção do rótulo RHD e salvando a seleção](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Repita as etapas acima com **[!UICONTROL Insulina &lt;50]**.

## Ativar a política de controle de acesso {#policy}

A política de controle de acesso padrão aproveitará os rótulos para definir quais funções de usuário têm acesso a recursos específicos da plataforma. Neste exemplo, o acesso a campos e segmentos de esquema será negado em todas as sandboxes para usuários que não estejam em uma função que tenha os rótulos correspondentes no campo de esquema.

Para ativar a política de controle de acesso, selecione [!UICONTROL Permissões] na navegação à esquerda e selecione **[!UICONTROL Políticas]**.

![Lista de políticas exibidas](../images/abac-end-to-end-user-guide/abac-policies-page.png)

Em seguida, selecione as reticências (`...`) ao lado do nome das políticas, e uma lista suspensa exibe controles para editar, ativar, excluir ou duplicar a função. Selecionar **[!UICONTROL Ativar]** na lista suspensa.

![Lista suspensa para ativar a política](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

A caixa de diálogo ativar política é exibida, solicitando que você confirme a ativação. Selecionar **[!UICONTROL Confirmar o]**.

![Caixa de diálogo Ativar política](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

A confirmação da ativação da política é recebida e você retorna ao [!UICONTROL Políticas] página.

![Ativar confirmação de política](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Próximas etapas

Você concluiu a aplicação de rótulos a uma função, campos de esquema e segmentos. A agência externa atribuída a essas funções tem restrições para visualizar esses rótulos e seus valores no esquema, conjunto de dados e exibição de perfil. Esses campos também não podem ser usados na definição do segmento ao usar o Construtor de segmentos.

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte [visão geral do controle de acesso baseado em atributos](./overview.md).

O vídeo a seguir é destinado a ajudá-lo a entender o controle de acesso baseado em atributos e descreve como configurar funções, recursos e políticas.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)
