---
title: Gerenciar expirações do conjunto de dados
description: Saiba como programar a expiração de um conjunto de dados na interface do usuário do Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 22%

---

# Gerenciar expirações do conjunto de dados {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Excluir registros e conjuntos de dados de clientes indesejados ou expirados"
>abstract="<h2>Descrição</h2><p>Para gerenciar o ciclo de vida dos dados da Experience Platform não relacionados à conformidade regulatória, você pode excluir registros do consumidor e programar datas de expiração para os conjuntos de dados. Para criar ou gerenciar solicitações do titular dos dados, consulte o bloco de casos de uso &quot;Respeitar solicitações de privacidade do titular dos dados&quot;.</p>"

>[!IMPORTANT]
>
>Atualmente, os recursos de higiene de dados na Adobe Experience Platform estão disponíveis apenas para organizações que compraram **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**. Esses recursos devem ser lançados em breve. Para obter mais informações sobre a disponibilidade futura, fale com o representante de serviços da Adobe. No entanto, você pode imediatamente [excluir conjuntos de dados por meio da [!UICONTROL Conjuntos de dados] IU](../../catalog/datasets/user-guide.md#delete).

A variável [[!UICONTROL Higiene de dados] espaço de trabalho](./overview.md) na interface do Adobe Experience Platform, permite agendar expirações para conjuntos de dados. Quando um conjunto de dados atinge sua data de expiração, o data lake, o serviço de identidade e o perfil do cliente em tempo real iniciam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos dos três serviços, a expiração será marcada como completa.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho downstream não sejam afetados negativamente.

Este documento aborda como agendar e gerenciar expirações de conjunto de dados na interface do usuário da plataforma.

## Programar uma expiração do conjunto de dados {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instruções"
>abstract="<ul><li>Selecione <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=pt-BR">Higiene de dados</a> na navegação à esquerda, e depois <b>Criar solicitação</b>.</li><li>Se quiser excluir registros:</li>   <li>Selecione <b>Registro</b>.</li>   <li>Selecione um conjunto de dados específico do qual deseja excluir registros ou escolha a opção para excluí-los de todos os conjuntos de dados.</li>   <li>Forneça a identidade dos consumidores cujos registros devem ser excluídos. Selecionar <b>Adicionar identidade</b> para fornecer as identidades, uma de cada vez ou selecione <b>Escolher arquivos</b> para carregar um arquivo JSON de identidades.</li>   <li>Se necessário, selecione <b>Modelo</b> para exibir o formato esperado do arquivo JSON.</li><li>Consulte a documentação para obter instruções se desejar <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">programar datas de expiração para conjuntos de dados</a>.</li></ul>"

Para criar uma nova solicitação, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![Imagem mostrando o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/ttl/create-request-button.png)

A caixa de diálogo de criação de solicitação é exibida. No **[!UICONTROL Ação solicitada]** , selecione **[!UICONTROL Excluir conjunto de dados]** para atualizar os controles disponíveis para o agendamento da expiração do conjunto de dados.

![Imagem mostrando o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/ttl/dataset-selected.png)

### Selecionar uma data e um conjunto de dados

A caixa de diálogo de criação de solicitação é exibida. No **[!UICONTROL Ação solicitada]** selecione uma data em que deseja que o conjunto de dados seja excluído. É possível inserir a data manualmente (no formato `mm/dd/yyyy`) ou selecione o ícone de calendário (![Imagem do ícone do calendário](../images/ui/ttl/calendar-icon.png)) para selecionar a data em uma caixa de diálogo.

![Imagem mostrando uma data de expiração sendo definida para o conjunto de dados](../images/ui/ttl/select-date.png)

Em seguida, em **[!UICONTROL Detalhes do conjunto de dados]**, selecione o ícone do banco de dados (![Imagem do ícone do banco de dados](../images/ui/ttl/database-icon.png)) para abrir uma caixa de diálogo de seleção de conjunto de dados. Escolha um conjunto de dados na lista ao qual aplicar a expiração e selecione **[!UICONTROL Concluído]**.

![Imagem mostrando um conjunto de dados que está sendo selecionado](../images/ui/ttl/select-dataset.png)

>[!NOTE]
Somente conjuntos de dados pertencentes à sandbox atual são mostrados.

### Enviar a solicitação

A variável [!UICONTROL Detalhes do conjunto de dados] A seção é preenchida para incluir a identidade e o esquema principais para o conjunto de dados selecionado. Em **[!UICONTROL Configurações de solicitação]**, insira um nome e uma descrição opcional para a solicitação, seguida por **[!UICONTROL Enviar]**.

![Imagem mostrando o [!UICONTROL Enviar] botão sendo selecionado](../images/ui/ttl/submit.png)

Você será solicitado a confirmar a data em que o conjunto de dados será excluído. Selecionar **[!UICONTROL Enviar]** para continuar.

Depois que a solicitação é enviada, uma ordem de serviço é criada e é exibida na guia principal do [!UICONTROL Higiene de dados] espaço de trabalho. Aqui, você pode monitorar o status da ordem de serviço à medida que ela processa a solicitação.

>[!NOTE]
Consulte a seção de visão geral em [linhas do tempo e transparência](../home.md#dataset-expiration-transparency) para obter detalhes sobre como as expirações do conjunto de dados são processadas depois de executadas.

## Editar ou cancelar a expiração de um conjunto de dados

Para editar ou cancelar a expiração de um conjunto de dados, selecione **[!UICONTROL Conjunto de dados]** na página principal do espaço de trabalho e selecione na lista a expiração do conjunto de dados.

Na página de detalhes da expiração do conjunto de dados, o painel direito mostra controles para editar ou cancelar a exclusão programada.

## Próximas etapas

Esse documento abordou como programar as expirações do conjunto de dados na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de higiene de dados na interface do usuário, consulte [visão geral da interface da higiene de dados](./overview.md).

Para saber como agendar expirações de conjunto de dados usando a API de higiene de dados, consulte o [guia de ponto de extremidade de expiração do conjunto de dados](../api/dataset-expiration.md).
