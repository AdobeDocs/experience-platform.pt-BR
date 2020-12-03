---
keywords: destinations;destination;destinations detail page;destinations details page
title: Página Detalhes de Destinos
seo-title: Página Detalhes de Destinos
description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. '
seo-description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. '
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---


# Página de detalhes do destino

Na interface do usuário do Adobe Experience Platform, você pode visualização e monitorar os atributos e atividades de seus destinos. Esses detalhes incluem o nome e a ID do destino, controles para ativar ou desativar os destinos e muito mais. Detalhes para destinos em lote também incluem métricas para registros de perfis ativados e histórico de execuções de fluxo de dados.

>[!NOTE]
>
>A página de detalhes de destinos faz parte da área de trabalho [!UICONTROL Destinos] na interface do usuário da plataforma. Consulte a visão geral [[!UICONTROL da área de trabalho] Destinos](./destinations-workspace.md) para obter mais informações.

Na área de trabalho **[!UICONTROL Destinos]** na interface do usuário da plataforma, navegue até a guia **[!UICONTROL Procurar]** e selecione o nome de um destino que deseja visualização.

![](../assets/ui/details-page/select-destination.png)

A página de detalhes do destino é exibida, mostrando seus controles disponíveis. Se você estiver visualizando os detalhes de um destino em lote, um painel de monitoramento também será exibido.

![](../assets/ui/details-page/details.png)

## Trilho direito

O painel direito exibe as informações básicas sobre o destino.

![](../assets/ui/details-page/right-rail.png)

O quadro seguinte cobre os controlos e os pormenores fornecidos pelo painel direito:

| Item do painel direito | Descrição |
| --- | --- |
| [!UICONTROL Ativar] | Selecione esse controle para editar quais segmentos são mapeados para o destino. Consulte o guia sobre como [ativar segmentos em um destino](./activate-destinations.md) para obter mais informações. |
| [!UICONTROL Nome do destino] | Este campo pode ser editado para atualizar o nome do destino. |
| [!UICONTROL Descrição] | Esse campo pode ser editado para atualizar ou adicionar uma descrição opcional ao destino. |
| [!UICONTROL Destino] | Representa a plataforma de destino para a qual o audiência é enviado. Consulte o catálogo [de](../catalog/overview.md) destinos para obter mais informações. |
| [!UICONTROL Status] | Indica se o destino está ativado ou desativado. |
| [!UICONTROL Ações de marketing] | Indica as ações de marketing (casos de uso) que se aplicam a esse destino para fins de gerenciamento de dados. |
| [!UICONTROL Categoria] | Indica o tipo de destino. Consulte o catálogo [de](../catalog/overview.md) destinos para obter mais informações. |
| [!UICONTROL Tipo de conexão] | Indica o formulário pelo qual suas audiências estão sendo enviadas para o destino. Os valores possíveis incluem &quot;[!UICONTROL Cookie]&quot; e &quot;baseado[!UICONTROL em]Perfis&quot;. |
| [!UICONTROL Frequência] | Indica com que frequência as audiências são enviadas para o destino. Os valores possíveis incluem &quot;[!UICONTROL Streaming]&quot; e &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identidade] | Representa a namespace de identidade aceita pelo destino, como `GAID`, `IDFA`ou `email`. Para obter mais informações sobre namespaces de identidade aceitas, consulte a visão geral [da namespace de](../../identity-service/namespaces.md)identidade. |
| [!UICONTROL Criado por] | Indica o usuário que criou este destino. |
| [!UICONTROL Criado] | Indica a data e hora UTC em que esse destino foi criado. |

## [!UICONTROL Alternância ativada]/[!UICONTROL desativada]

Você pode usar a opção **[!UICONTROL Ativado]/[!UICONTROL Desativado]** para alternar para o start e pausar todas as exportações de dados para o destino.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Execuções do Dataflow]

A guia [!UICONTROL Dataflow executa] fornece dados de métricas em suas execuções de fluxo de dados para destinos em lote. Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para registros de perfis:

* **[!UICONTROL Registros de perfil ativados]**: A contagem total de registros de perfis criados ou atualizados para ativação.
* **[!UICONTROL Registros de perfil ignorados]**:  A contagem total de registros de perfis ignorados para ativação com base em saídas de perfis ou atributos ausentes.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>As execuções de fluxo de dados são geradas com base na frequência de programação do fluxo de dados de destino. Uma execução de fluxo de dados separada é realizada para cada política de mesclagem aplicada a um segmento.

Para visualização dos detalhes de uma execução específica do fluxo de dados, selecione o tempo de start da execução na lista. A página de detalhes de uma execução de fluxo de dados contém informações adicionais, como o tamanho dos dados processados e uma lista de erros que ocorreram com detalhes do diagnóstico de erros.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Segmentos]

A guia [!UICONTROL Segmentos] exibe uma lista de segmentos que foram mapeados para o destino, incluindo a data e a data de start (se aplicável). Para visualização dos detalhes sobre um segmento específico, selecione seu nome na lista.

![](../assets/ui/details-page/segments.png)

>[!NOTE]
>
>Para obter detalhes sobre como explorar a página de detalhes de um segmento, consulte a visão geral [da interface do usuário de](../../segmentation/ui/overview.md#segment-details)segmentação.

## Próximas etapas

Este documento cobriu os recursos da página de detalhes de destino. Para obter mais informações sobre como gerenciar destinos na interface do usuário, consulte a visão geral da área de trabalho [[!UICONTROL Destinos]](./destinations-workspace.md).