---
keywords: Experience Platform;home;popular topics;cloud storage connector;cloud storage
solution: Experience Platform
title: Configurar um fluxo de dados para um conector de transmissão de armazenamentos em nuvem na interface do usuário
topic: overview
description: Um fluxo de dados é uma tarefa programada que recupera e ingere dados de uma fonte para um conjunto de dados da plataforma. Este tutorial fornece etapas para configurar um novo fluxo de dados usando o conector base do armazenamento em nuvem.
translation-type: tm+mt
source-git-commit: c1b493de7374cbd1c916d90f9382574f831e11e3
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---


# Configurar um fluxo de dados para um conector de transmissão de armazenamentos em nuvem na interface do usuário

Um fluxo de dados é uma tarefa programada que recupera e ingere dados de uma fonte para um [!DNL Platform] conjunto de dados. Este tutorial fornece etapas para configurar um novo fluxo de dados usando o conector base do armazenamento em nuvem.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado um conector de armazenamento em nuvem. Uma lista de tutoriais para criar diferentes conectores de armazenamento de nuvem na interface do usuário pode ser encontrada na visão geral [dos conectores de](../../../../home.md)origem.

## Selecionar dados

Depois de criar o conector de armazenamento em nuvem, a etapa *Selecionar dados* é exibida, fornecendo uma interface para selecionar de qual fluxo você fará o stream de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mapear campos de dados para um schema XDM

A etapa **[!UICONTROL Mapeamento]** é exibida, fornecendo uma interface interativa para mapear os dados de origem para um [!DNL Platform] conjunto de dados.

Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Usar conjunto de dados]** existente e clique no ícone do conjunto de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

A caixa de diálogo **[!UICONTROL Selecionar conjunto de dados]** é exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Usar um novo conjunto de dados**

Para assimilar dados em um novo conjunto de dados, selecione **[!UICONTROL Criar novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Em seguida, selecione o schema que deseja usar na lista suspensa.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Dê um nome ao seu fluxo de dados

A etapa de detalhes **[!UICONTROL do]** Dataflow é exibida, permitindo que você nomeie e forneça uma breve descrição sobre seu novo dataflow.

Forneça valores para o fluxo de dados e clique em **[!UICONTROL Avançar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Revisar seu fluxo de dados

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

- **[!UICONTROL Detalhes]** da fonte: Mostra o tipo de origem e outros detalhes relevantes sobre a origem.
- **[!UICONTROL Detalhes]** do público alvo: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o schema ao qual o conjunto de dados adere.

Depois de revisar seu fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitore e exclua seu fluxo de dados

Depois que seu fluxo de dados de armazenamento em nuvem for criado, você poderá monitorar os dados que estão sendo assimilados por ele. Para obter mais informações sobre monitoramento e exclusão de fluxos de dados, consulte o tutorial sobre [monitoramento de fluxos de dados](../../../../../ingestion/quality/monitor-data-flows.md).

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de dados para trazer dados de um armazenamento de nuvem externo e obteve insight sobre conjuntos de dados de monitoramento. Os dados recebidos agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] visão geral](../../../../../data-science-workspace/home.md)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de dados

Quando um fluxo de dados é criado, ele imediatamente se torna ativo e ingere dados de acordo com o agendamento que foi fornecido. Você pode desativar um fluxo de dados ativo a qualquer momento seguindo as instruções abaixo.

Na área de trabalho **[!UICONTROL Fontes]** , clique na guia **[!UICONTROL Procurar]** . Em seguida, clique no nome da conexão que está associada ao fluxo de dados ativo que você deseja desativar.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

A página **[!UICONTROL atividade]** de origem é exibida. Selecione o fluxo de dados ativo na lista para abrir sua coluna **[!UICONTROL Propriedades]** no lado direito da tela, que contém um botão de alternância **[!UICONTROL Ativado]** . Clique na alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Ativar dados de entrada para [!DNL Profile] população

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher seus [!DNL Real-time Customer Profile] dados. Para obter mais informações sobre como preencher seus [!DNL Real-time Customer Profile] dados, consulte o tutorial sobre a população [do](../../profile.md)Perfil.
