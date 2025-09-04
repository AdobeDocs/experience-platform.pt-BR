---
title: Assimilar dados de pagamentos de sua conta do Stripe para o Experience Platform usando a interface do usuário.
description: Saiba como assimilar dados de pagamentos de sua conta do Stripe para o Experience Platform usando a interface do usuário.
badge: Beta
exl-id: f20c5935-a7c0-4387-b29e-73e78cab4972
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '1637'
ht-degree: 3%

---

# Assimilar dados de pagamentos de sua conta [!DNL Stripe] para a Experience Platform usando a interface do usuário

Leia o tutorial a seguir para saber como assimilar dados de pagamentos de sua conta do [!DNL Stripe] para a Adobe Experience Platform usando a interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Autenticação

Leia a [[!DNL Stripe] visão geral](../../../../connectors/payments/stripe.md) para obter informações sobre como recuperar suas credenciais de autenticação.

## Conectar sua conta do [!DNL Stripe] {#connect}

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Pagamentos*, selecione **[!DNL Stripe]** e **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Quando uma conta autenticada existir, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens na interface do usuário do Experience Platform, com o cartão de origem do Stripe selecionado.](../../../../images/tutorials/create/stripe/catalog.png)

A página **[!UICONTROL Conectar conta do Stripe]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

>[!BEGINTABS]

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A interface de criação de nova conta do fluxo de trabalho de origens.](../../../../images/tutorials/create/stripe/new.png)

| Credencial | Descrição |
| --- | --- |
| Token de acesso | Seu token de acesso [!DNL Stripe]. Para obter informações sobre como recuperar o token de acesso, leia o [[!DNL Stripe] guia de autenticação](../../../../connectors/payments/stripe.md). |

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e a conta que deseja usar no catálogo de contas existente.

Selecione **[!UICONTROL Avançar]** para continuar.

![A página de seleção de conta existente do catálogo de fontes.](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## Selecionar dados {#select-data}

Agora que você tem acesso à sua conta, deve identificar o caminho apropriado para os dados do [!DNL Stripe] que deseja assimilar. Selecione **[!UICONTROL Caminho do recurso]** e selecione o ponto de extremidade de onde deseja assimilar dados. Os pontos de extremidade [!DNL Stripe] disponíveis são:

* Encargos
* Assinaturas
* Reembolsos
* Transações de Saldo
* Clientes
* Preços

![A janela suspensa de caminho de recurso.](../../../../images/tutorials/create/stripe/select-resource-path.png)

Depois que o ponto de extremidade é selecionado, a interface é atualizada em uma tela de visualização, exibindo a estrutura de dados do ponto de extremidade [!DNL Stripe] selecionado. Selecione **[!UICONTROL Avançar]** para continuar.

![A janela de visualização dos dados do Stripe.](../../../../images/tutorials/create/stripe/preview.png)

## Fornecer detalhes do conjunto de dados e do fluxo de dados {#provide-dataset-and-dataflow-details}

Em seguida, você deve fornecer informações sobre seu conjunto de dados e seu fluxo de dados.

### Detalhes do conjunto de dados {#dataset-details}

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os dados assimilados com sucesso na Experience Platform são armazenados no data lake como conjuntos de dados. Durante essa etapa, você pode criar um novo conjunto de dados ou usar um conjunto de dados existente.

>[!BEGINTABS]

>[!TAB Usar um novo conjunto de dados]

Para usar um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e forneça um nome e uma descrição opcional para seu conjunto de dados. Você também deve selecionar um esquema do Experience Data Model (XDM) ao qual seu conjunto de dados adere.

![A nova interface de seleção do conjunto de dados.](../../../../images/tutorials/create/stripe/new-dataset.png)

| Detalhes do novo conjunto de dados | Descrição |
| --- | --- |
| Nome do conjunto de dados de saída | O nome do novo conjunto de dados. |
| Descrição | (Opcional) Uma breve explicação do novo conjunto de dados. |
| Esquema | Uma lista suspensa de esquemas que existem em sua organização. Você também pode criar seu próprio esquema antes do processo de configuração de origem. Para obter mais informações, leia o manual sobre [criação de um esquema XDM na interface](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Usar um conjunto de dados existente]

Se você já tiver um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]** e use a opção **[!UICONTROL Pesquisa avançada]** para exibir uma janela de todos os conjuntos de dados na sua organização, incluindo seus respectivos detalhes, como se eles estão habilitados para assimilação no Perfil do cliente em tempo real ou não.

![A interface de seleção do conjunto de dados existente.](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++Selecione para obter as etapas para ativar a Assimilação de perfil, Diagnóstico de erro e Assimilação parcial.

Se o seu conjunto de dados estiver habilitado para o Perfil de cliente em tempo real, durante essa etapa você poderá alternar para **[!UICONTROL o conjunto de dados do perfil]** para habilitar seus dados para assimilação de perfil. Você também pode usar esta etapa para habilitar o **[!UICONTROL Diagnóstico de erro]** e a **[!UICONTROL Assimilação parcial]**.

* **[!UICONTROL Diagnóstico de erro]**: selecione **[!UICONTROL Diagnóstico de erro]** para instruir a origem a produzir o diagnóstico de erro que você poderá consultar posteriormente ao monitorar a atividade do conjunto de dados e o status do fluxo de dados.
* **[!UICONTROL Assimilação parcial]**: a assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros, até um determinado limite configurável. Esse recurso permite assimilar com sucesso todos os seus dados precisos na Experience Platform, enquanto todos os seus dados incorretos são armazenados em lote separadamente com informações sobre por que são inválidos.

+++

### Detalhes do fluxo de dados {#dataflow-details}

Depois que o conjunto de dados é configurado, você deve fornecer detalhes sobre o fluxo de dados, incluindo um nome, uma descrição opcional e configurações de alerta.

![A etapa de configuração de detalhes do fluxo de dados.](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| Configurações de fluxo de dados | Descrição |
| --- | --- |
| Nome do fluxo de dados | O nome do fluxo de dados.  Por padrão, esse campo usará o nome do arquivo que está sendo importado. |
| Descrição | (Opcional) Uma breve descrição do fluxo de dados. |
| Alertas | O Experience Platform pode produzir alertas baseados em eventos que os usuários podem assinar. Todas essas opções exigem um fluxo de dados em execução para serem acionadas.  Para obter mais informações, leia a [visão geral dos alertas](../../alerts.md) <ul><li>**Início da Execução do Fluxo de Dados de Fontes**: selecione este alerta para receber uma notificação quando a execução do fluxo de dados começar.</li><li>**Êxito na Execução do Fluxo de Dados de Fontes**: selecione este alerta para receber uma notificação se o fluxo de dados terminar sem erros.</li><li>**Falha na execução do fluxo de dados de fontes**: selecione este alerta para receber uma notificação se a execução do fluxo de dados terminar com erros.</li></ul> |

Quando terminar, selecione **[!UICONTROL Avançar]** para continuar.

## Mapear campos para um esquema XDM {#mapping}

A etapa **[!UICONTROL Mapping]** é exibida. Use a interface de mapeamento para mapear os dados de origem para os campos de esquema apropriados antes de assimilar esses dados na Experience Platform. Para obter um guia abrangente sobre como usar a interface de mapeamento, leia o [guia da interface do usuário do Preparo de Dados](../../../../../data-prep/ui/mapping.md) para obter mais informações.

![A interface de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/stripe/mapping.png)

## Configurar programação de assimilação {#scheduling}

Em seguida, use a interface de programação para criar uma programação de assimilação para o fluxo de dados.

Selecione a lista suspensa de frequência para configurar a frequência de assimilação do fluxo de dados.

![O menu suspenso de frequência.](../../../../images/tutorials/create/stripe/frequency.png)

Você também pode selecionar o ícone de calendário e usar um calendário pop-up para configurar a hora de início da assimilação.

![O calendário configurável para agendamento.](../../../../images/tutorials/create/stripe/calendar.png)

| Configuração de agendamento | Descrição |
| --- | --- |
| Frequência | Configure a frequência para indicar a frequência de execução do fluxo de dados. Você pode definir a frequência como: <ul><li>**Uma vez**: defina sua frequência como `once` para criar uma assimilação única. As configurações para intervalo e preenchimento retroativo não estão disponíveis ao criar um fluxo de dados de assimilação única. Por padrão, a frequência de agendamento é definida como uma vez.</li><li>**Minuto**: Defina sua frequência como `minute` para agendar seu fluxo de dados para assimilar dados por minuto.</li><li>**Hora**: Defina sua frequência como `hour` para agendar seu fluxo de dados para assimilar dados por hora.</li><li>**Dia**: Defina sua frequência como `day` para agendar seu fluxo de dados para assimilar dados por dia.</li><li>**Semana**: Defina sua frequência como `week` para agendar seu fluxo de dados para assimilar dados por semana.</li></ul> |
| Intervalo | Depois de selecionar uma frequência, você pode definir o intervalo para estabelecer o intervalo de tempo entre cada assimilação. Por exemplo, se você definir a frequência como dia e configurar o intervalo como 15, o fluxo de dados será executado a cada 15 dias. Você não pode definir o intervalo como zero. O valor mínimo de intervalo aceito para cada frequência é o seguinte:<ul><li>**Uma vez**: n/d</li><li>**Minuto**: 15</li><li>**Hora**: 1</li><li>**Dia**: 1</li><li>**Semana**: 1</li></ul> |
| Hora de início | O carimbo de data e hora da execução projetada, apresentado no fuso horário UTC. |
| Preenchimento retroativo | O preenchimento retroativo determina quais dados são assimilados inicialmente. Se o preenchimento retroativo estiver ativado, todos os arquivos atuais no caminho especificado serão assimilados durante a primeira assimilação agendada. Se o preenchimento retroativo estiver desativado, somente os arquivos carregados entre a primeira execução da assimilação e a hora de início serão assimilados. Os arquivos carregados antes da hora de início não serão assimilados. |

Depois de configurar o agendamento de assimilação do fluxo de dados, selecione **[!UICONTROL Avançar]**.

![A interface de agendamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/stripe/scheduling.png)

## Revisar seu fluxo de dados

A etapa final no processo de criação do fluxo de dados é revisar o fluxo de dados antes de executá-lo. Use a etapa **[!UICONTROL Revisão]** para revisar os detalhes do novo fluxo de dados antes de ele ser executado. Os detalhes estão agrupados nas seguintes categorias:

* **Conexão**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas nesse arquivo de origem.
* **Atribuir campos de conjunto de dados e mapa**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.
* **Agendamento**: mostra o período, a frequência e o intervalo ativos do agendamento de assimilação.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa Revisão do fluxo de trabalho de origens.](../../../../images/tutorials/create/stripe/review.png)

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de dados para trazer dados de pagamentos da sua origem [!DNL Stripe] para a Experience Platform. Para obter recursos adicionais, consulte a documentação descrita abaixo.

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para exibir informações sobre taxas de assimilação, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, visite o tutorial em [monitoramento de contas e fluxos de dados na interface](../../../../../dataflows/ui/monitor-sources.md).

### Atualizar seu fluxo de dados

Para atualizar as configurações do agendamento de fluxos de dados, mapeamento e informações gerais, visite o tutorial em [atualizando fluxos de dados de fontes na interface](../../update-dataflows.md).

### Excluir seu fluxo de dados

Você pode excluir fluxos de dados que não são mais necessários ou que foram criados incorretamente usando a função **[!UICONTROL Excluir]** disponível no espaço de trabalho **[!UICONTROL Fluxos de Dados]**. Para obter mais informações sobre como excluir fluxos de dados, visite o tutorial em [excluindo fluxos de dados na interface](../../delete.md).
