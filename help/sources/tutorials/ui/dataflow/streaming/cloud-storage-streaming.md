---
keywords: Experience Platform;página inicial;tópicos populares;streaming;conector de armazenamento em nuvem;armazenamento na nuvem
solution: Experience Platform
title: Criar um fluxo de dados de transmissão para uma fonte de armazenamento em nuvem na interface
type: Tutorial
description: Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma origem para um conjunto de dados da Platform. Este tutorial fornece etapas para configurar um novo fluxo de dados usando seu conector da base de armazenamento na nuvem.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 6419ae7648a91dc7f9432281c1960beccc65bdb0
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# Criar um fluxo de dados de transmissão para uma fonte de armazenamento em nuvem na interface

Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma origem para um conjunto de dados do Adobe Experience Platform. Este tutorial fornece etapas para criar um fluxo de dados de transmissão para uma fonte de armazenamento em nuvem na interface do usuário.

Antes de tentar este tutorial, primeiro você deve estabelecer uma conexão válida e autenticada entre sua conta de armazenamento em nuvem e a Platform. Se você ainda não tiver uma conexão autenticada, consulte um dos seguintes tutoriais para obter informações sobre como autenticar suas contas de armazenamento da nuvem de transmissão:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Fluxos de dados](../../../../../dataflows/home.md): os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, de origens a [!DNL Identity Service], [!DNL Profile] e [!DNL Destinations].
- [Preparo de dados](../../../../../data-prep/home.md): o Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM). O Preparo de dados é exibido como uma etapa de &quot;Mapa&quot; nos processos de Assimilação de dados, incluindo o fluxo de trabalho Assimilação de CSV.
- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Adicionar dados

>[!NOTE]
>
>Você só pode criar um fluxo de dados de origem por grupo de consumidores para um determinado Hub de Eventos.

Depois de criar sua conta de armazenamento de streaming na nuvem, a etapa **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para você selecionar qual fluxo de dados você trará para a Plataforma.

- A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
- A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

![interface](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Selecione o fluxo de dados que deseja usar e selecione **[!UICONTROL Escolher arquivo]** para carregar um esquema de exemplo.

>[!TIP]
>
>Se seus dados forem compatíveis com XDM, você poderá ignorar o carregamento de um esquema de amostra e selecionar **[!UICONTROL Avançar]** para continuar.

![selecionar fluxo](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Depois que o esquema for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário [!UICONTROL Campo de pesquisa] para acessar itens específicos de dentro do esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![visualização de esquema](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Mapeamento

A etapa **[!UICONTROL Mapping]** é exibida, fornecendo uma interface para mapear os dados de origem para um conjunto de dados da plataforma.

Escolha um conjunto de dados para os dados de entrada que serão assimilados. Você pode usar um conjunto de dados existente ou criar um novo.

### Novo conjunto de dados

Para assimilar dados em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Para adicionar um esquema, você pode inserir um nome de esquema existente na caixa de diálogo **[!UICONTROL Selecionar esquema]**. Como alternativa, você pode selecionar **[!UICONTROL Pesquisa avançada de esquema]** para procurar um esquema apropriado.

![novo-conjunto-de-dados](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

A janela [!UICONTROL Selecionar esquema] é exibida, fornecendo uma lista dos esquemas disponíveis para escolha. Selecione um esquema na lista para atualizar o painel direito para exibir detalhes específicos do esquema selecionado, incluindo informações sobre se o esquema está habilitado para [!DNL Profile].

Depois de identificar e selecionar o esquema que deseja usar, selecione **[!UICONTROL Concluído]**.

![selecionar-esquema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

A página [!UICONTROL Conjunto de dados de destino] é atualizada com o esquema selecionado exibido como parte do conjunto de dados. Durante esta etapa, você pode habilitar seu conjunto de dados para [!DNL Profile] e criar uma exibição holística dos atributos e comportamentos de uma entidade. Os dados de todos os conjuntos de dados habilitados serão incluídos em [!DNL Profile] e as alterações serão aplicadas quando você salvar seu fluxo de dados.

Alterne o botão **[!UICONTROL Conjunto de dados de perfil]** para habilitar seu conjunto de dados de destino para [!DNL Profile].

![novo-perfil](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Conjunto de dados existente

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]** e, em seguida, selecione o ícone do conjunto de dados.

![conjunto de dados existente](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

A caixa de diálogo **[!UICONTROL Selecionar conjunto de dados]** é exibida, fornecendo uma lista dos conjuntos de dados disponíveis para escolha. Selecione um conjunto de dados na lista para atualizar o painel direito para exibir detalhes específicos do conjunto de dados selecionado, incluindo informações sobre se o conjunto de dados pode ser habilitado para [!DNL Profile].

Depois de identificar e selecionar o conjunto de dados que deseja usar, selecione **[!UICONTROL Concluído]**.

![selecionar-conjunto-dados](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Depois de selecionar o conjunto de dados, selecione a opção [!DNL Profile] para habilitar o conjunto de dados para [!DNL Profile].

![perfil-existente](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Mapear campos padrão

Com seu conjunto de dados e esquema estabelecidos, a interface **[!UICONTROL Mapear campos padrão]** é exibida, permitindo configurar manualmente os campos de mapeamento para seus dados.

>[!TIP]
>
>A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso.

Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](../../../../../data-prep/ui/mapping.md).

Depois que os dados de origem forem mapeados, selecione **[!UICONTROL Próximo]**.

![mapeamento](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Detalhes do fluxo de dados

A etapa **[!UICONTROL Detalhes do fluxo de dados]** é exibida, permitindo nomear e fornecer uma breve descrição sobre o novo fluxo de dados.

Forneça valores para o fluxo de dados e selecione **[!UICONTROL Próximo]**.

![detalhes do fluxo de dados](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Revisar

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

- **[!UICONTROL Conexão]**: exibe o nome da sua conta, o tipo de origem e outras informações diversas específicas para a fonte de armazenamento da nuvem de streaming que você está usando.
- **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: exibe o conjunto de dados e o esquema de destino que você está usando para o fluxo de dados.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![avaliação](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Monitorar e excluir seu fluxo de dados

Depois que o fluxo de dados de armazenamento na nuvem de transmissão for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Para obter mais informações sobre monitoramento e exclusão de fluxos de dados de transmissão, consulte o tutorial em [monitoramento de fluxos de dados de transmissão](../../monitor-streaming.md).

## Próximas etapas

Seguindo este tutorial, você criou com êxito um fluxo de dados para transmitir dados de uma fonte de armazenamento na nuvem. Os dados de entrada agora podem ser usados por serviços downstream da Platform, como [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
- [Visão geral do [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)