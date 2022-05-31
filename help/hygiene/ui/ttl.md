---
title: Gerenciar TTLs do conjunto de dados
description: Saiba como agendar um TTL (time to live) para um conjunto de dados na interface do usuário do Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Gerenciar TTLs do conjunto de dados

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Adobe Shield for Healthcare.

O [[!UICONTROL Higiene de dados] espaço de trabalho](./overview.md) na interface do usuário do Adobe Experience Platform permite agendar um TTL (time to live) para um conjunto de dados.

Este documento aborda como agendar e gerenciar TTLs de conjuntos de dados na interface do usuário da plataforma.

## Agendar um TTL

Para criar uma nova solicitação, selecione **[!UICONTROL Criar solicitação]** na página principal do espaço de trabalho.

![Imagem que mostra o [!UICONTROL Criar solicitação] botão sendo selecionado](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### Selecionar uma data e um conjunto de dados

A caixa de diálogo de criação da solicitação é exibida. Em **[!UICONTROL Ação]** selecione uma data em que deseja que o conjunto de dados seja excluído. É possível inserir a data manualmente (no formato `mm/dd/yyyy`) ou selecione o ícone de calendário (![Imagem do ícone do calendário](../images/ui/ttl/calendar-icon.png)) para selecionar a data de uma caixa de diálogo.

![Imagem que mostra uma data de expiração sendo definida para o TTL](../images/ui/ttl/select-date.png)

Em seguida, em **[!UICONTROL Detalhes do conjunto de dados]**, selecione o ícone do banco de dados (![Imagem do ícone do banco de dados](../images/ui/ttl/database-icon.png)) para abrir uma caixa de diálogo de seleção de conjunto de dados. Escolha um conjunto de dados na lista para aplicar o TTL, em seguida, selecione **[!UICONTROL Concluído]**.

![Imagem que mostra um conjunto de dados sendo selecionado](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Somente os conjuntos de dados pertencentes à sandbox atual são mostrados.

### Enviar a solicitação

Depois de selecionar um conjunto de dados e uma data TTL, selecione **[!UICONTROL Enviar]**.

![Imagem que mostra o [!UICONTROL Enviar] botão sendo selecionado](../images/ui/ttl/submit.png)

Você receberá uma solicitação para confirmar a data em que o conjunto de dados será excluído. Selecionar **[!UICONTROL Enviar]** para continuar.

Depois que a solicitação é enviada, uma ordem de serviço é criada e aparece na guia principal do [!UICONTROL Higiene de dados] espaço de trabalho. A partir daqui, você pode monitorar o status da ordem de serviço enquanto ela processa a solicitação.

## Editar ou cancelar um TTL

Para editar ou cancelar um TTL, selecione **[!UICONTROL Conjunto de dados]** na página principal do espaço de trabalho e selecione o TTL na lista.

Na página de detalhes do TTL, o painel direito mostra controles para editar ou cancelar a exclusão agendada.

## Próximas etapas

Este documento cobriu como agendar TTLs de conjuntos de dados na interface do usuário do Experience Platform. Para saber como agendar TTLs de conjuntos de dados usando a API de Higiene de dados, consulte o [guia do endpoint TTL do conjunto de dados](../api/ttl.md).
