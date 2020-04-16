---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurar um fluxo de dados para um conector de protocolo na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 8a331e6711fab6f1823ff2ad030e5077e24d22d3

---


# Configurar um fluxo de dados para um conector de protocolo na interface do usuário

Um fluxo de conjunto de dados é uma tarefa programada que recupera e assimila dados de uma fonte para um conjunto de dados da plataforma Adobe Experience. Este tutorial fornece etapas para configurar um novo fluxo de conjunto de dados usando sua conta de protocolos.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado uma conta de protocolos. Uma lista de tutoriais para criar conectores de protocolo diferentes na interface do usuário pode ser encontrada na visão geral [dos conectores de](../../../home.md)origem.

## Selecionar dados

Depois de criar sua conta de protocolos, a etapa *Selecionar dados* é exibida, fornecendo uma interface interativa para que você explore sua hierarquia de arquivos.

- A metade esquerda da interface é um navegador de diretório que exibe os arquivos e diretórios do servidor.
- A metade direita da interface permite que você pré-visualização até 100 linhas de dados de um arquivo compatível.

Selecione o diretório que deseja usar e clique em **Avançar**.

![add-data](../../../images/tutorials/dataflow/protocols/add-data.png)

## Mapear campos de dados para um schema XDM

A etapa *Mapeamento* é exibida, fornecendo uma interface interativa para mapear os dados de origem para um conjunto de dados da Plataforma.

Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo conjunto de dados.

### Usar um conjunto de dados existente

Para assimilar dados em um conjunto de dados existente, selecione **Usar conjunto de dados** existente e clique no ícone do conjunto de dados.

![use-exist-dataset](../../../images/tutorials/dataflow/protocols/use-existing-dataset.png)

A caixa de diálogo *Selecionar conjunto de dados* é exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **Continuar**.

![select-exists-dataset](../../../images/tutorials/dataflow/protocols/select-existing-dataset.png)

### Usar um novo conjunto de dados

Para assimilar dados em um novo conjunto de dados, selecione **Criar novo conjunto de dados** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos.

Durante esse processo, você também pode ativar a assimilação *parcial* e o diagnóstico *de* erro. Habilitar a ingestão *parcial* fornece a capacidade de assimilar dados que contêm erros, até um certo limite que você pode definir. Ativar o diagnóstico de erro fornece detalhes sobre quaisquer dados incorretos que sejam armazenados em lote separadamente. Para obter mais informações, consulte a visão geral [](../../../../ingestion/batch-ingestion/partial.md)da ingestão em lote parcial.

Quando terminar, clique no ícone schema.

![create-new-dataset](../../../images/tutorials/dataflow/protocols/use-new-dataset.png)

A caixa de diálogo *Selecionar schema* é exibida. Selecione o schema que deseja aplicar ao novo conjunto de dados e clique em **Concluído**.

![select-schema](../../../images/tutorials/dataflow/protocols/select-existing-schema.png)

Com base em suas necessidades, você pode optar por mapear os campos diretamente ou usar as funções do mapeador para transformar dados de origem para derivar valores calculados ou calculados. Para obter mais informações sobre funções de mapeamento e mapeamento de dados, consulte o tutorial sobre como [mapear dados CSV para campos](../../../../ingestion/tutorials/map-a-csv-file.md)de schema XDM.

A tela *Mapeamento* também permite definir a coluna ** Delta. Quando o fluxo do conjunto de dados é criado, é possível definir qualquer campo de carimbo de data e hora como base para decidir quais registros serão assimilados em ingestões incrementais programadas.

Depois que os dados de origem forem mapeados, clique em **Avançar**.

![](../../../images/tutorials/dataflow/protocols/mapping.png)

A etapa *Agendamento* é exibida, permitindo que você configure um agendamento de ingestão para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. A tabela a seguir descreve os diferentes campos configuráveis para programação:

| Campo | Descrição |
| --- | --- |
| Frequência | As frequências selecionáveis incluem Minuto, Hora, Dia e Semana. |
| Intervalo | Um número inteiro que define o intervalo para a frequência selecionada. |
| hora do Start | Um carimbo de data e hora UTC para o qual ocorrerá a primeira ingestão. |
| Backfill | Um valor booliano que determina quais dados são inicialmente assimilados. Se o *preenchimento retroativo* estiver ativado, todos os arquivos atuais no caminho especificado serão ingeridos durante a primeira ingestão programada. Se o *preenchimento retroativo* estiver desativado, somente os arquivos carregados entre a primeira execução da ingestão e a hora *do* Start serão assimilados. Os arquivos carregados antes da hora *do* Start não serão ingeridos. |

Os fluxos de conjuntos de dados são projetados para assimilar dados automaticamente de acordo com uma programação. Se desejar ingerir apenas uma vez por meio desse fluxo de trabalho, você pode fazer isso configurando a **Frequência** para &quot;Dia&quot; e aplicando um número muito grande para o **Intervalo**, como 10000 ou semelhante.

Forneça os valores para o agendamento e clique em **Avançar**.

![programação](../../../images/tutorials/dataflow/protocols/scheduling.png)

## Nomear o fluxo do conjunto de dados

A etapa de detalhes *do fluxo do conjunto de* dados é exibida, onde você deve fornecer um nome e uma descrição opcional para o fluxo do conjunto de dados. Clique em **Avançar** ao concluir.

![dataset-flow-details](../../../images/tutorials/dataflow/protocols/dataset-flow-details.png)

## Revisar o fluxo do conjunto de dados

A etapa *Revisar* é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

- *Conexão*: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
- *Atribuir campos* do conjunto de dados e mapear: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o schema ao qual o conjunto de dados adere.
- *Agendamento*: Mostra o período ativo, a frequência e o intervalo do agendamento da ingestão.

Depois de revisar seu fluxo de dados, clique em **Concluir** e aguarde algum tempo para que o fluxo de dados seja criado.

![revisão](../../../images/tutorials/dataflow/protocols/review.png)

## Monitorar o fluxo do conjunto de dados

Depois que o fluxo do conjunto de dados for criado, você poderá monitorar os dados que estão sendo assimilados por ele. Para obter mais informações sobre como monitorar os fluxos do conjunto de dados, consulte o tutorial sobre [contas e fluxos](../monitor.md)do conjunto de dados.

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de conjunto de dados para trazer dados de um sistema de automação de marketing e obteve informações sobre o monitoramento de conjuntos de dados. Os dados recebidos agora podem ser usados pelos serviços de plataforma downstream, como o Perfil do cliente em tempo real e a Área de trabalho de análise de dados. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do Perfil do cliente em tempo real](../../../../profile/home.md)
- [Visão geral da Análise do espaço de trabalho da Data Science](../../../../data-science-workspace/home.md)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de conjunto de dados

Quando um fluxo de conjunto de dados é criado, ele imediatamente se torna ativo e ingere dados de acordo com o agendamento fornecido. Você pode desativar um fluxo de conjunto de dados ativo a qualquer momento seguindo as instruções abaixo.

Na tela Fluxos *do* conjunto de dados, selecione o nome do fluxo do conjunto de dados que deseja desativar.

![browse-dataset-flow](../../../images/tutorials/dataflow/protocols/view-dataset-flows.png)

A coluna *Propriedades* é exibida no lado direito da tela. Este painel contém um botão de alternância **Ativado** . Clique na alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![disable](../../../images/tutorials/dataflow/protocols/disable.png)

### Ativar dados de entrada para população de Perfis

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados de Perfil do cliente em tempo real. Para obter mais informações sobre como preencher os dados do Perfil do cliente real, consulte o tutorial sobre a população [do](../profile.md)Perfil.