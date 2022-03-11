---
keywords: editar ativação, editar destino, editar destino
title: Editar fluxos de dados de ativação
type: Tutorial
seo-title: Edit activation dataflows
description: Siga as etapas neste artigo para editar um fluxo de dados de ativação existente no Adobe Experience Platform.
seo-description: Follow the steps in this article to edit an existing activation dataflow in Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 2d944c7bd237efbbd4a770b3a6dd03c4133bc901
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Editar fluxos de dados de ativação {#edit-activation-flows}

No Adobe Experience Platform, você pode editar vários componentes de fluxos de dados de ativação existentes para destinos, como os segmentos exportados e atributos de perfil, a frequência de exportação, se o fluxo de dados de ativação estiver ativado ou desativado e muito mais.

Siga as etapas abaixo para editar os fluxos de dados de ativação existentes:

1. Faça logon no [Interface do usuário do Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Destinos]** na barra de navegação esquerda. Selecionar **[!UICONTROL Procurar]** no cabeçalho superior para exibir os fluxos de dados de destino existentes.

   ![Procurar destinos](../assets/ui/edit-activation/browse-destinations.png)

2. Selecione o ícone de filtro ![Ícone Filtro](../assets/ui/edit-activation/filter.png) na parte superior esquerda para iniciar o painel de classificação. O painel de classificação fornece uma lista de todos os destinos. Você pode selecionar mais de um destino na lista para ver uma seleção filtrada de fluxos de dados associada ao destino selecionado.

   ![Filtrar destinos](../assets/ui/edit-activation/filter-destinations.png)

3. Selecione o nome do fluxo de dados de destino que deseja editar.

   ![Selecionar destino](../assets/ui/edit-activation/destination-select.png)

4. O **[!UICONTROL Execuções do fluxo de dados]** será exibida a página de destino, mostrando seus controles disponíveis. Nesse ponto, você pode editar vários componentes do fluxo de dados de destino:

   * Selecionar **[!UICONTROL Ativar segmentos]** no painel direito para alterar quais segmentos ou atributos de perfil serão enviados para o destino. Essa ação direciona você ao fluxo de trabalho de ativação, que varia dependendo do tipo de destino. Para obter mais informações, consulte os guias em:
      * [como ativar dados do público-alvo para segmentar destinos de transmissão](./activate-segment-streaming-destinations.md) (por exemplo, Facebook ou Twitter);
      * [ativação de dados de público-alvo para destinos com base em perfil em lote](./activate-batch-profile-destinations.md) (por exemplo, Amazon S3 ou Oracle Eloqua);
      * [ativação de dados de público-alvo para streaming de destinos com base em perfil](./activate-streaming-profile-destinations.md) (por exemplo, API HTTP ou Amazon Kinesis).
   * Além disso, é possível editar o nome e a descrição do fluxo de dados de destino.
   * Você pode usar o **[!UICONTROL Ativado]/[!UICONTROL Desabilitado]** para iniciar e pausar todas as exportações de dados para o destino.

   ![Detalhes do destino](../assets/ui/edit-activation/destination-details.png)

5. Consulte [Visão geral de Ativation](activation-overview.md) para obter detalhes sobre como ativar novos segmentos para seus destinos.
