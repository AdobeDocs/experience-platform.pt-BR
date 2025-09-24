---
keywords: Experience Platform;home;tópicos populares;conector de banco de dados
solution: Experience Platform
title: Criar um Fluxo de Dados Usando um Source de Banco de Dados na Interface
type: Tutorial
description: Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma origem para um conjunto de dados do Experience Platform. Este tutorial fornece etapas sobre como criar um fluxo de dados para uma origem de banco de dados usando a interface do usuário do Experience Platform.
exl-id: 9fd8a7ec-bbd8-4890-9860-e6defc6cade3
source-git-commit: 2f8589ec58d9afe69e21f909f905a941e43f710c
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Criar um fluxo de dados usando uma fonte de banco de dados na interface

Um fluxo de dados é uma tarefa agendada que recupera e assimila dados de uma origem para um conjunto de dados na Adobe Experience Platform. Este tutorial fornece etapas sobre como criar um fluxo de dados para uma origem de banco de dados usando a interface do usuário do Experience Platform.

>[!NOTE]
>
>* Para criar um fluxo de dados, você já deve ter uma conta autenticada com uma fonte de banco de dados. Uma lista de tutoriais para criar diferentes contas de origem de banco de dados na interface do usuário pode ser encontrada na [visão geral das origens](../../../home.md#database).
>
>* Para que o Experience Platform assimile dados, os fusos horários de todas as fontes de lote baseadas em tabela devem ser configurados como UTC. O único carimbo de data/hora com suporte para [[!DNL Snowflake] origem](../../../connectors/databases/snowflake.md) é TIMESTAMP_NTZ com hora UTC.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)] Sistema](../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Data Prep]](../../../../data-prep/home.md): permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

## Adicionar dados

Depois de criar sua conta de origem de banco de dados, a etapa **[!UICONTROL Adicionar dados]** é exibida, fornecendo uma interface para você explorar a hierarquia de tabela da conta de origem de banco de dados.

* A metade esquerda da interface é um navegador que exibe uma lista das tabelas de dados contidas na sua conta. A interface também inclui uma opção de pesquisa que permite identificar rapidamente os dados de origem que você pretende usar.
* A metade direita da interface é um painel de visualização, que permite visualizar até 100 linhas de dados.

>[!NOTE]
>
>A opção de dados de fonte de pesquisa está disponível para todas as fontes baseadas em tabela, excluindo o Adobe Analytics, [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs].

Depois de localizar os dados de origem, selecione a tabela e, em seguida, selecione **[!UICONTROL Próximo]**.

![selecionar-dados](../../../images/tutorials/dataflow/table-based/select-data.png)

## Fornecer detalhes do fluxo de dados

A página [!UICONTROL Detalhes do fluxo de dados] permite selecionar se você deseja usar um conjunto de dados existente ou um novo conjunto de dados. Durante esse processo, você também pode definir as configurações para [!UICONTROL Conjunto de dados de perfil], [!UICONTROL Diagnóstico de erro], [!UICONTROL Assimilação parcial] e [!UICONTROL Alertas].

![detalhes do fluxo de dados](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Usar um conjunto de dados existente

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de conjuntos de dados existentes no menu suspenso. Depois de selecionar um conjunto de dados, forneça um nome e uma descrição para o fluxo de dados.

![conjunto de dados existente](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Usar um novo conjunto de dados

Para assimilar em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome de conjunto de dados de saída e uma descrição opcional. Em seguida, selecione um esquema para mapear usando a opção [!UICONTROL Pesquisa avançada] ou rolando pela lista de esquemas existentes no menu suspenso. Depois de selecionar um esquema, forneça um nome e uma descrição para o fluxo de dados.

![novo-conjunto-de-dados](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Habilitar [!DNL Profile] e diagnóstico de erro

Em seguida, selecione a opção **[!UICONTROL Conjunto de dados de perfil]** para habilitar seu conjunto de dados para [!DNL Profile]. Isso permite criar uma visualização integral dos atributos e comportamentos de uma entidade. Os dados de todos os conjuntos de dados habilitados para [!DNL Profile] serão incluídos em [!DNL Profile] e as alterações serão aplicadas quando você salvar seu fluxo de dados.

O [!UICONTROL Diagnóstico de erro] habilita a geração de mensagens de erro detalhadas para todos os registros incorretos que ocorrem no fluxo de dados, enquanto a [!UICONTROL Assimilação parcial] permite assimilar dados que contêm erros, até um determinado limite definido manualmente. Consulte a [visão geral da assimilação parcial de lotes](../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

![perfil e erros](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Ativar alertas

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de fontes usando a interface](../alerts.md).

Quando terminar de fornecer detalhes ao seu fluxo de dados, selecione **[!UICONTROL Avançar]**.

![alertas](../../../images/tutorials/dataflow/table-based/alerts.png)

## Mapear campos de dados para um esquema XDM

A etapa [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Ao mapear para esquemas baseados em modelo, certifique-se de que seus dados de origem incluam os campos obrigatórios, como uma chave primária e um identificador de versão ou um identificador de carimbo de data e hora para esquemas de série temporal.

Colunas de controle como `_change_request_type`, usadas para captura de dados de alteração, são lidas durante a assimilação, mas não são armazenadas no esquema de destino.

Os esquemas baseados em modelo também aceitam relações entre conjuntos de dados usando mapeamentos de chave primária e estrangeira.

Para obter mais informações, consulte a [visão geral do Data Mirror](../../../../xdm/data-mirror/overview.md) e a [referência técnica de esquemas baseados em modelo](../../../../xdm/schema/model-based.md).

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![mapeamento](../../../images/tutorials/dataflow/table-based/mapping.png)

## Programar execuções de assimilação

A etapa [!UICONTROL Agendamento] é exibida, permitindo configurar um agendamento de assimilação para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. Por padrão, o agendamento está configurado para `Once`. Para ajustar a frequência de assimilação, selecione **[!UICONTROL Frequência]** e escolha uma opção no menu suspenso.

>[!TIP]
>
>O intervalo e o preenchimento retroativo não ficam visíveis durante uma assimilação única.

![agendando](../../../images/tutorials/dataflow/table-based/scheduling.png)

Se você definir a frequência de assimilação como `Minute`, `Hour`, `Day` ou `Week`, deverá definir um intervalo para estabelecer um intervalo de tempo definido entre cada assimilação. Por exemplo, uma frequência de assimilação definida como `Day` e um intervalo definido como `15` significa que o fluxo de dados está agendado para assimilar dados a cada 15 dias.

Durante esta etapa, você também pode habilitar o **preenchimento retroativo** e definir uma coluna para a assimilação incremental de dados. O preenchimento retroativo é usado para assimilar dados históricos, enquanto a coluna definida para assimilação incremental permite que novos dados sejam diferenciados dos dados existentes.

Consulte a tabela abaixo para obter mais informações sobre como programar configurações.

| Configuração de agendamento | Descrição |
| --- | --- |
| Frequência | Configure a frequência para indicar a frequência de execução do fluxo de dados. Você pode definir a frequência como: <ul><li>**Uma vez**: defina sua frequência como `once` para criar uma assimilação única. As configurações para intervalo e preenchimento retroativo não estão disponíveis ao criar um fluxo de dados de assimilação única. Por padrão, a frequência de agendamento é definida como uma vez.</li><li>**Minuto**: Defina sua frequência como `minute` para agendar seu fluxo de dados para assimilar dados por minuto.</li><li>**Hora**: Defina sua frequência como `hour` para agendar seu fluxo de dados para assimilar dados por hora.</li><li>**Dia**: Defina sua frequência como `day` para agendar seu fluxo de dados para assimilar dados por dia.</li><li>**Semana**: Defina sua frequência como `week` para agendar seu fluxo de dados para assimilar dados por semana.</li></ul> |
| Intervalo | Depois de selecionar uma frequência, você pode definir o intervalo para estabelecer o intervalo de tempo entre cada assimilação. Por exemplo, se você definir a frequência como dia e configurar o intervalo como 15, o fluxo de dados será executado a cada 15 dias. Você não pode definir o intervalo como zero. O valor mínimo de intervalo aceito para cada frequência é o seguinte:<ul><li>**Uma vez**: n/d</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Dia**: 1</li><li>**Semana**: 1</li></ul> |
| Hora de início | O carimbo de data e hora da execução projetada, apresentado no fuso horário UTC. |
| Preenchimento retroativo | O preenchimento retroativo determina quais dados são assimilados inicialmente. Se o preenchimento retroativo estiver ativado, todos os arquivos atuais no caminho especificado serão assimilados durante a primeira assimilação agendada. Se o preenchimento retroativo estiver desativado, somente os arquivos carregados entre a primeira execução da assimilação e a hora de início serão assimilados. Os arquivos carregados antes da hora de início não serão assimilados. |
| Carregar dados incrementais por | Uma opção com um conjunto filtrado de campos de esquema de origem de tipo, data ou hora. O campo selecionado para **[!UICONTROL Carregar dados incrementais por]** deve ter seus valores de data e hora no fuso horário UTC para carregar corretamente os dados incrementais. Todas as origens de lote baseadas em tabela selecionam dados incrementais comparando um valor de carimbo de data/hora da coluna delta com a janela de execução de fluxo correspondente Horário UTC e, em seguida, copiando os dados da origem, se algum dado novo for encontrado na janela de tempo UTC. |

![preenchimento retroativo](../../../images/tutorials/dataflow/table-based/backfill.png)

## Revisar seu fluxo de dados

A etapa **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir campos de mapa e conjunto de dados]**: exibe o conjunto de dados no qual os dados de origem serão assimilados, juntamente com o esquema associado. Se estiver usando um esquema baseado em modelo, verifique se os campos obrigatórios, como a chave primária e o identificador de versão, estão mapeados corretamente. Além disso, verifique se as colunas de controle da captura de dados de alteração estão configuradas corretamente. Os conjuntos de dados que usam esquemas baseados em modelo suportam vários modelos de dados e habilitam [fluxos de trabalho de captura de dados de alteração](../../api/change-data-capture.md).
* **[!UICONTROL Agendamento]**: mostra o período, a frequência e o intervalo ativos do agendamento de assimilação.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![avaliação](../../../images/tutorials/dataflow/table-based/review.png)

## Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre taxas de assimilação, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, consulte o tutorial sobre [monitoramento de contas e fluxos de dados na interface](../monitor.md).

## Excluir seu fluxo de dados

Você pode excluir fluxos de dados que não são mais necessários ou que foram criados incorretamente usando a função **[!UICONTROL Excluir]** disponível no espaço de trabalho **[!UICONTROL Fluxos de Dados]**. Para obter mais informações sobre como excluir fluxos de dados, consulte o tutorial sobre [exclusão de fluxos de dados na interface](../delete.md).

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de dados para trazer dados da fonte do banco de dados para a Experience Platform. Os dados de entrada agora podem ser usados por serviços [!DNL Experience Platform] downstream, como [!DNL Real-Time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do [!DNL Real-Time Customer Profile]](../../../../profile/home.md)
* [Visão geral do [!DNL Data Science Workspace]](../../../../data-science-workspace/home.md)
