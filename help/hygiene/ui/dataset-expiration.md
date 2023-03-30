---
title: Gerenciar expirações do conjunto de dados
description: Saiba como agendar uma expiração de conjunto de dados na interface do usuário do Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Gerenciar expirações do conjunto de dados {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Excluir registros e conjuntos de dados de clientes indesejados ou expirados"
>abstract="<h2>Descrição</h2><p>Para gerenciar o ciclo de vida dos dados do Experience Platform não relacionados à conformidade normativa, você pode excluir registros do consumidor e programar datas de expiração para os conjuntos de dados. Para criar ou gerenciar solicitações do titular dos dados, consulte o bloco de casos de uso &quot;Respeitar solicitações de privacidade do titular dos dados&quot;.</p>"

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram **Blindagem do Adobe Healthcare** ou **Privacidade e proteção de segurança do Adobe**. Esses recursos devem ser lançados de forma geral em breve. Para obter mais informações sobre a disponibilidade futura, entre em contato com o representante de serviço da Adobe. Você pode, no entanto, imediatamente [exclua conjuntos de dados por meio da [!UICONTROL Conjuntos de dados] interface](../../catalog/datasets/user-guide.md#delete).

O [[!UICONTROL Higiene de dados] espaço de trabalho](./overview.md) na interface do usuário do Adobe Experience Platform permite agendar expirações para conjuntos de dados. Quando um conjunto de dados atinge sua data de expiração, o lago de dados, o Serviço de identidade e o Perfil do cliente em tempo real começam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos de todos os três serviços, a expiração será marcada como concluída.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho de downstream não sejam afetados negativamente.

Este documento aborda como agendar e gerenciar as expirações do conjunto de dados na interface do usuário da plataforma.

## Programar uma expiração de conjunto de dados {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instruções"
>abstract="<ul><li>Selecionar <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">Higiene de dados</a> na navegação à esquerda, selecione <b>Criar solicitação</b>.</li><li>Se quiser excluir registros:</li>   <li>Selecionar <b>Registro</b>.</li>   <li>Selecione um conjunto de dados específico do qual deseja excluir registros ou escolha a opção para excluí-los de todos os conjuntos de dados.</li>   <li>Indicar a identidade dos consumidores cujos registros devem ser suprimidos. Selecionar <b>Adicionar identidade</b> para fornecer as identidades, uma de cada vez ou selecione <b>Escolher arquivos</b> para carregar um arquivo JSON de identidades.</li>   <li>Se necessário, selecione <b>Modelo</b> para exibir o formato esperado do arquivo JSON.</li><li>Consulte a documentação para obter instruções se desejar <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">datas de expiração do agendamento para conjuntos de dados</a>.</li></ul>"

Para criar uma nova solicitação, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![Imagem que mostra o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/ttl/create-request-button.png)

A caixa de diálogo de criação da solicitação é exibida. Em **[!UICONTROL Ação solicitada]** seção , selecione **[!UICONTROL Excluir conjunto de dados]** para atualizar os controles disponíveis para o agendamento de expiração do conjunto de dados.

![Imagem que mostra o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/ttl/dataset-selected.png)

### Selecionar uma data e um conjunto de dados

A caixa de diálogo de criação da solicitação é exibida. Em **[!UICONTROL Ação solicitada]** selecione uma data em que deseja que o conjunto de dados seja excluído. É possível inserir a data manualmente (no formato `mm/dd/yyyy`) ou selecione o ícone de calendário (![Imagem do ícone do calendário](../images/ui/ttl/calendar-icon.png)) para selecionar a data de uma caixa de diálogo.

![Imagem que mostra uma data de expiração sendo definida para o conjunto de dados](../images/ui/ttl/select-date.png)

Em seguida, em **[!UICONTROL Detalhes do conjunto de dados]**, selecione o ícone do banco de dados (![Imagem do ícone do banco de dados](../images/ui/ttl/database-icon.png)) para abrir uma caixa de diálogo de seleção de conjunto de dados. Escolha um conjunto de dados na lista ao qual aplicar a expiração e selecione **[!UICONTROL Concluído]**.

![Imagem que mostra um conjunto de dados sendo selecionado](../images/ui/ttl/select-dataset.png)

>[!NOTE]
Somente os conjuntos de dados pertencentes à sandbox atual são mostrados.

### Enviar a solicitação

O [!UICONTROL Detalhes do conjunto de dados] é preenchida para incluir a identidade e o esquema primários do conjunto de dados selecionado. Em **[!UICONTROL Configurações da solicitação]**, insira um nome e uma descrição opcional para a solicitação, seguido de **[!UICONTROL Enviar]**.

![Imagem que mostra o [!UICONTROL Enviar] botão sendo selecionado](../images/ui/ttl/submit.png)

Você receberá uma solicitação para confirmar a data em que o conjunto de dados será excluído. Selecionar **[!UICONTROL Enviar]** para continuar.

Depois que a solicitação é enviada, uma ordem de serviço é criada e aparece na guia principal do [!UICONTROL Higiene de dados] espaço de trabalho. A partir daqui, você pode monitorar o status da ordem de serviço enquanto ela processa a solicitação.

>[!NOTE]
Consulte a seção de visão geral em [prazos e transparência](../home.md#dataset-expiration-transparency) para obter detalhes sobre como as expirações do conjunto de dados são processadas depois de executadas.

## Editar ou cancelar uma expiração de conjunto de dados

Para editar ou cancelar uma expiração de conjunto de dados, selecione **[!UICONTROL Conjunto de dados]** na página principal do espaço de trabalho e selecione a expiração do conjunto de dados na lista.

Na página de detalhes da expiração do conjunto de dados, o painel direito mostra controles para editar ou cancelar a exclusão agendada.

## Próximas etapas

Este documento cobriu como agendar as expirações do conjunto de dados na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de higiene de dados na interface do usuário, consulte [visão geral da interface do usuário da higiene de dados](./overview.md).

Para saber como agendar as expirações do conjunto de dados usando a API da Higiene de dados, consulte o [guia do endpoint de expiração de conjunto de dados](../api/dataset-expiration.md).
