---
title: Expirações do conjunto de dados automatizado
description: Saiba como programar a expiração de um conjunto de dados na interface do usuário do Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 19%

---

# Expirações automatizadas de conjuntos de dados {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Excluir registros e conjuntos de dados de clientes indesejados ou expirados"
>abstract="<h2>Descrição</h2><p>Para gerenciar o ciclo de vida dos dados da Experience Platform não relacionados à conformidade regulatória, você pode excluir registros do consumidor e programar datas de expiração para os conjuntos de dados. Para criar ou gerenciar solicitações de titulares de dados, consulte o bloco de casos de uso “Respeitar solicitações de privacidade de titulares de dados”.</p>"

O espaço de trabalho [[!UICONTROL Data Lifecycle]](./overview.md) na interface do usuário do Adobe Experience Platform permite agendar expirações para conjuntos de dados. Quando um conjunto de dados atinge sua data de expiração, o data lake, o serviço de identidade e o perfil do cliente em tempo real iniciam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos dos três serviços, a expiração será marcada como completa.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho downstream não sejam afetados negativamente.

Este documento aborda como agendar e automatizar as expirações de conjuntos de dados na interface do usuário do Experience Platform.

>[!NOTE]
>
>No momento, a expiração do conjunto de dados não exclui dados do Adobe Experience Platform Edge Network. No entanto, não há possibilidade de os dados permanecerem na Edge Network após o conjunto de dados estar definido para expirar. Isso ocorre porque o contrato de licença de serviço de 15 dias para a expiração do conjunto de dados se sobrepõe ao período de 14 dias em que os dados existem na Edge Network antes de serem descartados.

O Gerenciamento Avançado do Ciclo de Vida dos Dados suporta exclusões de conjuntos de dados por meio do [ponto de extremidade de expiração do conjunto de dados](../api/dataset-expiration.md) e exclusões de ID (dados em nível de linha) usando identidades primárias por meio do [ponto de extremidade da ordem de trabalho](../api/workorder.md). Também é possível gerenciar expirações de conjuntos de dados e [exclusões de registros](./record-delete.md) por meio da interface do usuário do Experience Platform. Consulte a documentação vinculada para obter mais informações.

>[!NOTE]
>
>O ciclo de vida dos dados não oferece suporte à exclusão em lote.

## Programar uma expiração de conjunto de dados {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instruções"
>abstract="<ul><li>Selecione <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=pt-BR">Ciclo de vida dos dados</a> na navegação à esquerda e clique em <b>Criar solicitação</b>.</li><li>Se quiser excluir registros:</li>   <li>Selecione <b>Registro</b>.</li>   <li>Selecione um conjunto de dados específico do qual deseja excluir registros ou escolha a opção para excluí-los de todos os conjuntos de dados.</li>   <li>Forneça a identidade dos consumidores cujos registros devem ser excluídos. Selecionar <b>Adicionar identidade</b> para fornecer as identidades, uma de cada vez ou selecione <b>Escolher arquivos</b> para carregar um arquivo JSON de identidades.</li>   <li>Se necessário, selecione <b>Modelo</b> para exibir o formato esperado do arquivo JSON.</li><li>Consulte a documentação para obter instruções se desejar <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=pt-BR#schedule-dataset-expiration">programar datas de expiração para conjuntos de dados</a>.</li></ul>"

Para criar uma solicitação, selecione **[!UICONTROL Create request]** na página principal do espaço de trabalho.

>[!IMPORTANT]
>
>Os usuários do Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics têm 20 ordens de serviço de expiração do conjunto de dados programadas pendentes. Os usuários do Healthcare Shield e do Privacy and Security Shield têm 50 ordens de trabalho de expiração programadas do conjunto de dados. Isso significa que você pode ter 20 ou 50 conjuntos de dados programados para serem excluídos a qualquer momento.<br>Por exemplo, se você tiver 20 expirações de conjunto de dados agendadas e um conjunto de dados precisar ser excluído amanhã, você não poderá definir mais expirações até que esse conjunto de dados tenha sido excluído.

![O espaço de trabalho [!UICONTROL Data Lifecycle] com [!UICONTROL Create request] realçado.](../images/ui/ttl/create-request-button.png)

O workflow de criação da solicitação é exibido. Na seção [!UICONTROL Requested Action], selecione **[!UICONTROL Delete Dataset]** para atualizar os controles do agendamento de expiração do conjunto de dados.

![O fluxo de trabalho de criação da solicitação com a opção [!UICONTROL Delete dataset] realçada.](../images/ui/ttl/dataset-selected.png)

### Selecionar uma data e um conjunto de dados {#select-date-and-dataset}

Na seção **[!UICONTROL Requested Action]**, selecione uma data em que deseja que o conjunto de dados seja excluído. Você pode inserir a data manualmente (no formato `mm/dd/yyyy`) ou selecionar o ícone de calendário (![Um ícone de calendário.](/help/images/icons/calendar.png)) para selecionar a data em uma caixa de diálogo.

![Uma caixa de diálogo de calendário com uma data de expiração selecionada e realçada para o conjunto de dados.](../images/ui/ttl/select-date.png)

Em seguida, em **[!UICONTROL Dataset Details]**, selecione o ícone do banco de dados (![O ícone do banco de dados.](/help/images/icons/database.png)) para abrir uma caixa de diálogo de seleção de conjunto de dados. Escolha um conjunto de dados na lista ao qual aplicar a expiração e selecione **[!UICONTROL Done]**.

![A caixa de diálogo [!UICONTROL Select dataset] com um conjunto de dados selecionado e [!UICONTROL Done] realçado.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Somente conjuntos de dados pertencentes à sandbox atual são mostrados.

### Enviar a solicitação {#submit-request}

A seção [!UICONTROL Dataset Details] é preenchida para incluir a identidade e o esquema principais para o conjunto de dados selecionado. Em **[!UICONTROL Request settings]**, insira um nome e uma descrição opcional para a solicitação, seguida por **[!UICONTROL Submit]**.

![Uma solicitação de expiração de conjunto de dados concluída com os botões [!UICONTROL Request settings] e [!UICONTROL Submit] realçados.](../images/ui/ttl/submit.png)

Uma caixa de diálogo [!UICONTROL Confirm request] é exibida. Você será solicitado a confirmar o nome do conjunto de dados e a data em que ele será excluído. Selecione **[!UICONTROL Submit]** para continuar.

Depois que a solicitação é enviada, uma ordem de serviço é criada e aparece na guia principal do espaço de trabalho [!UICONTROL Data Lifecycle]. Aqui, você pode monitorar o status da ordem de serviço à medida que ela processa a solicitação.

>[!NOTE]
>
>Consulte a seção de visão geral em [linhas do tempo e transparência](../home.md#dataset-expiration-transparency) para obter detalhes sobre como as expirações do conjunto de dados são processadas depois de executadas.

## Editar ou cancelar a expiração de um conjunto de dados {#edit-or-cancel}

Para editar ou cancelar a expiração de um conjunto de dados, selecione **[!UICONTROL Dataset]** na página principal do espaço de trabalho e selecione a expiração do conjunto de dados na lista.

Na página de detalhes da expiração do conjunto de dados, o painel direito mostra controles para editar ou cancelar a exclusão programada.

## Próximas etapas

Esse documento abordou como agendar expirações de conjunto de dados na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de minimização de dados na interface, consulte a [visão geral sobre a interface do ciclo de vida dos dados](./overview.md).

Para saber como agendar expirações de conjunto de dados usando a API de higiene de dados, consulte o [manual de ponto de extremidade de expiração do conjunto de dados](../api/dataset-expiration.md).
