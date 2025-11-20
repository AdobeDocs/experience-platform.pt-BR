---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributo;;home;popular topics;access control;attribute-based access control;ABAC
title: Gerenciar políticas de controle de acesso
description: Este documento fornece informações sobre como gerenciar políticas de controle de acesso por meio da interface de Permissões no Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: afd883c530ab1b335888e79b5f4075e774fced4b
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 11%

---

# Gerenciar políticas de controle de acesso

As políticas de controle de acesso são declarações que reúnem atributos para estabelecer ações permitidas e inadmissíveis. As políticas de acesso podem ser locais ou globais e podem substituir outras políticas. A Adobe fornece uma política padrão que pode ser ativada imediatamente ou sempre que sua organização estiver pronta para começar a controlar o acesso a objetos específicos com base em rótulos. A política padrão usa rótulos aplicados a recursos para negar acesso, a menos que os usuários estejam em uma função com um rótulo correspondente.

>[!IMPORTANT]
>
>As políticas de acesso não devem ser confundidas com as políticas de uso de dados, que controlam como os dados são usados no Adobe Experience Platform, em vez de quais usuários na organização têm acesso a eles. Consulte o manual sobre como criar [políticas de uso de dados](../../../data-governance/policies/create.md) para obter mais informações.

<!-- ## Create a new policy

To create a new policy, select the **[!UICONTROL Policies]** tab in the sidebar and select **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** dialog appears, prompting you to enter a name, and an optional description. When finished, select **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Using the dropdown arrow select if you would like to **Permit access to** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png)) a resource or **Deny access to** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) a resource.

Next, select the resource that you would like to include in the policy using the dropdown menu and search access type, read or write.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Next, using the dropdown arrow select the condition you would like to apply to this policy, **The following being true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) or **The following being false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Select the plus icon to **Add matches expression** or **Add expression group** for the resource. 

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Using the dropdown, select the **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Next, using the dropdown select the **Matches**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Next, using the dropdown, select the type of label (**[!UICONTROL Core label]** or **[!UICONTROL Custom label]**) to match the label assigned to the User in roles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finally, select the **Sandbox** that you would like the policy conditions to apply to, using the dropdown menu.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Add resource** to add more resources. Once finished, select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The new policy is successfully created, and you are redirected to the **[!UICONTROL Policies]** tab, where you will see the newly created policy appear in the list. 

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Edit a policy

To edit an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to the policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select edit from the dropdown.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

The policy permissions screen appears. Make the updates then select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The policy is successfully updated, and you are redirected to the **[!UICONTROL Policies]** tab.

## Duplicate a policy

To duplicate an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select duplicate from the dropdown.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** dialog appears, prompting you to confirm the duplication. 

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

The new policy appears in the list as a copy of the original on the **[!UICONTROL Policies]** tab.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Delete a policy

To delete an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to delete.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select delete from the dropdown.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** dialog appears, prompting you to confirm the deletion. 

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

You are returned to the **[!UICONTROL policies]** tab and a confirmation of deletion pop over appears.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png) -->

## Configurar política para uma sandbox

>[!IMPORTANT]
>
>Por padrão, o recurso [!UICONTROL Auto-include] é ativado para todos os clientes, o que significa que todas as sandboxes são adicionadas à política.

>[!NOTE]
>
>A política **[!UICONTROL Default-Label-Based-Access-Control-Policy]** é a única disponível para configuração no momento.

Para exibir sandboxes associadas a uma política, selecione a política na guia **[!UICONTROL Policies]**.

![A página de políticas mostrando uma lista de políticas existentes disponíveis.](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Em seguida, selecione a política e depois a guia **[!UICONTROL Sandboxes]**. Uma lista de sandboxes associadas à política é exibida.

![A página de políticas mostrando uma lista de políticas existentes disponíveis.](../../images/flac-ui/abac-policies-sandboxes-tab.png)

### Adicionar política a todas as sandboxes

Use o botão **[!UICONTROL Auto-include]** na guia **[!UICONTROL Sandboxes]** para ativar a política para todas as sandboxes.

![A guia [!UICONTROL Sandboxes] mostrando a alternância [!UICONTROL Auto-include].](../../images/flac-ui/abac-policies-auto-include.png)

A caixa de diálogo **[!UICONTROL Enable Auto-include]** é exibida solicitando que você confirme sua seleção. Selecione **[!UICONTROL Enable]** para concluir a definição de configuração.

![O diálogo [!UICONTROL Enable Auto-include] destacando [!UICONTROL Enable].](../../images/flac-ui/abac-policies-auto-include-enable.png)

>[!SUCCESS]
>
>A política é ativada para todas as sandboxes existentes e será adicionada automaticamente a qualquer nova sandbox quando ela estiver disponível.

### Adicionar política para selecionar sandboxes

>[!IMPORTANT]
>
>Sandboxes futuras não serão incluídas na política por padrão se o botão [!UICONTROL Auto-include] estiver desativado. Será necessário gerenciar e adicionar sandboxes manualmente à política.

Use o botão **[!UICONTROL Auto-include]** na guia **[!UICONTROL Sandboxes]** para desabilitar a política para todas as sandboxes.

![A guia [!UICONTROL Sandboxes] mostrando a alternância [!UICONTROL Auto-include].](../../images/flac-ui/abac-policies-auto-include.png)

Na guia **[!UICONTROL Sandboxes]**, selecione **[!UICONTROL Add Sandboxes]** para selecionar sandboxes às quais esta política será aplicada.

![A guia [!UICONTROL Sandboxes] mostrando uma lista de sandboxes adicionadas à política.](../../images/flac-ui/abac-policies-sandboxes-tab-add.png)

Uma lista de sandboxes é exibida. Selecione a sandbox que deseja adicionar na lista. Como alternativa, use a barra de pesquisa para pesquisar a sandbox. Selecione **[!UICONTROL Save]**.

![A página [!UICONTROL Add Sandboxes] mostrando uma lista de sandboxes existentes disponíveis para serem adicionadas à política.](../../images/flac-ui/abac-policies-sandboxes-list.png)

>[!SUCCESS]
>
>As sandboxes selecionadas foram adicionadas com sucesso à política.

### Remover sandboxes de uma política

Para remover uma sandbox, selecione o ícone **X** ao lado do nome da sandbox.

![A guia [!UICONTROL Sandboxes] mostrando uma lista de sandboxes, destacando o [!UICONTROL X] a ser excluído.](../../images/flac-ui/abac-policies-remove-sandbox-x.png)

A caixa de diálogo **[!UICONTROL Remove]** é exibida solicitando que você confirme sua seleção. Selecione **[!UICONTROL Confirm]** para concluir a remoção.

![O diálogo [!UICONTROL Remove] destacando [!UICONTROL Confirm].](../../images/flac-ui/abac-policies-remove-sandbox.png)

>[!SUCCESS]
>
>A sandbox selecionada foi removida com sucesso da política.

## Ativar uma política {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="O que são políticas?"
>abstract="Políticas são declarações que reúnem atributos para estabelecer ações permitidas e não permitidas. Cada organização possui uma política padrão que você deve ativar para começar a controlar o acesso a objetos específicos com base em rótulos. Os rótulos aplicados aos recursos negam o acesso, a menos que os usuários sejam atribuídos a uma função com um rótulo correspondente. As políticas padrão não podem ser editadas ou excluídas, mas é possível ativá-las ou desativá-las."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Gerenciar rótulos"

Para ativar uma política existente, selecione a política na guia **[!UICONTROL Policies]**.

![flac-policy-select](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Em seguida, selecione as reticências (`…`) ao lado de um nome de política, e uma lista suspensa exibe controles para editar, ativar, excluir ou duplicar a função. Selecione ativar na lista suspensa.

![flac-policy-ativate](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

A caixa de diálogo **[!UICONTROL Activate policy]** é exibida, solicitando que você confirme a ativação.

![flac-policy-ativate-confirm](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


Você retornará à guia **[!UICONTROL policies]** e uma confirmação do pop-over de ativação será exibida. O status da política é exibido como ativo.

![flac-policy-enabled](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## Próximas etapas

Com uma política ativada, você pode prosseguir para a próxima etapa para [gerenciar permissões para uma função](permissions.md).
