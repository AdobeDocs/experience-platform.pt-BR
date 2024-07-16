---
keywords: editar ativação, editar destino, editar destino
title: Editar fluxos de dados de ativação
type: Tutorial
description: Siga as etapas deste artigo para editar um fluxo de dados de ativação existente no Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Editar fluxos de dados de ativação {#edit-activation-flows}

No Adobe Experience Platform, você pode editar vários componentes de fluxos de dados de ativação existentes para destinos, como os públicos-alvo exportados e atributos de perfil, a frequência de exportação, se o fluxo de dados de ativação está ativado ou desativado e muito mais.

## Editar fluxos de dados {#edit-dataflows}

Siga as etapas abaixo para editar os fluxos de dados de ativação existentes:

1. Faça logon na [interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecione **[!UICONTROL Procurar]** no cabeçalho superior para exibir seus fluxos de dados de destino existentes.

   ![Procurar destinos](../assets/ui/edit-activation/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone de filtro](../assets/ui/edit-activation/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os seus destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associados ao destino selecionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Selecione o nome do fluxo de dados de destino que deseja editar.

   ![Selecionar destino](../assets/ui/edit-activation/destination-select.png)

4. A página **[!UICONTROL Execuções do fluxo de dados]** para o destino é exibida, mostrando seus controles disponíveis. Nesse ponto, é possível editar vários componentes do fluxo de dados de destino:

   * Selecione **[!UICONTROL Ativar públicos-alvo]** no painel direito para alterar quais públicos-alvo ou atributos de perfil enviar para o destino. Essa ação leva você ao fluxo de trabalho de ativação, que difere dependendo do tipo de destino. Para obter mais informações, consulte os guias em:
      * [ativação de dados de público-alvo para destinos de transmissão de público-alvo](./activate-segment-streaming-destinations.md) (por exemplo, Facebook ou Twitter);
      * [ativando dados de público-alvo para destinos baseados em perfil em lote](./activate-batch-profile-destinations.md) (por exemplo, Amazon S3 ou Oracle Eloqua);
      * [ativando dados de público-alvo para destinos baseados em perfil de streaming](./activate-streaming-profile-destinations.md) (por exemplo, API HTTP ou Amazon Kinesis).

   * Além disso, você pode editar o nome e a descrição do fluxo de dados de destino.
   * Você pode usar a opção **[!UICONTROL Habilitado]/[!UICONTROL Desabilitado]** para iniciar e pausar todas as exportações de dados para o destino.

   ![Detalhes do destino](../assets/ui/edit-activation/destination-details.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você usou com êxito o espaço de trabalho **[!UICONTROL destinos]** para atualizar fluxos de dados de destino existentes.

Para obter mais informações sobre destinos, consulte a [visão geral sobre destinos](../catalog/overview.md).
