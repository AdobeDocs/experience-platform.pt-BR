---
keywords: Experience Platform, home, tópicos populares, conector de armazenamento em nuvem, armazenamento em nuvem
solution: Experience Platform
title: Configurar um fluxo de dados para um conector de fluxo de armazenamento em nuvem na interface do usuário
topic-legacy: overview
type: Tutorial
description: Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma origem em um conjunto de dados da plataforma. Este tutorial fornece etapas para configurar um novo fluxo de dados usando o conector da base de armazenamento em nuvem.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# Configurar um fluxo de dados para uma conexão de fluxo de armazenamento em nuvem na interface do usuário

Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma fonte para um conjunto de dados [!DNL Platform]. Este tutorial fornece etapas para configurar um novo fluxo de dados usando o conector da base de armazenamento em nuvem.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Além disso, este tutorial exige que você já tenha criado um conector de armazenamento em nuvem. Uma lista de tutoriais para criar diferentes conectores de armazenamento em nuvem na interface do usuário pode ser encontrada na [visão geral dos conectores de origem](../../../../home.md).

## Selecionar dados

Depois de criar o conector de armazenamento em nuvem, a etapa *Selecionar dados* é exibida, fornecendo uma interface para selecionar de qual fluxo os dados serão transmitidos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mapear campos de dados para um esquema XDM

A etapa **[!UICONTROL Mapping]** é exibida, fornecendo uma interface interativa para mapear os dados de origem para um conjunto de dados [!DNL Platform].

Escolha um conjunto de dados para os dados de entrada que serão assimilados. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Use existing dataset]** e clique no ícone do conjunto de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

A caixa de diálogo **[!UICONTROL Select dataset]** é exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Usar um novo conjunto de dados**

Para assimilar dados em um novo conjunto de dados, selecione **[!UICONTROL Create new dataset]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Em seguida, selecione o schema que deseja usar na lista suspensa .

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Dê um nome ao seu fluxo de dados

A etapa **[!UICONTROL Dataflow detail]** é exibida, permitindo nomear e fornecer uma breve descrição sobre o novo fluxo de dados.

Forneça valores para o fluxo de dados e clique em **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Revisar o fluxo de dados

A etapa **[!UICONTROL Review]** é exibida, permitindo que você revise o novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

- **[!UICONTROL Source details]**: Mostra o tipo de origem e outros detalhes relevantes sobre a origem.
- **[!UICONTROL Target details]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Finish]** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitorar e excluir o fluxo de dados

Depois que o fluxo de dados do armazenamento em nuvem for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Para obter mais informações sobre monitoramento e exclusão de fluxos de dados, consulte o tutorial em [monitorando fluxos de dados](../../../../../ingestion/quality/monitor-data-ingestion.md).

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para trazer dados de um armazenamento externo em nuvem e ganhou informações sobre o monitoramento de conjuntos de dados. Os dados recebidos agora podem ser usados por serviços [!DNL Platform] downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] visão geral](../../../../../data-science-workspace/home.md)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de dados

Quando um fluxo de dados é criado, ele imediatamente se torna ativo e assimila dados de acordo com o cronograma que foi fornecido. Você pode desativar um fluxo de dados ativo a qualquer momento seguindo as instruções abaixo.

No espaço de trabalho **[!UICONTROL Sources]**, clique na guia **[!UICONTROL Browse]**. Em seguida, clique no nome da conexão associada ao fluxo de dados ativo que você deseja desativar.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

A página **[!UICONTROL Source activity]** é exibida. Selecione o fluxo de dados ativo na lista para abrir sua coluna **[!UICONTROL Properties]** no lado direito da tela, que contém um botão de alternância **[!UICONTROL Enabled]**. Clique no botão de alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Ativar dados de entrada para a população [!DNL Profile]

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados de [!DNL Real-time Customer Profile]. Para obter mais informações sobre como preencher os dados [!DNL Real-time Customer Profile], consulte o tutorial em [População do perfil](../../profile.md).
