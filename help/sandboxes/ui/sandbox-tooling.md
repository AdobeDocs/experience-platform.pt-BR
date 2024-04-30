---
title: Ferramentas de sandboxes
description: Exporte e importe configurações de sandbox facilmente entre sandboxes.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 1a474fa0947cb930bad95f94c1901fffb7e23e7b
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 7%

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
| Plataforma de dados do cliente | Públicos-alvo | Somente o **[!UICONTROL Público-alvo do cliente]** type **[!UICONTROL Serviço de segmentação]** é compatível. Os rótulos existentes para consentimento e governança serão copiados no mesmo trabalho de importação. O sistema selecionará automaticamente a Política de mesclagem padrão na sandbox de destino com a mesma classe XDM ao verificar as dependências da política de mesclagem. |
| Plataforma de dados do cliente | Identidades | O sistema deduplicará automaticamente os namespaces de identidade padrão do Adobe ao criar na sandbox de destino. Os públicos só podem ser copiados quando todos os atributos nas regras de público-alvo estão habilitados no esquema de união. Os esquemas necessários devem ser movidos e ativados para o perfil unificado primeiro. |
| Plataforma de dados do cliente | Esquemas | Os rótulos existentes para consentimento e governança serão copiados no mesmo trabalho de importação. O usuário tem a flexibilidade de importar esquemas sem a opção Perfil unificado ativada. O caso de borda das relações de esquema não está incluído no pacote. |
| Plataforma de dados do cliente | Conjuntos de dados | Os conjuntos de dados são copiados com a configuração de perfil unificado desativada por padrão. |
| Plataforma de dados do cliente | Políticas de consentimento e governança | Adicionar políticas personalizadas criadas por um usuário a um pacote e movê-las para sandboxes. |

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
| [!DNL Adobe Journey Optimizer] | Política de mesclagem | As políticas de mesclagem usadas na jornada podem ser copiadas como objetos dependentes. Na sandbox do Target, você **não é possível** criar uma nova política de mesclagem, você só pode utilizar uma já existente. |
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

Usando o menu suspenso, selecione a variável **[!UICONTROL Nome do pacote]** você deseja importar para a sandbox de destino. Adicione um opcional **[!UICONTROL Nome do trabalho]**, que serão usados para monitoramento futuro. Por padrão, o perfil unificado será desativado quando os schemas do pacote forem importados. Alternar **Ativar esquemas para o perfil** para habilitar isso, selecione **[!UICONTROL Próxima]**.

![A página de detalhes da importação mostrando o [!UICONTROL Nome do pacote] seleção suspensa](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

A variável [!UICONTROL Objeto e dependências do pacote] A página fornece uma lista de todos os ativos incluídos neste pacote. O sistema detecta automaticamente objetos dependentes que são necessários para a importação bem-sucedida de objetos pai selecionados. Todos os atributos ausentes são exibidos na parte superior da página. Selecionar **[!UICONTROL Exibir detalhes]** para obter uma análise mais detalhada.

![A variável [!UICONTROL Objeto e dependências do pacote] mostra os atributos ausentes.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Objetos dependentes podem ser substituídos por objetos existentes na sandbox de destino, o que permite reutilizar objetos existentes em vez de criar uma nova versão. Por exemplo, ao importar um pacote incluindo esquemas, você pode reutilizar grupos de campos personalizados existentes e namespaces de identidade na sandbox de destino. Como alternativa, ao importar um pacote incluindo Jornadas, você pode reutilizar segmentos existentes na sandbox de destino.

Para usar um objeto existente, selecione o ícone de lápis ao lado do objeto dependente.

![A variável [!UICONTROL Objeto e dependências do pacote] A página mostra uma lista de ativos incluídos no pacote.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

As opções para criar um novo ou usar um existente são exibidas. Selecionar **[!UICONTROL Usar existente]**.

![A variável [!UICONTROL Objeto e dependências do pacote] página mostrando opções de objeto dependente [!UICONTROL Criar novo] e [!UICONTROL Usar existente].](../images/ui/sandbox-tooling/use-existing-object.png)

A variável **[!UICONTROL Grupo de campos]** mostra uma lista de grupos de campos disponíveis para o objeto. Selecione os grupos de campos necessários e selecione **[!UICONTROL Salvar]**.

![Uma lista de campos mostrados na variável [!UICONTROL Grupo de campos] , destacando o [!UICONTROL Salvar] seleção. ](../images/ui/sandbox-tooling/field-group-list.png)

Você retornará à janela [!UICONTROL Objeto e dependências do pacote] página. Aqui, selecione **[!UICONTROL Concluir]** para concluir a importação do pacote.

![A variável [!UICONTROL Objeto e dependências do pacote] mostra uma lista de ativos incluídos no pacote, destacando [!UICONTROL Concluir].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportar e importar uma sandbox inteira

>[!NOTE]
>
>Somente objetos da plataforma de dados do cliente em tempo real são compatíveis com uma exportação/importação de sandbox completa. Os objetos de jornada não serão incluídos.

### Exportar uma sandbox inteira {#export-entire-sandbox}

Para exportar uma sandbox inteira, navegue até a [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]** e selecione **[!UICONTROL Criar pacote]**.

![A variável [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]** realce da guia [!UICONTROL Criar pacote].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Selecionar **[!UICONTROL Sandbox inteira]** para o [!UICONTROL Tipo de pacote] no [!UICONTROL Criar pacote] diálogo. Forneça um [!UICONTROL Nome do pacote] para o novo pacote e selecione a variável **[!UICONTROL Sandbox]** na lista suspensa. Finalmente, selecione **[!UICONTROL Criar]** para confirmar as entradas.

![A variável [!UICONTROL Criar pacote] caixa de diálogo mostrando campos concluídos e realces [!UICONTROL Criar].](../images/ui/sandbox-tooling/create-package-dialog.png)

O pacote é criado com sucesso, selecione **[!UICONTROL Publish]** para publicar o pacote.

![Lista de pacotes de sandbox destacando o novo pacote publicado.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Você retornará à janela **[!UICONTROL Pacotes]** na guia [!UICONTROL Sandboxes] ambiente, onde é possível ver o novo pacote publicado.

### Importar todo o pacote de sandbox {#import-entire-sandbox-package}

>[!NOTE]
>
>Todos os objetos serão importados para a sandbox de destino como novos objetos. É uma prática recomendada importar um pacote de sandbox completo para uma sandbox vazia.

Para importar o pacote para uma sandbox de destino, navegue até a [!UICONTROL Sandboxes] **[!UICONTROL Procurar]** e selecione a opção de sinal de mais (+) ao lado do nome da sandbox.

![As sandboxes **[!UICONTROL Procurar]** guia destacando a seleção do pacote de importação.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Usando o menu suspenso, selecione a sandbox completa usando a **[!UICONTROL Nome do pacote]** lista suspensa. Adicionar um **[!UICONTROL Nome do trabalho]**, que serão utilizados para monitoramento futuro e uma **[!UICONTROL Descrição do trabalho]** e selecione **[!UICONTROL Próxima]**.

![A página de detalhes da importação mostrando o [!UICONTROL Nome do pacote] seleção suspensa](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Você deve ter permissões totais para todos os objetos incluídos no pacote. Se você não tiver permissões, a operação de importação falhará e serão exibidas mensagens de erro.

Você é levado para o [!UICONTROL Objeto e dependências do pacote] página na qual você pode ver o número de objetos e dependências importados e excluídos. Aqui, selecione **[!UICONTROL Importar]** para concluir a importação do pacote.

![A variável [!UICONTROL Objeto e dependências do pacote] mostra a mensagem embutida de tipos de objeto não suportados, destacando [!UICONTROL Importar].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Aguarde algum tempo para a conclusão da importação. O tempo de conclusão pode variar dependendo do número de objetos no pacote. É possível monitorar o trabalho de importação do [!UICONTROL Sandboxes] **[!UICONTROL Tarefas]** guia.

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

## Monitorar detalhes da importação {#view-import-details}

Para exibir os detalhes importados, navegue até o [!UICONTROL Sandboxes] **[!UICONTROL Tarefas]** e selecione o pacote na lista. Como alternativa, use a barra de pesquisa para procurar o pacote.

![As sandboxes [!UICONTROL Tarefas] A guia destaca a seleção do pacote de importação.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Selecionar **[!UICONTROL Exibir resumo de importação]** no painel direito de detalhes da **[!UICONTROL Tarefas]** no ambiente Sandboxes.

![As sandboxes [!UICONTROL Importações] A guia destaca a [!UICONTROL Exibir detalhes da importação] no painel direito.](../images/ui/sandbox-tooling/view-import-details.png)

A variável **[!UICONTROL Importar resumo]** A caixa de diálogo mostra um detalhamento das importações com o progresso como uma porcentagem.

>[!NOTE]
>
>Você pode ver uma lista de objetos navegando até páginas específicas do inventário.

![A variável [!UICONTROL Detalhes da importação] mostrando uma análise detalhada das importações.](../images/ui/sandbox-tooling/import-details.png)

Quando a importação for concluída, uma notificação será recebida na interface do usuário da plataforma. Você pode acessar essas notificações pelo ícone de alertas. Você pode acessar a solução de problemas aqui se uma tarefa não for bem-sucedida.

## Tutorial em vídeo

O vídeo a seguir é destinado a ajudá-lo a entender as ferramentas de sandbox e descreve como criar um novo pacote, publicar um pacote e importar um pacote.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Próximas etapas

Este documento demonstrou como usar o recurso de ferramenta sandbox na interface do usuário do Experience Platform. Para obter informações sobre sandboxes, consulte o [guia do usuário de sandbox](../ui/user-guide.md).

Para obter etapas sobre como executar operações diferentes usando a API de sandbox, consulte a [guia do desenvolvedor de sandbox](../api/getting-started.md). Para obter uma visão geral de alto nível das sandboxes no Experience Platform, consulte o [documentação de visão geral](../home.md).
