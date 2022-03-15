---
keywords: destinos, destino, página de detalhes de destinos, página de detalhes de destinos
title: Exibir detalhes do destino
description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino. Os detalhes do destino incluem o nome do destino, a ID, os segmentos mapeados para o destino e os controles para editar a ativação e ativar e desativar o fluxo de dados. '
seo-description: The details page for an individual destination provides an overview of the destination details. Destination details include the destination name, ID, segments mapped to the destination, and controls to edit the activation and to enable and disable the data flow.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a129085f034665a6398bbf0ccfe2f1dc8acbdd8a
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---

# Exibir detalhes do destino

## Visão geral {#overview}

Na interface do usuário do Adobe Experience Platform, é possível visualizar e monitorar os atributos e atividades dos destinos. Esses detalhes incluem o nome e a ID do destino, controles para ativar ou desativar os destinos e muito mais. Os detalhes também incluem métricas para registros de perfil ativados, identidades ativadas, falhas e excluídas, e um histórico de execuções de fluxo de dados.

>[!NOTE]
>
>A página de detalhes de destinos faz parte do [!UICONTROL Destinos] na área de trabalho do [!DNL Platform] [!DNL UI]. Consulte a [[!UICONTROL Destinos] visão geral do espaço de trabalho](./destinations-workspace.md) para obter mais informações.

## Exibir detalhes do destino {#view-details}

Siga as etapas abaixo para visualizar mais detalhes sobre um destino existente.

1. Faça logon no [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecionar **[!UICONTROL Procurar]** no cabeçalho superior para exibir os destinos existentes.

   ![Procurar destinos](../assets/ui/details-page/browse-destinations.png)

1. Selecione o ícone de filtro ![Ícone Filtro](../assets/ui/details-page/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

   ![Filtrar destinos](../assets/ui/details-page/filter-destinations.png)

1. Selecione o nome do destino que deseja visualizar.

   ![Selecionar destino](../assets/ui/details-page/destination-select.png)

1. A página de detalhes do destino é exibida, mostrando os controles disponíveis.

   ![Detalhes do destino](../assets/ui/details-page/destination-details.png)

## Painel direito {#right-rail}

O painel direito exibe as informações básicas sobre o destino selecionado.

![trilho direito](../assets/ui/details-page/right-sidebar.png)

O quadro seguinte cobre os controlos e os pormenores fornecidos pelo painel direito:

| Item do painel direito | Descrição |
| --- | --- |
| [!UICONTROL Ativar segmentos] | Selecione esse controle para editar quais segmentos são mapeados para o destino, atualizar programações de exportação ou adicionar e remover atributos e identidades mapeadas. Veja os guias em [como ativar dados do público-alvo para segmentar destinos de transmissão](./activate-segment-streaming-destinations.md), [ativação de dados de público-alvo para destinos com base em perfil em lote](./activate-batch-profile-destinations.md)e [ativação de dados de público-alvo para streaming de destinos com base em perfil](./activate-streaming-profile-destinations.md) para obter mais informações. |
| [!UICONTROL Excluir] | Permite excluir esse fluxo de dados e desmapeia os segmentos que foram ativados anteriormente, caso existam. |
| [!UICONTROL Nome do destino] | Este campo pode ser editado para atualizar o nome do destino. |
| [!UICONTROL Descrição] | Este campo pode ser editado para atualizar ou adicionar uma descrição opcional ao destino. |
| [!UICONTROL Destino] | Representa a plataforma de destino para a qual os públicos-alvo são enviados. Consulte a [catálogo de destinos](../catalog/overview.md) para obter mais informações. |
| [!UICONTROL Status] | Indica se o destino está ativado ou desativado. |
| [!UICONTROL Ações de marketing] | Indica as ações de marketing (casos de uso) que se aplicam a esse destino para fins de governança de dados. |
| [!UICONTROL Categoria] | Indica o tipo de destino. Consulte a [catálogo de destinos](../catalog/overview.md) para obter mais informações. |
| [!UICONTROL Tipo de conexão] | Indica o formulário pelo qual seus públicos-alvo estão sendo enviados para o destino. Os valores possíveis incluem [!UICONTROL Cookie] e [!UICONTROL Baseado em perfil]. |
| [!UICONTROL Frequência] | Indica a frequência com que os públicos-alvo são enviados para o destino. Os valores possíveis incluem [!UICONTROL Streaming] e [!UICONTROL Em lote]. |
| [!UICONTROL Identidade] | Representa o namespace de identidade aceito pelo destino, como `GAID`, `IDFA`ou `email`. Para obter mais informações sobre namespaces de identidade aceitos, consulte o [visão geral do namespace de identidade](../../identity-service/namespaces.md). |
| [!UICONTROL Criado por] | Indica o usuário que criou esse destino. |
| [!UICONTROL Criado] | Indica a data e hora UTC em que esse destino foi criado. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Ativado]/[!UICONTROL Desabilitado] alternar {#enabled-disabled-toggle}

Você pode usar o **[!UICONTROL Ativado]/[!UICONTROL Desabilitado]** para iniciar e pausar todas as exportações de dados para o destino.

![Ativar ou desativar a alternância de fluxo de dados](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Execuções do fluxo de dados] {#dataflow-runs}

O [!UICONTROL Execuções do fluxo de dados] A guia fornece dados de métrica em suas execuções de fluxo de dados para destinos de lote e fluxo. Consulte [Monitorar fluxos de dados](monitor-dataflows.md) para obter detalhes e definições de métricas.

>[!NOTE]
>
>A funcionalidade de monitoramento de destinos é atualmente compatível com todos os destinos no Experience Platform *Except* o [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Hubs de Eventos do Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [API HTTP](/help/destinations/catalog/streaming/http-destination.md), [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)e [Personalização personalizada](/help/destinations/catalog/personalization/custom-personalization.md) destinos.

![Exibição de execuções do fluxo de dados](../assets/ui/details-page/dataflow-runs.png)

## [!UICONTROL Dados de ativação] {#activation-data}

O [!UICONTROL Dados de ativação] exibe uma lista de segmentos que foram mapeados para o destino, incluindo a data de início e a data de término (se aplicável) e outras informações relevantes para a exportação de dados, como tipo de exportação, programação e frequência. Para exibir os detalhes sobre um segmento específico, selecione o nome na lista.

>[!TIP]
>
>Para exibir e editar detalhes sobre os atributos e identidades mapeados para um destino, selecione **[!UICONTROL Ativar segmentos]** no [trilho direito](#right-rail).

![Destino em lote da exibição de dados de ativação](../assets/ui/details-page/activation-data-batch.png)

![Destino de transmissão da exibição de dados de ativação](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Para obter detalhes sobre como explorar a página de detalhes de um segmento, consulte o [Visão geral da interface do usuário de segmentação](../../segmentation/ui/overview.md#segment-details).
