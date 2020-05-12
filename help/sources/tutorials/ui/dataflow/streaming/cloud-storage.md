---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurar um fluxo de dados para um conector de transmissão de armazenamentos em nuvem na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: dca1accc16395de72db6d0cc8eac78f07dd05e03
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# Configurar um fluxo de dados para um conector de transmissão de armazenamentos em nuvem na interface do usuário

Um fluxo de dados é uma tarefa programada que recupera e ingere dados de uma fonte para um conjunto de dados da plataforma. Este tutorial fornece etapas para configurar um novo fluxo de dados usando o conector base do armazenamento em nuvem.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado um conector de armazenamento em nuvem. Uma lista de tutoriais para criar diferentes conectores de armazenamento de nuvem na interface do usuário pode ser encontrada na visão geral [dos conectores de](../../../../home.md)origem.

## Selecionar dados

Depois de criar o conector de armazenamento em nuvem, a etapa *Selecionar dados* é exibida, fornecendo uma interface para selecionar de qual fluxo você fará o stream de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Mapear campos de dados para um schema XDM

A etapa *Mapeamento* é exibida, fornecendo uma interface interativa para mapear os dados de origem para um conjunto de dados da Plataforma.

Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar dados em um conjunto de dados existente, selecione **Usar conjunto de dados** existente e clique no ícone do conjunto de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

A caixa de diálogo _Selecionar conjunto de dados_ é exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **Continuar**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Usar um novo conjunto de dados**

Para assimilar dados em um novo conjunto de dados, selecione **Criar novo conjunto de dados** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Em seguida, selecione o schema que deseja usar na lista suspensa.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Dê um nome ao seu fluxo de dados

A etapa de detalhes *do* Dataflow é exibida, permitindo que você nomeie e forneça uma breve descrição sobre seu novo dataflow.

Forneça valores para o fluxo de dados e clique em **Avançar**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Revisar seu fluxo de dados

A etapa *Revisar* é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

- *Detalhes* da fonte: Mostra o tipo de origem e outros detalhes relevantes sobre a origem.
- *Detalhes* do Público alvo: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o schema ao qual o conjunto de dados adere.

Depois de revisar seu fluxo de dados, clique em **Concluir** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitore seu fluxo de dados

Depois que seu fluxo de dados de armazenamento em nuvem for criado, você poderá monitorar os dados que estão sendo assimilados por ele. Para obter mais informações sobre como monitorar conjuntos de dados, consulte o tutorial sobre como [monitorar fluxos de dados](../../../../../ingestion/quality/monitor-data-flows.md)de transmissão contínua.

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de dados para trazer dados de um armazenamento de nuvem externo e obteve insight sobre conjuntos de dados de monitoramento. Os dados recebidos agora podem ser usados pelos serviços de plataforma downstream, como o Perfil do cliente em tempo real e a Área de trabalho de análise de dados. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
- [Visão geral da Análise do espaço de trabalho da Data Science](../../../../../data-science-workspace/home.md)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de dados

Quando um fluxo de dados é criado, ele imediatamente se torna ativo e ingere dados de acordo com o agendamento que foi fornecido. Você pode desativar um fluxo de dados ativo a qualquer momento seguindo as instruções abaixo.

Na área de trabalho *Fontes* , clique na guia **Procurar** . Em seguida, clique no nome da conexão básica que está associada ao fluxo de dados ativo que você deseja desativar.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

A página *atividade* de origem é exibida. Selecione o fluxo de dados ativo na lista para abrir sua coluna *Propriedades* no lado direito da tela, que contém um botão de alternância **Ativado** . Clique na alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Ativar dados de entrada para população de Perfis

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados de Perfil do cliente em tempo real. Para obter mais informações sobre como preencher os dados do Perfil do cliente real, consulte o tutorial sobre a população [do](../../profile.md)Perfil.
