---
keywords: Experience Platform, home, tópicos populares, configurar fluxo de dados, conector de publicidade
solution: Experience Platform
title: Configurar um fluxo de dados para uma conexão de fonte de publicidade na interface do usuário
topic-legacy: overview
type: Tutorial
description: Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma fonte para um conjunto de dados da Adobe Experience Platform. Este tutorial fornece etapas para configurar um novo fluxo de dados usando sua conta publicitária.
exl-id: 8dd1d809-e812-4a13-8831-189726b2430e
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Configurar um fluxo de dados para uma conexão de publicidade na interface do usuário

Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma fonte para um conjunto de dados da Adobe Experience Platform. Este tutorial fornece etapas para configurar um novo fluxo de dados usando sua conta publicitária.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Além disso, este tutorial exige que você já tenha criado uma conta publicitária. Uma lista de tutoriais para criar diferentes conectores de pagamento na interface do usuário pode ser encontrada no [visão geral dos conectores de origem](../../../home.md).

## Selecionar dados

Depois de criar sua conta publicitária, a variável **[!UICONTROL Selecionar dados]** será exibida, fornecendo uma interface interativa para explorar sua hierarquia de arquivos.

- A metade esquerda da interface é um navegador de diretório, que exibe os arquivos e diretórios do seu servidor.
- A metade direita da interface permite visualizar até 100 linhas de dados de um arquivo compatível.

Você pode usar o **[!UICONTROL Pesquisar]** na parte superior da página para identificar rapidamente os dados de origem que você pretende usar.

>[!NOTE]
>
>A opção de dados de origem da pesquisa está disponível para todos os conectores de origem baseados em tabelas, excluindo os conectores Analytics, Classificações, Hubs de eventos e Kinesis.

Depois de encontrar os dados de origem, selecione o diretório e clique em **[!UICONTROL Próximo]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)


## Mapear campos de dados para um esquema XDM

O **[!UICONTROL Mapeamento]** é exibida, fornecendo uma interface interativa para mapear os dados de origem para um [!DNL Platform] conjunto de dados.

Escolha um conjunto de dados para os dados de entrada que serão assimilados. Você pode usar um conjunto de dados existente ou criar um novo conjunto de dados.

### Usar um conjunto de dados existente

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Usar conjunto de dados existente]** e clique no ícone do conjunto de dados.

![conjunto de dados use-existing](../../../images/tutorials/dataflow/advertising/use-existing-target-dataset.png)

O **[!UICONTROL Selecionar conjunto de dados]** será exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **[!UICONTROL Continuar]**.

![select-existing-dataset](../../../images/tutorials/dataflow/advertising/select-existing-dataset.png)

### Usar um novo conjunto de dados

Para assimilar dados em um novo conjunto de dados, selecione **[!UICONTROL Criar novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos.

Você pode anexar um campo de esquema ao inserir um nome de esquema na variável **[!UICONTROL Selecionar esquema]** barra de pesquisa. Você também pode selecionar o ícone suspenso para ver uma lista de schemas existentes. Como alternativa, você pode selecionar **[!UICONTROL Pesquisa avançada]** para acessar a tela de esquemas existentes, incluindo seus respectivos detalhes.

Durante essa etapa, é possível ativar o conjunto de dados para [!DNL Real-time Customer Profile] e criar uma visualização holística dos atributos e comportamentos de uma entidade. Os dados de todos os conjuntos de dados ativados serão incluídos em [!DNL Profile] As alterações e são aplicadas quando você salva o fluxo de dados.

Ative o **[!UICONTROL Conjunto de dados de perfil]** para ativar seu conjunto de dados de destino para [!DNL Profile].

![create-new-dataset](../../../images/tutorials/dataflow/advertising/target-dataset.png)

O **[!UICONTROL Selecionar esquema]** será exibida. Selecione o schema que deseja aplicar ao novo conjunto de dados e clique em **[!DNL Done]**.

![select-schema](../../../images/tutorials/dataflow/advertising/select-existing-schema.png)

Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e dos campos calculados, consulte o [Guia da interface do usuário de preparação de dados](../../../../data-prep/ui/mapping.md).

>[!TIP]
>
>A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema de destino ou conjunto de dados selecionado. Você pode ajustar manualmente as regras de mapeamento de acordo com seus casos de uso.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Selecionar **[!UICONTROL Visualizar dados]** para ver os resultados de mapeamento de até 100 linhas de dados de amostra do conjunto de dados selecionado.

Durante a visualização, a coluna de identidade é priorizada como o primeiro campo, pois são as informações principais necessárias ao validar resultados de mapeamento.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Depois que os dados de origem forem mapeados, selecione **[!UICONTROL Fechar]**.

## Agendar execução de ingestão

O **[!UICONTROL Agendamento]** é exibida, permitindo configurar um agendamento de assimilação para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. A tabela a seguir descreve os diferentes campos configuráveis para programação:

| Campo | Descrição |
| --- | --- |
| Frequência | As frequências selecionáveis incluem `Once`, `Minute`, `Hour`, `Day`e `Week`. |
| Intervalo | Um número inteiro que define o intervalo para a frequência selecionada. |
| Hora de início | Um carimbo de data e hora UTC indicando quando a primeira assimilação está definida para ocorrer. |
| Preenchimento retroativo | Um valor booleano que determina quais dados são assimilados inicialmente. If **[!UICONTROL Preenchimento retroativo]** estiver habilitado, todos os arquivos atuais no caminho especificado serão assimilados durante a primeira assimilação agendada. If **[!UICONTROL Preenchimento retroativo]** estiver desativado, somente os arquivos carregados entre a primeira execução da assimilação e a hora de início serão assimilados. Os arquivos carregados antes da hora de início não serão assimilados. |
| Coluna Delta | Uma opção com um conjunto filtrado de campos do schema de origem do tipo, data ou hora. Esse campo é usado para diferenciar dados novos e existentes. Os dados incrementais serão assimilados com base no carimbo de data e hora da coluna selecionada. |

Os fluxos de dados são projetados para assimilar dados automaticamente de forma programada. Comece selecionando a frequência de assimilação. Em seguida, defina o intervalo para designar o período entre duas execuções de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero e deve ser definido como maior ou igual a 15.

Para definir a hora de início da assimilação, ajuste a data e a hora exibidas na caixa de hora de início. Como alternativa, você pode selecionar o ícone de calendário para editar o valor de hora de início. A hora de início deve ser maior ou igual à hora UTC atual.

Selecionar **[!UICONTROL Carregar dados incrementais por]** para atribuir a coluna delta. Este campo estabelece uma distinção entre dados novos e dados existentes.

![intervalo de agendamento](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Configurar um fluxo de dados de ingestão único

Para configurar a assimilação única, selecione a seta suspensa de frequência e selecione **[!UICONTROL Uma vez]**.

>[!TIP]
>
>**[!UICONTROL Intervalo]** e **[!UICONTROL Preenchimento retroativo]** não são visíveis durante uma ingestão única.

Depois de fornecer os valores apropriados ao agendamento, selecione **[!UICONTROL Próximo]**.

![agendar uma vez](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Fornecer detalhes do fluxo de dados

O **[!UICONTROL Detalhes do fluxo de dados]** será exibida, permitindo nomear e fornecer uma breve descrição sobre o novo fluxo de dados.

Durante esse processo, também é possível ativar **[!UICONTROL Ingestão parcial]** e **[!UICONTROL Diagnóstico de erros]**. Habilitar **[!UICONTROL Ingestão parcial]** O oferece a capacidade de assimilar dados que contenham erros até um determinado limite. Uma vez **[!UICONTROL Ingestão parcial]** estiver ativado, arraste a **[!UICONTROL Limite de erros %]** disque para ajustar o limite de erro do lote. Como alternativa, você pode ajustar manualmente o limite selecionando a caixa de entrada. Para obter mais informações, consulte o [visão geral da ingestão parcial de lote](../../../../ingestion/batch-ingestion/partial.md).
Forneça valores para o fluxo de dados e selecione **[!UICONTROL Próximo]**.

![detalhes do fluxo de dados](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Revisar o fluxo de dados

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

- **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas dentro desse arquivo de origem.
- **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.
- **[!UICONTROL Agendamento]**: Mostra o período ativo, a frequência e o intervalo do agendamento de ingestão.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![revisão](../../../images/tutorials/dataflow/advertising/review.png)

## Monitorar o fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre taxas de ingestão, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, consulte o tutorial em [monitoramento de contas e fluxos de dados na interface do usuário](../monitor.md).

## Excluir seu fluxo de dados

É possível excluir os fluxos de dados que não são mais necessários ou foram criados incorretamente usando o **[!UICONTROL Excluir]** disponível na função **[!UICONTROL Fluxos de dados]** espaço de trabalho. Para obter mais informações sobre como excluir fluxos de dados, consulte o tutorial em [exclusão de fluxos de dados na interface do usuário](../delete.md).

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para trazer dados de um sistema de automação de marketing e ganhou informações sobre o monitoramento de conjuntos de dados. Os dados recebidos agora podem ser usados pelo downstream [!DNL Platform] serviços como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

- [Visão geral do perfil do cliente em tempo real](../../../../profile/home.md)
- [Visão geral do Data Science Workspace](../../../../data-science-workspace/home.md)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de dados

Quando um fluxo de dados é criado, ele imediatamente se torna ativo e assimila dados de acordo com o cronograma que foi fornecido. Você pode desativar um fluxo de dados ativo a qualquer momento seguindo as instruções abaixo.

No **[!UICONTROL Fluxos de dados]** selecione o nome do fluxo de dados que deseja desativar.

![browse-dataset-flow](../../../images/tutorials/dataflow/advertising/view-dataset-flows.png)

O **[!UICONTROL Propriedades]** é exibida no lado direito da tela. Esse painel contém um **[!UICONTROL Ativado]** botão de alternância. Clique no botão de alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![disable](../../../images/tutorials/dataflow/advertising/disable.png)

### Ativar dados de entrada para [!DNL Profile] população

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher [!DNL Real-time Customer Profile] dados. Para obter mais informações sobre como preencher [!DNL Real-time Customer Profile] dados, consulte o tutorial em [População do perfil](../profile.md).
