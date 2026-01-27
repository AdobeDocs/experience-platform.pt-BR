---
title: Conectar sua conta do Salesforce Marketing Cloud (V2) à Experience Platform por meio da interface
description: Saiba como conectar sua conta do Salesforce Marketing Cloud (V2) ao Experience Platform por meio da interface do usuário do.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# Conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform

Leia este guia para saber como conectar sua conta do [!DNL Salesforce Marketing Cloud] à Adobe Experience Platform usando o espaço de trabalho de fontes na interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Leia a [[!DNL Salesforce Marketing Cloud] visão geral](../../../../connectors/marketing-automation/sfmc.md#prerequisites) para obter informações sobre autenticação.

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Sources]*. Escolha uma categoria ou use a barra de pesquisa para localizar sua fonte.

Para se conectar a [!DNL Salesforce Marketing Cloud], vá para a categoria *[!UICONTROL Marketing Automation]*, selecione o cartão de origem **[!UICONTROL (V2) Salesforce Marketing Cloud]** e selecione **[!UICONTROL Set up]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Set up]** quando uma determinada origem ainda não tem uma conta autenticada. Depois que uma conta autenticada é criada, esta opção muda para **[!UICONTROL Add data]**.

![O catálogo de origens com a origem do Salesforce Marketing Cloud selecionada.](../../../../images/tutorials/create/sfmc/catalog.png)

## Usar uma conta existente {#existing}

Para usar uma conta existente, selecione **[!UICONTROL Existing account]** e depois selecione a conta [!DNL Salesforce Marketing Cloud] que deseja usar.

![A interface de conta existente do fluxo de trabalho de origem](../../../../images/tutorials/create/sfmc/existing.png)

## Criar uma nova conta {#new}

Para criar uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome e uma descrição em seu [!UICONTROL Source connection details]. Em seguida, em [!UICONTROL Account authentication], forneça valores para sua **ID do Cliente**, **Segredo do Cliente** e **Ponto de extremidade Base**. Você pode ler o [guia de autenticação](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials) para obter mais informações sobre essas credenciais. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde alguns segundos para estabelecer sua conexão.

![A nova interface de conta do fluxo de trabalho de origens.](../../../../images/tutorials/create/sfmc/new.png)

## Selecionar dados

A fonte [!DNL Salesforce Marketing Cloud] oferece suporte à assimilação de dados somente de [!DNL Salesforce Marketing Cloud] extensões de dados.

Use a interface [!UICONTROL Select data] para selecionar a extensão de dados que você deseja assimilar da instância [!DNL Salesforce Marketing Cloud]. Depois de selecionar a extensão de dados, você pode usar o painel de visualização para confirmar se o conjunto de dados contém os campos esperados antes de continuar.

![A etapa de seleção de dados do fluxo de trabalho de fontes](../../../../images/tutorials/create/sfmc/select-data.png)

## Detalhes do conjunto de dados e do fluxo de dados

Em seguida, você deve fornecer informações sobre o conjunto de dados e o fluxo de dados. Durante essa etapa, é possível usar um conjunto de dados existente ou criar um novo. Além disso, você pode, opcionalmente, ativar seu conjunto de dados para assimilação no Perfil do cliente em tempo real durante essa etapa.

![A etapa de detalhes do conjunto de dados e do fluxo de dados do fluxo de trabalho de fontes.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## Mapeamento

Em [!DNL Salesforce Marketing Cloud], as extensões de dados não são consideradas como objetos padrão. Portanto, não há campos de mapeamento predefinidos ou fixos para um esquema do Experience Platform. Embora o Preparo de dados no Experience Platform execute um alinhamento de melhor esforço entre os campos de origem do [!DNL Salesforce Marketing Cloud] e o esquema do Experience Data Model (XDM) de destino, ainda pode haver alguns casos em que uma revisão ou ajuste manual seja necessário para resolver campos não mapeados ou errôneos.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/sfmc/mapping.png)

## Programar um fluxo de dados

Com o mapeamento concluído, agora é possível configurar um agendamento de assimilação para o fluxo de dados. Defina seu [!UICONTROL Frequency] como `Once` para configurar uma execução de assimilação única. Para assimilação incremental, você pode definir seu [!UICONTROL Frequency] como `Hour`, `Day` ou `Week`. Ao usar a assimilação incremental, você também deve configurar o [!UICONTROL Interval] para definir a quantidade de tempo que ocorre entre as execuções de assimilação. Por exemplo, uma frequência de assimilação definida como `Day` e um intervalo definido como `15` significa que o fluxo de dados está agendado para assimilar dados a cada 15 dias.

>[!TIP]
>
> A frequência de assimilação por minuto não está disponível para a origem [!DNL Salesforce Marketing Cloud]. A programação mais frequente que você pode escolher é por hora. Selecione um agendamento que corresponda às suas necessidades de atualização de dados. Lembre-se de que a seleção de uma programação mais frequente aumentará os custos de computação.

Você deve selecionar um campo delta (data/hora) no conjunto de dados para habilitar a sincronização incremental. Se o conjunto de dados não contiver um campo delta adequado, você não poderá criar o fluxo de dados.

![A etapa de agendamento do fluxo de trabalho de fontes.](../../../../images/tutorials/create/sfmc/schedule.png)

## Revisar

Com o agendamento de assimilação configurado, use a interface [!UICONTROL Review] para confirmar os detalhes do fluxo de dados. Selecione **[!UICONTROL Finish]** para concluir a configuração e aguarde alguns minutos para que seu fluxo de dados seja iniciado.

![A etapa de revisão do fluxo de trabalho de fontes.](../../../../images/tutorials/create/sfmc/review.png)

## Monitorar

Depois que o fluxo de dados for selecionado, ele fará um preenchimento retroativo de dados único e a sincronização incremental subsequente no agendamento especificado. O status da sincronização pode ser monitorado navegando até o fluxo de dados. Para obter mais informações, leia o guia sobre [fluxos de dados de fontes de monitoramento na interface](../../../../../dataflows/ui/monitor-sources.md).

## Próximas etapas

Este tutorial guiou você pela conexão da conta do [!DNL Salesforce Marketing Cloud] (V2) com a Experience Platform usando a interface do usuário. Você aprendeu a selecionar ou criar uma conta de origem, fornecer as credenciais necessárias, escolher as extensões de dados para assimilar, especificar os detalhes do conjunto de dados e do fluxo de dados, mapear seus dados, configurar uma programação para assimilação de dados e monitorar seus fluxos de dados. Ao seguir essas etapas, você integrou com êxito os dados do [!DNL Salesforce Marketing Cloud] com o Experience Platform para ativação e análise.

Para obter informações adicionais, leia a seguinte documentação:

* [Visão geral das fontes](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

