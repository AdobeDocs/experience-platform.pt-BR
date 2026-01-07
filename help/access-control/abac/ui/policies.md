---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;controle de acesso baseado em atributo;;home;popular topics;access control;attribute-based access control;ABAC
title: Gerenciar políticas de controle de acesso
description: Gerencie políticas de controle de acesso por meio da interface de Permissões no Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 8%

---

# Gerenciar políticas de controle de acesso

As políticas de controle de acesso são declarações que reúnem atributos para estabelecer ações permitidas e inadmissíveis. A Adobe fornece uma política padrão que pode ser ativada imediatamente ou quando sua organização estiver pronta para começar a controlar o acesso a objetos específicos com base em [rótulos](./labels.md){target="_blank"}. A política padrão, **[!UICONTROL Default-Label-Based-Access-Control-Policy]**, usa rótulos aplicados a recursos para negar acesso, a menos que os usuários estejam em uma função com um rótulo correspondente.

>[!IMPORTANT]
>
>As políticas de controle de acesso não devem ser confundidas com as políticas de uso de dados, que controlam como os dados são usados no Adobe Experience Platform. Consulte o manual sobre como criar [políticas de uso de dados](../../../data-governance/policies/create.md){target="_blank"} para obter mais informações.

## Configurar sandboxes para uma política {#configure-policy}

As políticas são aplicadas no nível da sandbox para controlar quais sandboxes impõem controle de acesso baseado em rótulo. Por padrão, o recurso **[!UICONTROL Auto-include]** está ativado, o que significa que todas as sandboxes atuais e futuras são automaticamente adicionadas à política. Quando **[!UICONTROL Auto-include]** estiver desativado, somente as sandboxes adicionadas manualmente estarão sujeitas às regras de controle de acesso da política.

>[!NOTE]
>
>A política **[!UICONTROL Default-Label-Based-Access-Control-Policy]** é a única disponível para configuração no momento.

Para começar a configurar as sandboxes de uma política, navegue até **[!UICONTROL Permissions]** no [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Selecione **[!UICONTROL Policies]** no painel esquerdo e, em seguida, selecione **[!UICONTROL Default-Label-Based-Access-Control-Policy]** na lista.

![O espaço de trabalho de políticas mostrando uma lista de políticas existentes.](../../images/ui/policies/policies-home.png){zoomable="yes"}

O espaço de trabalho de detalhes da política é exibido. Selecione a guia **[!UICONTROL Sandboxes]** para exibir a lista de sandboxes associadas à política e acessar as opções de configuração da sandbox.

![O espaço de trabalho da sandbox da política mostrando uma lista de sandboxes associadas.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Gerenciar inclusão automática {#manage-auto-include}

>[!IMPORTANT]
>
>Por padrão, **[!UICONTROL Auto-include]** está ativado, o que significa que todas as sandboxes atuais e futuras são automaticamente adicionadas à política.

Para controlar quais sandboxes estão incluídas em uma política, você pode ativar ou desativar o recurso **[!UICONTROL Auto-include]**. Ao desligar **[!UICONTROL Auto-include]**, sandboxes futuras não serão adicionadas automaticamente à política. No entanto, a desativação do recurso **não** removerá sandboxes que já estejam incluídas na política.

![A guia da sandbox da política com a opção Incluir automaticamente realçada e no estado &quot;desligado&quot;.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Para habilitar novamente **[!UICONTROL Auto-include]**, use o botão para ativá-lo novamente. A caixa de diálogo **[!UICONTROL Enable Auto-include]** é exibida solicitando que você confirme sua seleção. Selecione **[!UICONTROL Enable]** para concluir a definição de configuração.

>[!NOTE]
>
>Quando você reabilitar **[!UICONTROL Auto-include]**, todas as sandboxes removidas anteriormente da política serão adicionadas novamente.

![A caixa de diálogo Habilitar Inclusão Automática com a opção Habilitar foi realçada.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Gerenciar sandboxes manualmente {#manually-manage-sandboxes}

Quando **[!UICONTROL Auto-include]** está desativado, você pode adicionar ou remover manualmente sandboxes específicas da política. Isso oferece controle preciso sobre quais sandboxes aplicam as regras de controle de acesso da política.

>[!NOTE]
>
>Para adicionar ou remover sandboxes manualmente, a opção **[!UICONTROL Auto-include]** de **deve** estar desativada.

**Para adicionar sandboxes:**

Selecione **[!UICONTROL Add Sandboxes]** no espaço de trabalho de sandbox da política.

![Espaço de trabalho da política com a opção Adicionar Sandboxes realçada.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

A caixa de diálogo **[!UICONTROL Add Sandboxes]** é exibida, exibindo sua biblioteca de sandboxes disponíveis. Selecione as sandboxes que deseja adicionar à política e selecione **[!UICONTROL Save]**.

![A caixa de diálogo Adicionar Sandboxes com uma sandbox selecionada e a opção Salvar realçada.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Se todas as sandboxes disponíveis já estiverem incluídas na política, você verá a mensagem &quot;Você não tem nada na biblioteca&quot; na caixa de diálogo.

**Para remover sandboxes:**

Localize a sandbox que você deseja remover da lista e selecione o ícone **X** ao lado do nome.

![A lista de sandbox da política com um &quot;x&quot; realçado para remover uma sandbox.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

Uma caixa de diálogo de confirmação será exibida. Selecione **[!UICONTROL Confirm]** para concluir a remoção da sandbox da política.

![Uma caixa de diálogo de confirmação da sandbox com a opção Confirmar foi realçada.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Ativar uma política {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="O que são políticas?"
>abstract="Políticas são declarações que reúnem atributos para estabelecer ações permitidas e não permitidas. Cada organização possui uma política padrão que você deve ativar para começar a controlar o acesso a objetos específicos com base em rótulos. Os rótulos aplicados aos recursos negam o acesso, a menos que os usuários sejam atribuídos a uma função com um rótulo correspondente. As políticas não podem ser editadas ou excluídas, mas podem ser ativadas ou desativadas."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Gerenciar rótulos"

Para ativar uma política existente, selecione a política na guia **[!UICONTROL Policies]** em **[!UICONTROL Permissions]**. O status de ativação da política está visível na seção **[!UICONTROL Status]**.

![O espaço de trabalho de políticas com o status de uma política realçado.](../../images/ui/policies/policy-status.png){zoomable="yes"}

O espaço de trabalho de detalhes da política será exibido. Selecione **[!UICONTROL Activate]**.

![O espaço de trabalho de detalhes da política com a opção Ativar realçada.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

A caixa de diálogo **[!UICONTROL Activate Policy]** é exibida. Selecione **[!UICONTROL Confirm]** para concluir a ativação da política.

![A caixa de diálogo Ativar Política com a opção Confirmar foi realçada.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Próximas etapas

Com uma política ativada, você pode prosseguir para a próxima etapa para [gerenciar permissões para uma função](permissions.md).
