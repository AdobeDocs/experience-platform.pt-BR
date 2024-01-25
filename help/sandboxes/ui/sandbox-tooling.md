---
title: Ferramentas de sandboxes
description: Exporte e importe configurações de sandbox facilmente entre sandboxes.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 1f7b7f0486d0bb2774f16a766c4a5af6bbb8848a
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 9%

---

# Ferramentas de sandbox

>[!NOTE]
>
>As ferramentas de sandbox são um recurso fundamental que oferece suporte [!DNL Real-Time Customer Data Platform] e [!DNL Journey Optimizer] para melhorar a eficiência do ciclo de desenvolvimento e a precisão da configuração.<br><br>Você precisa ter as duas seguintes permissões de controle de acesso baseado em função para usar o recurso de ferramenta sandbox:<br>- `manage-sandbox` ou `view-sandbox`<br>- `manage-package`

Melhore a precisão da configuração em sandboxes e exporte e importe configurações de sandbox facilmente entre sandboxes com o recurso de ferramenta de sandbox. Use as ferramentas de sandbox para reduzir o tempo de retorno do processo de implementação e mover configurações bem-sucedidas entre sandboxes.

Você pode usar o recurso de ferramenta sandbox para selecionar objetos diferentes e exportá-los em um pacote. Um pacote pode consistir em um único objeto ou em vários objetos. <!--or an entire sandbox.-->Todos os objetos incluídos em um pacote devem ser da mesma sandbox.

## Objetos compatíveis com as ferramentas de sandbox {#supported-objects}

O recurso de ferramenta sandbox oferece a capacidade de exportar [!DNL Adobe Real-Time Customer Data Platform] e [!DNL Adobe Journey Optimizer] objetos em um pacote.

### Objetos do Real-time Customer Data Platform {#real-time-cdp-objects}

A tabela abaixo lista [!DNL Adobe Real-Time Customer Data Platform] objetos atualmente compatíveis com as ferramentas de sandbox:

| Plataforma | Objeto | Detalhes |
| --- | --- | --- |
| Plataforma de dados do cliente | Origens | As credenciais da conta de origem não são replicadas na sandbox de destino por motivos de segurança e precisarão ser atualizadas manualmente. O fluxo de dados de origem é copiado em um status de rascunho por padrão. |
| Plataforma de dados do cliente | Públicos-alvo | Somente o **[!UICONTROL Público-alvo do cliente]** type **[!UICONTROL Serviço de segmentação]** é compatível. Os rótulos existentes para consentimento e governança serão copiados no mesmo trabalho de importação. |
| Plataforma de dados do cliente | Identidades | O sistema deduplicará automaticamente os namespaces de identidade padrão do Adobe ao criar na sandbox de destino. Os públicos só podem ser copiados quando todos os atributos nas regras de público-alvo estão habilitados no esquema de união. Os esquemas necessários devem ser movidos e ativados para o perfil unificado primeiro. |
| Plataforma de dados do cliente | Esquemas | Os rótulos existentes para consentimento e governança serão copiados no mesmo trabalho de importação. O status do perfil unificado do esquema será copiado como está da sandbox de origem. Se o esquema estiver ativado para o perfil unificado na sandbox de origem, todos os atributos serão movidos para o esquema de união. O caso de borda das relações de esquema não está incluído no pacote. |
| Plataforma de dados do cliente | Conjuntos de dados | Os conjuntos de dados são copiados com a configuração de perfil unificado desativada por padrão. |

Os seguintes objetos são importados, mas estão em um rascunho ou estão desabilitados:

| Recurso | Objeto | Status |
| --- | --- | --- |
| Status da importação | Fluxo de dados de origem | Rascunho |
| Status da importação | Jornada | Rascunho |
| Perfil unificado | Conjunto de dados | Perfil unificado desabilitado |
| Políticas | Políticas de governança de dados | Desabilitado |

### Objetos do Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

A tabela abaixo lista [!DNL Adobe Journey Optimizer] objetos atualmente compatíveis com ferramentas e limitações de sandbox:

| Plataforma | Objeto | Detalhes |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Público-alvo | Um público-alvo pode ser copiado como um objeto dependente do objeto de jornada. Você pode selecionar criar um novo público ou reutilizar um existente na sandbox de destino. |
| [!DNL Adobe Journey Optimizer] | Esquema | Os esquemas usados na jornada podem ser copiados como objetos dependentes. Você pode selecionar criar um novo esquema ou reutilizar um existente na sandbox de destino. |
| [!DNL Adobe Journey Optimizer] | Jornada - detalhes da tela | A representação da jornada na tela inclui os objetos na jornada, como condições, ações, eventos, públicos-alvo de leitura e assim por diante, que são copiados. A atividade de salto é excluída da cópia. |
| [!DNL Adobe Journey Optimizer] | Evento | Os eventos e detalhes do evento usados na jornada são copiados. Ele sempre criará uma nova versão na sandbox de destino. |
| [!DNL Adobe Journey Optimizer] | Ação | As mensagens de email e de push usadas na jornada podem ser copiadas como objetos dependentes. As atividades de ação de canal usadas nos campos de jornada, que são usadas para personalização na mensagem, não são verificadas para verificação de integridade. Os blocos de conteúdo não são copiados.<br><br>A ação de perfil de atualização usada na jornada pode ser copiada. Ações personalizadas e detalhes de ação usados na jornada também são copiados. Ele sempre criará uma nova versão na sandbox de destino. |

As superfícies (por exemplo, predefinições) não são copiadas. O sistema seleciona automaticamente a correspondência mais próxima possível na sandbox de destino com base no tipo de mensagem e no nome da superfície. Se não houver superfícies encontradas na sandbox de destino, a cópia de superfície falhará, fazendo com que a cópia da mensagem falhe, pois uma mensagem requer que uma superfície esteja disponível para configuração. Nesse caso, pelo menos uma superfície precisa ser criada para o canal direito da mensagem para que a cópia funcione.

Os tipos de identidade personalizados não são suportados como objetos dependentes ao exportar uma jornada.

## Exportar objetos em um pacote {#export-objects}

>[!NOTE]
>
>Todas as ações de exportação são registradas nos logs de auditoria.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Remover um objeto"
>abstract="Para remover um objeto do pacote, selecione a linha a ser removida e use a opção Excluir disponibilizada após a seleção. Observe que não é possível remover objetos de pacotes publicados."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Configurações de expiração do pacote"
>abstract="Os pacotes estão definidos para expirar após um período de inatividade no status de rascunho. O prazo padrão é de 90 dias a partir do dia atual. Essa data continua sendo alterada até que o pacote seja publicado. Se você visitar o pacote com status de rascunho amanhã, a data será alterada em +1 dia, a menos que você defina manualmente."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Status do pacote"
>abstract="Por padrão, o status é definido como rascunho. Após a publicação do pacote, o status é alterado para publicado. Não é possível fazer alterações após a publicação do pacote."

>[!NOTE]
>
>Você só poderá importar um pacote se tiver permissão para acessar os objetos.

Este exemplo documenta o processo de exportação de um esquema e sua adição a um pacote. Você pode usar o mesmo processo para exportar outros objetos, por exemplo, conjuntos de dados, jornadas e muito mais.

### Adicionar objeto a um novo pacote {#add-object-to-new-package}

Selecionar **[!UICONTROL Esquemas]** na navegação à esquerda e selecione o **[!UICONTROL Procurar]** , que lista os esquemas disponíveis. Em seguida, selecione as reticências (`...`) ao lado do schema selecionado, e uma lista suspensa exibe controles. Selecionar **[!UICONTROL Adicionar ao pacote]** na lista suspensa.

![Lista de esquemas mostrando o menu suspenso destacando o [!UICONTROL Adicionar ao pacote] controle.](../images/ui/sandbox-tooling/add-to-package.png)

No **[!UICONTROL Adicionar ao pacote]** , selecione a **[!UICONTROL Criar novo pacote]** opção. Forneça um [!UICONTROL Nome] para o seu pacote e uma [!UICONTROL Descrição]e selecione **[!UICONTROL Adicionar]**.

![A variável [!UICONTROL Adicionar ao pacote] diálogo com [!UICONTROL Criar novo pacote] selecionado e realce [!UICONTROL Adicionar].](../images/ui/sandbox-tooling/create-new-package.png)

Você retornará à janela **[!UICONTROL Esquemas]** ambiente. Agora é possível adicionar outros objetos ao pacote criado seguindo as próximas etapas listadas abaixo.

### Adicionar um objeto a um pacote existente e publicar {#add-object-to-existing-package}

Para exibir uma lista de esquemas disponíveis, selecione **[!UICONTROL Esquemas]** na navegação à esquerda e selecione o **[!UICONTROL Procurar]** guia. Em seguida, selecione as reticências (`...`) ao lado do schema selecionado para ver as opções de controle em um menu suspenso. Selecionar **[!UICONTROL Adicionar ao pacote]** na lista suspensa.

![Lista de esquemas mostrando o menu suspenso destacando o [!UICONTROL Adicionar ao pacote] controle.](../images/ui/sandbox-tooling/add-to-package.png)

A variável **[!UICONTROL Adicionar ao pacote]** será exibida. Selecione o **[!UICONTROL Pacote existente]** e selecione a opção **[!UICONTROL Nome do pacote]** e selecione o pacote necessário. Finalmente, selecione **[!UICONTROL Adicionar]** para confirmar suas escolhas.

![[!UICONTROL Adicionar ao pacote] , mostrando um pacote selecionado na lista suspensa.](../images/ui/sandbox-tooling/add-to-existing-package.png)

A lista de objetos adicionados ao pacote é listada. Para publicar o pacote e disponibilizá-lo para importação em sandboxes, selecione **[!UICONTROL Publish]**.

![Uma lista de objetos no pacote, destacando o [!UICONTROL Publish] opção.](../images/ui/sandbox-tooling/publish-package.png)

Selecionar **[!UICONTROL Publish]** para confirmar a publicação do pacote.

![Caixa de diálogo de confirmação Publicar pacote, destacando o [!UICONTROL Publish] opção.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Após a publicação, o conteúdo do pacote não pode ser alterado. Para evitar problemas de compatibilidade, verifique se todos os ativos necessários foram selecionados. Se for necessário fazer alterações, você precisará criar um novo pacote.

Você retornará à janela **[!UICONTROL Pacotes]** na guia [!UICONTROL Sandboxes] ambiente, onde é possível ver o novo pacote publicado.

![Lista de pacotes de sandbox destacando o novo pacote publicado.](../images/ui/sandbox-tooling/published-packages.png)

## Importar um pacote para uma sandbox de destino {#import-package-to-target-sandbox}

>[!NOTE]
>
>Todas as ações de importação são registradas nos logs de auditoria.

Para importar o pacote para uma sandbox de destino, navegue até as Sandboxes **[!UICONTROL Procurar]** e selecione a opção de sinal de mais (+) ao lado do nome da sandbox.

![As sandboxes **[!UICONTROL Procurar]** guia destacando a seleção do pacote de importação.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Usando o menu suspenso, selecione a variável **[!UICONTROL Nome do pacote]** você deseja importar para a sandbox de destino. Adicione um opcional **[!UICONTROL Nome do trabalho]**, que será usado para monitoramento futuro, selecione **[!UICONTROL Próxima]**.

![A página de detalhes da importação mostrando o [!UICONTROL Nome do pacote] seleção suspensa](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

A variável [!UICONTROL Objeto e dependências do pacote] A página fornece uma lista de todos os ativos incluídos neste pacote. O sistema detecta automaticamente objetos dependentes que são necessários para a importação bem-sucedida de objetos pai selecionados.

![A variável [!UICONTROL Objeto e dependências do pacote] A página mostra uma lista de ativos incluídos no pacote.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Objetos dependentes podem ser substituídos por objetos existentes na sandbox de destino, o que permite reutilizar objetos existentes em vez de criar uma nova versão. Por exemplo, ao importar um pacote incluindo esquemas, você pode reutilizar grupos de campos personalizados existentes e namespaces de identidade na sandbox de destino. Como alternativa, ao importar um pacote incluindo Jornadas, você pode reutilizar segmentos existentes na sandbox de destino.

Para usar um objeto existente, selecione o ícone de lápis ao lado do objeto dependente. As opções para criar um novo ou usar um existente são exibidas. Selecionar **[!UICONTROL Usar existente]**.

![A variável [!UICONTROL Objeto e dependências do pacote] página mostrando opções de objeto dependente [!UICONTROL Criar novo] e [!UICONTROL Usar existente].](../images/ui/sandbox-tooling/use-existing-object.png)

A variável **[!UICONTROL Grupo de campos]** mostra uma lista de grupos de campos disponíveis para o objeto. Selecione os grupos de campos necessários e selecione **[!UICONTROL Salvar]**.

![Uma lista de campos mostrados na variável [!UICONTROL Grupo de campos] , destacando o [!UICONTROL Salvar] seleção. ](../images/ui/sandbox-tooling/field-group-list.png)

Você retornará à janela [!UICONTROL Objeto e dependências do pacote] página. Aqui, selecione **[!UICONTROL Concluir]** para concluir a importação do pacote.

![A variável [!UICONTROL Objeto e dependências do pacote] mostra uma lista de ativos incluídos no pacote, destacando [!UICONTROL Concluir].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

<!--
## Export and import an entire sandbox 

>[!NOTE]
>
>All export and import actions are recorded in the audit logs.

### Export an entire sandbox {#export-entire-sandbox}

To export an entire sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab and select **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab highlighting [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Select **[!UICONTROL Entire sandbox]** for the Type of package in the [!UICONTROL Create package] dialog. Provide a [!UICONTROL Package name] for your package and select the **[!UICONTROL Sandbox]** from the dropdown. Finally, select **[!UICONTROL Create]** to confirm your entries.

![The [!UICONTROL Create package] dialog showing completed fields and highlighting [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

The package is created successfully, select **[!UICONTROL Publish]** to publish the package.

![List of sandbox packages highlighting the new published package.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

You are returned to the **[!UICONTROL Packages]** tab in the [!UICONTROL Sandboxes] environment, where you can see the new published package.

### Import the entire sandbox package {#import-entire-sandbox-package}

To import the package into a target sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Browse]** tab and select the plus (+) option beside the sandbox name.

![The sandboxes **[!UICONTROL Browse]** tab highlighting the import package selection.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Using the dropdown menu, select the full sandbox using the **[!UICONTROL Package name]** dropdown. Add an optional **[!UICONTROL Job name]**, which will be used for future monitoring, then select **[!UICONTROL Next]**.

![The import details page showing the [!UICONTROL Package name] dropdown selection](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>All objects are created as new from the package when importing an entire sandbox. The objects are not listed in the [!UICONTROL Package object and dependencies] page, as there can be multiples. An inline message is displayed, advising of object types that are not supported.

You are taken to the [!UICONTROL Package object and dependencies] page where you can see the number of objects and dependencies that are imported and excluded objects. From here, select **[!UICONTROL Import]** to complete the package import.

 ![The [!UICONTROL Package object and dependencies] page shows the inline message of object types not supported, highlighting [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)
-->

## Monitorar trabalhos de importação e exibir detalhes dos objetos de importação

Para exibir os objetos importados e os detalhes importados, navegue até o [!UICONTROL Sandboxes] **[!UICONTROL Importações]** e selecione o pacote na lista. Como alternativa, use a barra de pesquisa para procurar o pacote.

![As sandboxes [!UICONTROL Importações] A guia destaca a seleção do pacote de importação.](../images/ui/sandbox-tooling/imports-tab.png)

### Exibir objetos importados {#view-imported-objects}

No **[!UICONTROL Importações]** na guia [!UICONTROL Sandboxes] ambiente, selecione **[!UICONTROL Exibir objetos importados]** no painel de detalhes direito.

Selecionar **[!UICONTROL Exibir objetos importados]** no painel direito de detalhes da **[!UICONTROL Importações]** na guia [!UICONTROL Sandboxes] ambiente.

![As sandboxes [!UICONTROL Importações] A guia destaca a [!UICONTROL Exibir objetos importados] no painel direito.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use as setas para expandir objetos e ver a lista completa de campos que foram importados para o pacote.

![As sandboxes [!UICONTROL Objetos importados] mostrando uma lista de objetos importados no pacote.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Exibir detalhes da importação {#view-import-details}

Selecionar **[!UICONTROL Exibir detalhes da importação]** no painel direito de detalhes da **[!UICONTROL Importações]** no ambiente Sandboxes.

![As sandboxes [!UICONTROL Importações] A guia destaca a [!UICONTROL Exibir detalhes da importação] no painel direito.](../images/ui/sandbox-tooling/view-import-details.png)

A variável **[!UICONTROL Detalhes da importação]** mostra uma análise detalhada das importações.

![A variável [!UICONTROL Detalhes da importação] mostrando uma análise detalhada das importações.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>Quando uma importação é concluída, você recebe notificações na interface do usuário da Platform. Você pode acessar essas notificações pelo ícone de alertas. Você pode acessar a solução de problemas aqui se uma tarefa não for bem-sucedida.

## Tutorial em vídeo

O vídeo a seguir é destinado a ajudá-lo a entender as ferramentas de sandbox e descreve como criar um novo pacote, publicar um pacote e importar um pacote.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Próximas etapas

Este documento demonstrou como usar o recurso de ferramenta sandbox na interface do usuário do Experience Platform. Para obter informações sobre sandboxes, consulte o [guia do usuário de sandbox](../ui/user-guide.md).

Para obter etapas sobre como executar operações diferentes usando a API de sandbox, consulte a [guia do desenvolvedor de sandbox](../api/getting-started.md). Para obter uma visão geral de alto nível das sandboxes no Experience Platform, consulte o [documentação de visão geral](../home.md).
