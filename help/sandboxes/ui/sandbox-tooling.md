---
title: Ferramentas de sandboxes
description: Exporte e importe configurações de sandbox facilmente entre sandboxes.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 8%

---


# [!BADGE Beta] Ferramentas de sandbox

>[!IMPORTANT]
>
>A variável **Ferramentas de sandbox** O recurso descrito abaixo está disponível somente para clientes Beta selecionados.

>[!NOTE]
>
>As ferramentas de sandbox são um recurso fundamental que oferece suporte [!DNL Real-Time Customer Data Platform] e [!DNL Journey Optimizer] para melhorar a eficiência do ciclo de desenvolvimento e a precisão da configuração.<br><br>Você precisa ter as duas seguintes permissões de controle de acesso baseado em função para usar o recurso de ferramenta sandbox:<br>- `manage-sandbox` ou `view-sandbox`<br>- `manage-package`

Melhore a precisão da configuração em sandboxes e exporte e importe configurações de sandbox facilmente entre sandboxes com o recurso de ferramenta de sandbox. Use as ferramentas de sandbox para reduzir o tempo de retorno do processo de implementação e mover configurações bem-sucedidas entre sandboxes.

Você pode usar o recurso de ferramenta sandbox para selecionar objetos diferentes e exportá-los em um pacote. Um pacote pode consistir em um único objeto, vários objetos ou em uma sandbox inteira. Todos os objetos incluídos em um pacote devem ser da mesma sandbox.

## Objetos compatíveis com as ferramentas de sandbox {#supported-objects}

A tabela abaixo lista os objetos atualmente compatíveis com as ferramentas de sandbox:

| Plataforma | Objeto |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Jornadas |
| Plataforma de dados do cliente | Origens |
| Plataforma de dados do cliente | Segmentos |
| Plataforma de dados do cliente | Identidades |
| Plataforma de dados do cliente | Políticas |
| Plataforma de dados do cliente | Esquemas |
| Plataforma de dados do cliente | Conjuntos de dados |

Os seguintes objetos são importados, mas estão com status de rascunho ou desativado:

| Recurso | Objeto | Status |
| --- | --- | --- |
| Status da importação | Fluxo de dados de origem | Rascunho |
| Status da importação | Jornada | Rascunho |
| Perfil unificado | Esquema | Desativado |
| Perfil unificado | Conjunto de dados | Desativado |
| Políticas | Políticas de consentimento | Desativado |
| Políticas | Políticas de governança de dados | Desativado |

Os casos de borda listados abaixo não estão incluídos no pacote:

* Relacionamentos de esquema

## Exportar objetos em um pacote {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Salvar e sair do pacote"
>abstract="Para sair do pacote e salvar, simplesmente use a opção voltar."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Remover um objeto"
>abstract="É necessário selecionar a linha e usar a opção de exclusão (disponibilizada após a seleção) para remover a linha."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Configurações de expiração do pacote"
>abstract="A data é definida para 90 dias a partir de hoje. Essa data continua sendo alterada até que o pacote seja publicado. Se você visitar o pacote com o status de rascunho amanhã, a data será movida em +1 dia (a menos que definida pelo usuário ou usuária)."

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

## Exportar e importar uma sandbox inteira

### Exportar uma sandbox inteira {#export-entire-sandbox}

Para exportar uma sandbox inteira, navegue até a [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]** e selecione **[!UICONTROL Criar pacote]**.

![A variável [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]** realce da guia [!UICONTROL Criar pacote].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Selecionar **[!UICONTROL Sandbox inteira]** para o Tipo de pacote no [!UICONTROL Criar pacote] diálogo. Forneça um [!UICONTROL Nome do pacote] para o pacote e selecione o **[!UICONTROL Sandbox]** na lista suspensa. Finalmente, selecione **[!UICONTROL Criar]** para confirmar as entradas.

![A variável [!UICONTROL Criar pacote] caixa de diálogo mostrando campos concluídos e realces [!UICONTROL Criar].](../images/ui/sandbox-tooling/create-package-dialog.png)

O pacote é criado com sucesso, selecione **[!UICONTROL Publish]** para publicar o pacote.

![Lista de pacotes de sandbox destacando o novo pacote publicado.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Você retornará à janela **[!UICONTROL Pacotes]** na guia [!UICONTROL Sandboxes] ambiente, onde é possível ver o novo pacote publicado.

### Importar todo o pacote de sandbox {#import-entire-sandbox-package}

Para importar o pacote para uma sandbox de destino, navegue até a [!UICONTROL Sandboxes] **[!UICONTROL Procurar]** e selecione a opção de sinal de mais (+) ao lado do nome da sandbox.

![As sandboxes **[!UICONTROL Procurar]** guia destacando a seleção do pacote de importação.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Usando o menu suspenso, selecione a sandbox completa usando a **[!UICONTROL Nome do pacote]** lista suspensa. Adicione um opcional **[!UICONTROL Nome do trabalho]**, que será usado para monitoramento futuro, selecione **[!UICONTROL Próxima]**.

![A página de detalhes da importação mostrando o [!UICONTROL Nome do pacote] seleção suspensa](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Todos os objetos são criados como novos no pacote ao importar uma sandbox inteira. Os objetos não estão listados na variável [!UICONTROL Objeto e dependências do pacote] página, pois pode haver vários. Uma mensagem em linha é exibida, avisando sobre tipos de objetos que não são compatíveis.

Você é levado para o [!UICONTROL Objeto e dependências do pacote] página na qual você pode ver o número de objetos e dependências importados e excluídos. Aqui, selecione **[!UICONTROL Importar]** para concluir a importação do pacote.

![A variável [!UICONTROL Objeto e dependências do pacote] mostra a mensagem embutida de tipos de objeto não suportados, destacando [!UICONTROL Importar].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

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

## Próximas etapas

Este documento demonstrou como usar o recurso de ferramenta sandbox na interface do usuário do Experience Platform. Para obter informações sobre sandboxes, consulte o [guia do usuário de sandbox](../ui/user-guide.md).

Para obter etapas sobre como executar operações diferentes usando a API de sandbox, consulte a [guia do desenvolvedor de sandbox](../api/getting-started.md). Para obter uma visão geral de alto nível das sandboxes no Experience Platform, consulte o [documentação de visão geral](../home.md).
