---
keywords: editar ativação, editar destino, editar destino
title: Editar fluxos de dados de ativação
type: Tutorial
description: Siga as etapas deste artigo para editar um fluxo de dados de ativação existente no Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ca33131c505803b74075f6d8331095b016a301a0
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Editar fluxos de dados de ativação {#edit-activation-flows}

No Adobe Experience Platform, você pode configurar vários componentes de fluxos de dados de ativação existentes para destinos, como:

* [Habilitar ou desabilitar](#enable-disable-dataflows) fluxos de dados de ativação;
* [Adicione mais públicos-alvo e atributos de perfil](#add-audiences) aos fluxos de dados de ativação;
* [Adicionar conjuntos de dados adicionais](#add-datasets) aos fluxos de trabalho de ativação;
* [Editar nomes e descrições](#edit-names-descriptions) para seus fluxos de dados de ativação;

<!-- * [Apply access labels](#apply-access-labels) to exported data; -->

## Procurar fluxos de dados de ativação {#browse-activation-dataflows}

Siga as etapas abaixo para procurar seus fluxos de dados de ativação existentes e identificar aquele que deseja editar.

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecione **[!UICONTROL Procurar]** no cabeçalho superior para exibir seus fluxos de dados de destino existentes.

   ![Procurar destinos](../assets/ui/edit-activation/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../../images/icons/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Selecione o nome do fluxo de dados de destino que deseja editar.

   ![Selecionar destino](../assets/ui/edit-activation/destination-select.png)

4. A página **[!UICONTROL Execuções do fluxo de dados]** para o destino é exibida, mostrando seus controles disponíveis. Dependendo do tipo de destino, é possível executar várias operações de fluxo de dados. Consulte as próximas seções para cada operação de fluxo de dados compatível.

## Habilitar ou desabilitar fluxos de dados de ativação {#enable-disable-dataflows}

Use a opção **[!UICONTROL Habilitado]/[!UICONTROL Desabilitado]** para iniciar ou pausar todas as exportações de dados para o destino.

![Imagem da interface do Experience Platform mostrando a alternância de execução do fluxo de dados Habilitado/Desabilitado.](../assets/ui/edit-activation/enable-toggle.png)

## Adicionar públicos-alvo a um fluxo de dados de ativação {#add-audiences}

Selecione **[!UICONTROL Ativar públicos-alvo]** no painel direito para alterar quais públicos-alvo ou atributos de perfil enviar para o destino. Essa ação leva você ao fluxo de trabalho de ativação, que difere dependendo do tipo de destino.

![imagem da interface do usuário do Experience Platform mostrando a opção de execução do fluxo de dados Ativar públicos-alvo.](../assets/ui/edit-activation/activate-audiences.png)

Para obter mais informações sobre os workflows de ativação para cada tipo de destino, consulte os guias a seguir:

* [Ativar públicos para destinos de streaming](./activate-segment-streaming-destinations.md) (por exemplo, Facebook ou Twitter);
* [Ativar públicos para destinos de exportação de perfil em lote](./activate-batch-profile-destinations.md) (por exemplo, Amazon S3 ou Oracle Eloqua);
* [Ative públicos para destinos de exportação de perfil de streaming](./activate-streaming-profile-destinations.md) (por exemplo, API HTTP ou Amazon Kinesis).

## Adicionar conjuntos de dados a um fluxo de dados de ativação {#add-datasets}

Selecione **[!UICONTROL Exportar conjuntos de dados]** no painel direito para selecionar conjuntos de dados adicionais para exportar para o seu destino. Essa opção direciona você ao [fluxo de trabalho de exportação do conjunto de dados](export-datasets.md).

>[!NOTE]
>
>Esta opção só é visível para [destinos que oferecem suporte à exportação do conjunto de dados](export-datasets.md#supported-destinations).

![Imagem da interface do usuário do Experience Platform mostrando a opção de execução do fluxo de dados Exportar conjuntos de dados.](../assets/ui/edit-activation/export-datasets.png)

<!-- ## Apply access labels {#apply-access-labels}

Select **[!UICONTROL Apply access labels]** to edit the data usage labels for the exported data. See the [data usage labels documentation](../../data-governance/labels/overview.md) to learn more.

![Experience Platform UI image showing the Export datasets dataflow run option.](../assets/ui/edit-activation/apply-access-labels.png) -->

## Editar nomes e descrições do fluxo de dados de ativação {#edit-names-descriptions}

Para editar o nome e a descrição do fluxo de dados de ativação, use os campos **[!UICONTROL Nome do destino]** e **[!UICONTROL Descrição]**.

![Detalhes do destino](../assets/ui/edit-activation/edit-destination-name-description.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você usou com êxito o espaço de trabalho **[!UICONTROL destinos]** para atualizar fluxos de dados de destino existentes.

Para obter mais informações sobre destinos, consulte a [visão geral sobre destinos](../catalog/overview.md).
