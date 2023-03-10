---
title: Gerenciar expirações do conjunto de dados
description: Saiba como programar a expiração de um conjunto de dados na interface do usuário do Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Gerenciar expirações do conjunto de dados {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Descrição"
>abstract=""

>[!IMPORTANT]
>
>Atualmente, os recursos de higiene de dados na Adobe Experience Platform estão disponíveis apenas para organizações que compraram **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**.

A variável [[!UICONTROL Higiene de dados] espaço de trabalho](./overview.md) na interface do Adobe Experience Platform, permite agendar expirações para conjuntos de dados. Quando um conjunto de dados atinge sua data de expiração, o data lake, o serviço de identidade e o perfil do cliente em tempo real iniciam processos separados para remover o conteúdo do conjunto de dados de seus respectivos serviços. Depois que os dados forem excluídos dos três serviços, a expiração será marcada como completa.

>[!WARNING]
>
>Se um conjunto de dados estiver definido para expirar, você deverá alterar manualmente todos os fluxos de dados que possam estar assimilando dados nesse conjunto de dados para que seus fluxos de trabalho downstream não sejam afetados negativamente.

Este documento aborda como agendar e gerenciar expirações de conjunto de dados na interface do usuário da plataforma.

## Programar uma expiração do conjunto de dados {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instruções"
>abstract=""

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
>
>Somente conjuntos de dados pertencentes à sandbox atual são mostrados.

### Enviar a solicitação

A variável [!UICONTROL Detalhes do conjunto de dados] A seção é preenchida para incluir a identidade e o esquema principais para o conjunto de dados selecionado. Em **[!UICONTROL Configurações de solicitação]**, insira um nome e uma descrição opcional para a solicitação, seguida por **[!UICONTROL Enviar]**.

![Imagem mostrando o [!UICONTROL Enviar] botão sendo selecionado](../images/ui/ttl/submit.png)

Você será solicitado a confirmar a data em que o conjunto de dados será excluído. Selecionar **[!UICONTROL Enviar]** para continuar.

Depois que a solicitação é enviada, uma ordem de serviço é criada e é exibida na guia principal do [!UICONTROL Higiene de dados] espaço de trabalho. Aqui, você pode monitorar o status da ordem de serviço à medida que ela processa a solicitação.

>[!NOTE]
>
>Consulte a seção de visão geral em [linhas do tempo e transparência](../home.md#dataset-expiration-transparency) para obter detalhes sobre como as expirações do conjunto de dados são processadas depois de executadas.

## Editar ou cancelar a expiração de um conjunto de dados

Para editar ou cancelar a expiração de um conjunto de dados, selecione **[!UICONTROL Conjunto de dados]** na página principal do espaço de trabalho e selecione na lista a expiração do conjunto de dados.

Na página de detalhes da expiração do conjunto de dados, o painel direito mostra controles para editar ou cancelar a exclusão programada.

## Próximas etapas

Esse documento abordou como programar as expirações do conjunto de dados na interface do usuário do Experience Platform. Para obter informações sobre como executar outras tarefas de higiene de dados na interface do usuário, consulte [visão geral da interface da higiene de dados](./overview.md).

Para saber como agendar expirações de conjunto de dados usando a API de higiene de dados, consulte o [guia de ponto de extremidade de expiração do conjunto de dados](../api/dataset-expiration.md).
