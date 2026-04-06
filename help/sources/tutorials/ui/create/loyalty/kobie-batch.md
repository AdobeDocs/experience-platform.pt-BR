---
title: Assimilar Dados Em Lote Do Kobie No Experience Platform Usando A Interface Do
description: Saiba como assimilar dados em lote do Kobie na Adobe Experience Platform usando a interface do.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 3cba7ab5ddadc0f3b940f25280eb66a85725d1a6
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 1%

---

# Assimilar dados em lote de [!DNL Kobie] no Experience Platform usando a interface

Leia este tutorial para saber como assimilar dados em lote da conta do [!DNL Kobie] na Adobe Experience Platform usando o espaço de trabalho de fontes na interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

>[!IMPORTANT]
>
>Leia a [[!DNL Kobie] visão geral](../../../../connectors/loyalty/kobie.md) para saber mais sobre as etapas de pré-requisito que você precisa concluir antes de conectar sua conta à Experience Platform.

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Sources]*. Selecione a categoria apropriada no painel *[!UICONTROL Categories]*. Como alternativa, use a barra de pesquisa para navegar até a fonte específica que deseja usar.

Para assimilar dados de [!DNL Kobie], selecione o cartão de origem **[!UICONTROL Kobie Batch Source Connector]** em *[!UICONTROL Loyalty]* e selecione **[!UICONTROL Add data]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Set up]** quando uma determinada origem ainda não tem uma conta autenticada. Depois que uma conta autenticada é criada, esta opção muda para **[!UICONTROL Add data]**.



### Criar uma nova conta

Para criar uma nova conta para sua origem [!DNL Kobie], selecione **[!UICONTROL New account]** e forneça um nome e uma descrição opcional para sua conta. Em seguida, forneça seu domínio [!DNL Kobie] e seu [!UICONTROL Kobie Management API Key]. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde alguns instantes para estabelecer sua conexão.



### Usar uma conta existente

Para usar uma conta existente, selecione **[!UICONTROL Existing account]** e selecione a conta [!DNL Kobie] que deseja usar na interface de contas.

## Selecionar dados

Após a autenticação, forneça valores para o **applicationId** e o **sessionType**. Durante essa etapa, é possível usar as funcionalidades de visualização para inspecionar a estrutura dos dados. Quando terminar, selecione **[!UICONTROL Next]** para continuar.



## Configurar detalhes do conjunto de dados e do fluxo de dados

Em seguida, você deve fornecer informações sobre o conjunto de dados e o fluxo de dados.

### Detalhes do conjunto de dados

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas/campos) e registros (linhas). Os dados assimilados com sucesso na Experience Platform são mantidos no data lake como conjuntos de dados.

Durante essa etapa, é possível usar um conjunto de dados existente ou criar um novo.

>[!NOTE]
>
>Independentemente de você usar um conjunto de dados existente ou criar um novo, você deve garantir que seu conjunto de dados esteja **habilitado para assimilação do Perfil**.

+++Selecione para obter as etapas para ativar a Assimilação de perfil, Diagnóstico de erro e Assimilação parcial.

Se o conjunto de dados estiver habilitado para o Perfil de Cliente em Tempo Real, durante essa etapa você poderá alternar entre **[!UICONTROL Profile dataset]** e habilitar os dados para assimilação de Perfil. Você também pode usar esta etapa para habilitar **[!UICONTROL Error diagnostics]** e **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Selecione **[!UICONTROL Error diagnostics]** para instruir a origem a produzir diagnósticos de erro que você poderá consultar posteriormente ao monitorar a atividade do conjunto de dados e o status do fluxo de dados.
* **[!UICONTROL Partial ingestion]**: Assimilação parcial em lote é a capacidade de assimilar dados que contêm erros, até um determinado limite configurável. Esse recurso permite assimilar com sucesso todos os seus dados precisos na Experience Platform, enquanto todos os seus dados incorretos são armazenados em lote separadamente com informações sobre por que são inválidos.

+++

## Detalhes do fluxo de dados

Depois que o conjunto de dados é configurado, você deve fornecer detalhes sobre o fluxo de dados, incluindo um nome, uma descrição opcional e configurações de alerta.



| Configurações de fluxo de dados | Descrição |
| --- | --- |
| Nome do fluxo de dados | O nome do fluxo de dados. Por padrão, esse campo usará o nome do arquivo que está sendo importado. |
| Descrição | (Opcional) Uma breve descrição do fluxo de dados. |
| Alertas | O Experience Platform pode produzir alertas baseados em eventos, nos quais os usuários podem assinar. Essas opções permitem que um fluxo de dados em execução acione esses alertas.  Para obter mais informações, leia a [visão geral dos alertas](../../alerts.md) <ul><li>**Início da Execução do Fluxo de Dados de Fontes**: selecione este alerta para receber uma notificação quando a execução do fluxo de dados começar.</li><li>**Êxito na Execução do Fluxo de Dados de Fontes**: selecione este alerta para receber uma notificação se o fluxo de dados terminar sem erros.</li><li>**Falha na execução do fluxo de dados de fontes**: selecione este alerta para receber uma notificação se a execução do fluxo de dados terminar com erros.</li></ul> |

{style="table-layout:auto"}

## Mapeamento

Com o conjunto de dados e os detalhes do fluxo de dados configurados, agora é possível continuar a mapear os campos de dados de origem para os campos XDM de destino apropriados. Use a interface de mapeamento para mapear os dados de origem para os campos de esquema apropriados antes de assimilar dados na Experience Platform. Para obter mais informações, leia o [guia de mapeamento na interface](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Para obter orientação adicional sobre como mapear os dados de origem do [!DNL Kobie], leia a [[!DNL Kobie] visão geral]



## Agendar a assimilação do fluxo de dados

A etapa [!UICONTROL Scheduling] é exibida. Use a interface para configurar uma programação de assimilação para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. Por padrão, o agendamento está configurado para `Once`. Para ajustar a frequência de assimilação, selecione **[!UICONTROL Frequency]** e, em seguida, selecione uma opção no menu suspenso.

>[!TIP]
>
>O intervalo e o preenchimento retroativo não ficam visíveis durante uma assimilação única.

Se você definir a frequência de assimilação como `Minute`, `Hour`, `Day` ou `Week`, deverá definir um intervalo para estabelecer um intervalo de tempo definido entre cada assimilação. Por exemplo, uma frequência de assimilação definida como `Day` e um intervalo definido como `15` significa que o fluxo de dados está agendado para assimilar dados a cada 15 dias.

Durante esta etapa, você também pode habilitar o **preenchimento retroativo** e definir uma coluna para a assimilação incremental de dados. O preenchimento retroativo é usado para assimilar dados históricos, enquanto a coluna definida para assimilação incremental permite que novos dados sejam diferenciados dos dados existentes.

Consulte a tabela abaixo para obter mais informações sobre como programar configurações.

| Configuração de agendamento | Descrição |
| --- | --- |
| Frequência | Configure a frequência para indicar a frequência de execução do fluxo de dados. Você pode definir a frequência como: <ul><li>**Uma vez**: defina sua frequência como `once` para criar uma assimilação única. As configurações para intervalo e preenchimento retroativo não estão disponíveis ao criar um fluxo de dados de assimilação única. Por padrão, a frequência de agendamento é definida como uma vez.</li><li>**Minuto**: Defina sua frequência como `minute` para agendar seu fluxo de dados para assimilar dados por minuto.</li><li>**Hora**: Defina sua frequência como `hour` para agendar seu fluxo de dados para assimilar dados por hora.</li><li>**Dia**: Defina sua frequência como `day` para agendar seu fluxo de dados para assimilar dados por dia.</li><li>**Semana**: Defina sua frequência como `week` para agendar seu fluxo de dados para assimilar dados por semana.</li></ul> |
| Intervalo | Depois de selecionar uma frequência, você pode definir o intervalo para estabelecer o intervalo de tempo entre cada assimilação. Por exemplo, se você definir a frequência como dia e configurar o intervalo como 15, o fluxo de dados será executado a cada 15 dias. Você não pode definir o intervalo como zero. O valor mínimo de intervalo aceito para cada frequência é o seguinte:<ul><li>**Uma vez**: n/d</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Dia**: 1</li><li>**Semana**: 1</li></ul> |
| Hora de início | O carimbo de data e hora da execução projetada, apresentado no fuso horário UTC. |
| Preenchimento retroativo | O preenchimento retroativo determina quais dados são assimilados inicialmente. Se o preenchimento retroativo estiver ativado, todos os arquivos atuais no caminho especificado serão assimilados durante a primeira assimilação agendada. Se o preenchimento retroativo estiver desativado, somente os arquivos carregados entre a primeira execução da assimilação e a hora de início serão assimilados. Os arquivos carregados antes da hora de início não serão assimilados. |



## Revisar

A etapa *[!UICONTROL Review]* é exibida, permitindo que você revise os detalhes do fluxo de dados antes que ele seja criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Connection]**: mostra o nome da conta, a plataforma de origem e o nome de origem.
* **[!UICONTROL Assign dataset and map fields]**: mostra o conjunto de dados de destino e o esquema ao qual o conjunto de dados pertence.

Depois de confirmar que os detalhes estão corretos, selecione **[!UICONTROL Finish]**.



## Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para ver informações sobre taxas de assimilação, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, consulte o tutorial sobre [monitoramento de contas e fluxos de dados na interface](../../../../../dataflows/ui/monitor-sources.md).
