---
title: Transmitir dados do banco de dados do Snowflake para o Experience Platform usando a interface do
type: Tutorial
description: Saiba como transmitir dados do banco de dados do Snwoflake para o Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 3%

---

# Transmita dados de seu [!DNL Snowflake] banco de dados para Experience Platform usando a interface

Saiba como usar a interface do usuário do para transmitir dados de seu [!DNL Snowflake] banco de dados à Adobe Experience Platform seguindo este guia.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Autenticação

Leia o guia em [pré-requisito de configuração para [!DNL Snowflake] transmissão de dados](../../../../connectors/databases/snowflake-streaming.md) para obter informações sobre as etapas que devem ser concluídas antes de assimilar dados de transmissão do [!DNL Snowflake] para Experience Platform.

## Use o [!DNL Snowflake Streaming] origem para fluxo [!DNL Snowflake] dados para Experience Platform

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *Bancos de dados* categoria, selecione **[!DNL Snowflake Streaming]** e selecione **[!UICONTROL Adicionar dados]**.

>[!TIP]
>
>As origens que não têm uma conta autenticada no catálogo de origens exibem a **[!UICONTROL Configurar]** opção. Quando uma conta autenticada existir, essa opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do usuário do Experience Platform, com o cartão de origem de transmissão Snowflake selecionado.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

A variável **[!UICONTROL Conectar a conta de transmissão Snowflake]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

>[!BEGINTABS]

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A interface de criação de nova conta do workflow de origens.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Credencial | Descrição |
| --- | --- |
| Conta | O nome do seu [!DNL Snowflake] conta. |
| Warehouse | O nome do seu [!DNL Snowflake] depósito. Os depósitos gerenciam a execução de consultas no [!DNL Snowflake]. Each [!DNL Snowflake] o warehouse é independente um do outro e deve ser acessado individualmente para trazer os dados para o Experience Platform. |
| Banco de dados | O nome do seu [!DNL Snowflake] banco de dados. O banco de dados contém os dados que você deseja trazer para o Experience Platform. |
| Esquema | (Opcional) O esquema de banco de dados associado à [!DNL Snowflake] conta. |
| Nome de usuário | O nome de usuário do seu [!DNL Snowflake] conta. |
| Senha | A senha para o seu [!DNL Snowflake] conta. |
| Função | (Opcional) Uma função definida personalizada que pode ser fornecida a um usuário para uma determinada conexão. Se não for fornecido, esse valor assumirá como padrão `public`. |

Para obter mais informações sobre a criação de contas, leia a seção sobre [definindo configurações de função](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) no [!DNL Snowflake Streaming] visão geral.

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e selecione a conta desejada no catálogo de contas existente.

Selecione **[!UICONTROL Próximo]** para continuar.

![A página de seleção de conta existente do catálogo de códigos-fonte.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Selecionar dados {#select-data}

>[!IMPORTANT]
>
>Uma coluna de carimbo de data e hora deve existir na tabela de origem para que um fluxo de dados de transmissão seja criado. O carimbo de data e hora é necessário para que o Experience Platform saiba quando os dados serão assimilados e quando os dados incrementais serão transmitidos. Você pode adicionar retroativamente uma coluna de carimbo de data e hora para uma conexão existente e criar um novo fluxo de dados.

A variável [!UICONTROL Selecionar dados] é exibida. Nesta etapa, você deve selecionar os dados que deseja importar para o Experience Platform, configurar carimbos de data e hora e fusos horários e fornecer um arquivo de dados de origem de amostra para a assimilação de dados brutos.

Use o diretório do banco de dados à esquerda da tela e selecione a tabela que deseja importar para o Experience Platform.

![A interface de dados selecionada com uma tabela de banco de dados selecionada.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

Em seguida, selecione o tipo de coluna de carimbo de data e hora da tabela. Você pode selecionar entre dois tipos de colunas de carimbo de data e hora: `TIMESTAMP_NTZ` ou  `TIMESTAMP_LTZ`. Se você selecionar um tipo de coluna de `TIMESTAMP_NTZ`, você também deve fornecer um fuso horário. Suas colunas devem ter uma restrição não nula. Para obter mais informações, leia a seção sobre [limitações e perguntas frequentes]

Você também pode definir configurações de preenchimento retroativo durante essa etapa. O preenchimento retroativo determina quais dados são assimilados inicialmente. Se o preenchimento retroativo estiver ativado, todos os arquivos atuais no caminho especificado serão assimilados durante a primeira assimilação agendada. Caso contrário, então somente os arquivos carregados entre a primeira execução da assimilação e a hora de início serão assimilados. Os arquivos carregados antes da hora de início não serão assimilados.

Selecione o **[!UICONTROL Preenchimento retroativo]** ativar o preenchimento retroativo.

![As etapas de configuração de carimbo de data e hora, fuso horário e preenchimento retroativo.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Finalmente, selecione **[!UICONTROL Escolher arquivo]** fazer upload de dados de origem de amostra para ajudar a criar o conjunto de mapeamento, que será usado em uma etapa posterior para mapear seus dados originais para o Experience Data Model (XDM).

Quando terminar, selecione **[!UICONTROL Próxima]** para continuar.

![A visualização dos dados de amostra de origem.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Fornecer detalhes do conjunto de dados e do fluxo de dados {#provide-dataset-and-dataflow-details}

Em seguida, você deve fornecer informações sobre seu conjunto de dados e seu fluxo de dados.

### Detalhes do conjunto de dados {#dataset-details}

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os dados assimilados com sucesso no Experience Platform são mantidos no data lake como conjuntos de dados. Durante essa etapa, você pode criar um novo conjunto de dados ou usar um conjunto de dados existente.

>[!BEGINTABS]

>[!TAB Usar um novo conjunto de dados]

Para usar um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]**, em seguida, forneça um nome e uma descrição opcional para seu conjunto de dados. Você também deve selecionar um esquema do Experience Data Model (XDM) ao qual seu conjunto de dados adere.

![A nova interface de seleção do conjunto de dados.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Detalhes do novo conjunto de dados | Descrição |
| --- | --- |
| Nome do conjunto de dados de saída | O nome do novo conjunto de dados. |
| Descrição | (Opcional) Uma breve visão geral do novo conjunto de dados. |
| Esquema | Uma lista suspensa de esquemas que existem em sua organização. Você também pode criar seu próprio esquema antes do processo de configuração de origem. Para obter mais informações, leia o guia em [criação de um esquema XDM na interface do usuário](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Usar um conjunto de dados existente]

Se você já tiver um conjunto de dados, selecione **[!UICONTROL Conjunto de dados existente]** e, em seguida, use o **[!UICONTROL Pesquisa avançada]** opção para exibir uma janela de todos os conjuntos de dados em sua organização, incluindo seus respectivos detalhes, como se eles estão habilitados para assimilação no Perfil do cliente em tempo real.

![A interface de seleção do conjunto de dados existente.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++Selecione para obter as etapas para habilitar a Assimilação de perfil, o diagnóstico de erros e a assimilação parcial.

Se o conjunto de dados estiver ativado para o Perfil de cliente em tempo real, durante essa etapa é possível alternar **[!UICONTROL Conjunto de dados Perfil]** para ativar seus dados para assimilação de perfis. Você também pode usar esta etapa para habilitar **[!UICONTROL Diagnóstico de erro]** e **[!UICONTROL Assimilação parcial]**.

* **[!UICONTROL Diagnóstico de erro]**: Selecionar **[!UICONTROL Diagnóstico de erro]** para instruir a origem a produzir diagnósticos de erro que você poderá consultar posteriormente ao monitorar a atividade do conjunto de dados e o status do fluxo de dados.
* **[!UICONTROL Assimilação parcial]**: a assimilação parcial de lotes é a capacidade de assimilar dados que contêm erros, até um determinado limite configurável. Esse recurso permite assimilar com sucesso todos os seus dados precisos no Experience Platform, enquanto todos os seus dados incorretos são armazenados em lote separadamente com informações sobre por que são inválidos.

+++

### Detalhes do fluxo de dados {#dataflow-details}

Depois que o conjunto de dados é configurado, você deve fornecer detalhes sobre o fluxo de dados, incluindo um nome, uma descrição opcional e configurações de alerta.

![A etapa de configuração de detalhes do fluxo de dados.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Configurações de fluxo de dados | Descrição |
| --- | --- |
| Nome do fluxo de dados | O nome do fluxo de dados.  Por padrão, esse campo usará o nome do arquivo que está sendo importado. |
| Descrição | (Opcional) Uma breve descrição do fluxo de dados. |
| Alertas | O Experience Platform pode produzir alertas baseados em eventos que os usuários podem assinar. Essas opções exigem um fluxo de dados em execução para serem acionadas. Para obter mais informações, leia a [visão geral dos alertas](../../alerts.md) <ul><li>**Início da execução do fluxo de dados de fontes**: selecione esse alerta para receber uma notificação quando a execução do fluxo de dados começar.</li><li>**Êxito na execução do fluxo de dados de fontes**: selecione esse alerta para receber uma notificação se o fluxo de dados terminar sem erros.</li><li>**Falha na execução do fluxo de dados de fontes**: selecione esse alerta para receber uma notificação se a execução do fluxo de dados terminar com erros.</li></ul> |

Quando terminar, selecione **[!UICONTROL Próxima]** para continuar.

## Mapear campos para um esquema XDM {#mapping}

A variável [!UICONTROL Mapeamento] é exibida. Use a interface de mapeamento para mapear os dados de origem para os campos de esquema apropriados antes de assimilar esses dados no Experience Platform e selecione **[!UICONTROL Próxima]**. Para obter um guia extenso sobre como usar a interface de mapeamento, leia o [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md) para obter mais informações.

![A interface de mapeamento do workflow de origens.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Revisar seu fluxo de dados {#review}

A etapa final no processo de criação do fluxo de dados é revisar o fluxo de dados antes de executá-lo. Use o **[!UICONTROL Revisão]** etapa para revisar os detalhes do novo fluxo de dados antes de ele ser executado. Os detalhes estão agrupados nas seguintes categorias:

* **Conexão**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas nesse arquivo de origem.
* **Atribuir conjunto de dados e mapear campos**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

![A etapa Revisar do fluxo de trabalho de origens.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados de transmissão para [!DNL Snowflake] dados. Para obter recursos adicionais, leia a documentação abaixo.

### Monitorar seu fluxo de dados

Depois que o fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por meio dele para exibir informações sobre taxas de assimilação, sucesso e erros. Para obter mais informações sobre como monitorar a transmissão de dados, consulte o tutorial em [monitoramento de fluxos de dados de transmissão na interface do](../../monitor-streaming.md).

### Atualizar seu fluxo de dados

Para atualizar as configurações para o agendamento de fluxos de dados, mapeamento e informações gerais, visite o tutorial em [atualização de fluxos de dados de fontes na interface do usuário](../../update-dataflows.md).

### Excluir seu fluxo de dados

É possível excluir fluxos de dados que não são mais necessários ou que foram criados incorretamente usando o **[!UICONTROL Excluir]** disponível na **[!UICONTROL Fluxos de dados]** espaço de trabalho. Para obter mais informações sobre como excluir fluxos de dados, consulte o tutorial em [exclusão de fluxos de dados na interface](../../delete.md).