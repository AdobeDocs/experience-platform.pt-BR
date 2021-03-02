---
keywords: destinos, destino, página de detalhes de destinos, página de detalhes de destinos
title: Exibir detalhes do destino
description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como o nome do destino, a ID, os segmentos mapeados para o destino e os controles para editar a ativação e ativar e desativar o fluxo de dados. '
seo-description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como o nome do destino, a ID, os segmentos mapeados para o destino e os controles para editar a ativação e ativar e desativar o fluxo de dados. '
translation-type: tm+mt
source-git-commit: 9305936ca1e73821b2fe948ff1a17a7168840cba
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---


# Exibir detalhes do destino

Na interface do usuário da Adobe Experience Platform, é possível visualizar e monitorar os atributos e atividades dos destinos. Esses detalhes incluem o nome e a ID do destino, controles para ativar ou desativar os destinos e muito mais. Os detalhes para destinos em lote também incluem métricas para registros de perfil ativados e um histórico de execuções de fluxo de dados.

>[!NOTE]
>
>A página de detalhes de destinos faz parte do espaço de trabalho [!UICONTROL Destinos] na interface do usuário da plataforma. Consulte a [[!UICONTROL Destinos] visão geral do espaço de trabalho](./destinations-workspace.md) para obter mais informações.

Na área de trabalho **[!UICONTROL Destinations]** na interface do usuário da plataforma, navegue até a guia **[!UICONTROL Browse]** e selecione o nome de um destino que deseja visualizar.

![](../assets/ui/details-page/select-destination.png)

A página de detalhes do destino é exibida, mostrando os controles disponíveis. Se você estiver visualizando os detalhes de um destino de lote, um painel de monitoramento também será exibido.

![](../assets/ui/details-page/details.png)

Além disso, na guia Procurar, é possível optar por excluir o fluxo de dados selecionado selecionando o ícone ![lixeira](../assets/ui/details-page/trash-icon.png). Quaisquer segmentos ativados para destinos serão desmapeados antes que o fluxo de dados seja excluído.

![](../assets/ui/details-page/delete-flow.png)

## Painel direito

O painel direito exibe as informações básicas sobre o destino.

![](../assets/ui/details-page/right-rail.png)

O quadro seguinte cobre os controlos e os pormenores fornecidos pelo painel direito:

| Item do painel direito | Descrição |
| --- | --- |
| [!UICONTROL Ativar] | Selecione esse controle para editar quais segmentos são mapeados para o destino. Consulte o guia em [ativar segmentos em um destino](./activate-destinations.md) para obter mais informações. |
| [!UICONTROL Excluir] | Permite excluir esse fluxo de dados e desmapear os segmentos que foram ativados anteriormente, caso existam. |
| [!UICONTROL Nome do destino] | Este campo pode ser editado para atualizar o nome do destino. |
| [!UICONTROL Descrição] | Este campo pode ser editado para atualizar ou adicionar uma descrição opcional ao destino. |
| [!UICONTROL Destino] | Representa a plataforma de destino para a qual os públicos-alvo são enviados. Consulte o [catálogo de destinos](../catalog/overview.md) para obter mais informações. |
| [!UICONTROL Status] | Indica se o destino está ativado ou desativado. |
| [!UICONTROL Ações de marketing] | Indica as ações de marketing (casos de uso) que se aplicam a esse destino para fins de governança de dados. |
| [!UICONTROL Categoria] | Indica o tipo de destino. Consulte o [catálogo de destinos](../catalog/overview.md) para obter mais informações. |
| [!UICONTROL Tipo de conexão] | Indica o formulário pelo qual seus públicos-alvo estão sendo enviados para o destino. Os valores possíveis incluem &quot;[!UICONTROL Cookie]&quot; e &quot;[!UICONTROL Baseado em perfil]&quot;. |
| [!UICONTROL Frequência] | Indica a frequência com que os públicos-alvo são enviados para o destino. Os valores possíveis incluem &quot;[!UICONTROL Streaming]&quot; e &quot;[!UICONTROL Batch]&quot;. |
| [!UICONTROL Identidade] | Representa o namespace de identidade aceito pelo destino, como `GAID`, `IDFA` ou `email`. Para obter mais informações sobre namespaces de identidade aceitos, consulte a [visão geral do namespace de identidade](../../identity-service/namespaces.md). |
| [!UICONTROL Criado por] | Indica o usuário que criou esse destino. |
| [!UICONTROL Criado] | Indica a data e hora UTC em que esse destino foi criado. |

## [!UICONTROL Ativar]/ Desativar alternância

Você pode usar a opção **[!UICONTROL Enabled]/[!UICONTROL Disabled]** para iniciar e pausar todas as exportações de dados para o destino.

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Execuções do fluxo de dados]

A guia [!UICONTROL Dataflow executa] fornece dados de métrica em suas execuções de fluxo de dados para destinos em lote. Uma lista de execuções individuais e suas métricas específicas é exibida, juntamente com os seguintes totais para registros de perfil:

* **[!UICONTROL Registros de perfil ativados]**: A contagem total de registros de perfil que foram criados ou atualizados para ativação.
* **[!UICONTROL Registros de perfil ignorados]**: A contagem total de registros de perfil que são ignorados para ativação com base em saídas de perfil ou atributos ausentes.

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>As execuções de fluxo de dados são geradas com base na frequência de agendamento do fluxo de dados de destino. Uma execução de fluxo de dados separada é feita para cada política de mesclagem aplicada a um segmento.

Para exibir os detalhes de uma execução específica do fluxo de dados, selecione a hora de início da execução na lista. A página de detalhes de uma execução do fluxo de dados contém informações adicionais, como o tamanho dos dados processados e uma lista de erros que ocorreram com detalhes para o diagnóstico de erros.

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Dados de ativação] {#activation-data}

A guia [!UICONTROL Ativation data] exibe uma lista de segmentos que foram mapeados para o destino, incluindo sua data inicial e data final (se aplicável). Para exibir os detalhes sobre um segmento específico, selecione o nome na lista.

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Para obter detalhes sobre como explorar a página de detalhes de um segmento, consulte a [Visão geral da interface do usuário de segmentação](../../segmentation/ui/overview.md#segment-details).

## Próximas etapas

Este documento cobriu os recursos da página de detalhes do destino. Para obter mais informações sobre como gerenciar destinos na interface do usuário, consulte a visão geral no espaço de trabalho [[!UICONTROL Destinos]](./destinations-workspace.md).