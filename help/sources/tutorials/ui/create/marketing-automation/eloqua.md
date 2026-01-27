---
title: Conexão do Oracle Eloqua (V2) ao Experience Platform na interface do
description: Saiba como conectar sua conta do Oracle Eloqua ao Experience Platform na interface do usuário do.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# Conectar o [!DNL Oracle Eloqua] (V2) ao Experience Platform na interface

O conector de origem do [!DNL Oracle Eloqua (V2)] permite conectar sua conta do Oracle Eloqua com o Adobe Experience Platform, permitindo a assimilação automatizada e escalonável dos principais dados de marketing B2B, incluindo contatos, contas, campanhas e atividades de envolvimento.

Use esse conector de origem para configurar a autenticação segura, selecione as entidades de dados Eloqua exatas necessárias e mapeie-as para esquemas padronizados do Experience Data Model (XDM). Opções de agendamento flexíveis permitem configurar carregamentos de dados iniciais e sincronizações recorrentes e incrementais, garantindo que seus dados de marketing permaneçam atualizados e acionáveis.

Criado com base na estrutura de assimilação corporativa da Adobe, o conector de origem do [!DNL Oracle Eloqua (V2)] fornece uma base confiável e extensível para otimização de campanha, medição de desempenho e personalização entre canais.

Leia este guia para saber como conectar sua conta do [!DNL Oracle Eloqua] à Adobe Experience Platform usando o espaço de trabalho de fontes na interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias {#credentials}

Leia a [[!DNL Eloqua] visão geral](../../../../connectors/marketing-automation/eloqua.md) para obter informações sobre autenticação.

## Navegar pelo catálogo de origens {#catalog}

Na interface do Experience Platform, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Sources]*. Escolha uma categoria ou use a barra de pesquisa para localizar sua fonte.

Para se conectar a [!DNL Eloqua], vá para a categoria *[!UICONTROL Marketing Automation]*, selecione o cartão de origem **[!UICONTROL (V2) Oracle Eloqua]** e selecione **[!UICONTROL Set up]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Set up]** quando uma determinada origem ainda não tem uma conta autenticada. Depois que uma conta autenticada é criada, esta opção muda para **[!UICONTROL Add data]**.

![O cartão de origem Eloqua no catálogo de origens com o botão Configurar realçado.](../../../../images/tutorials/create/eloqua/catalog.png)

## Usar uma conta existente {#existing}

Para usar uma conta existente, selecione **[!UICONTROL Existing account]** e depois selecione a conta [!DNL Eloqua] que deseja usar.

![A opção Conta existente selecionada na interface de criação de conta.](../../../../images/tutorials/create/eloqua/existing.png)

## Criar uma nova conta {#new}

Para criar uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome e uma descrição em seu [!UICONTROL Source connection details]. Em seguida, em [!UICONTROL Account authentication], forneça valores para sua **ID do Cliente**, **Segredo do cliente**, **Nome de Usuário**, **Senha** e **Ponto de extremidade base**. Você pode ler o [guia de autenticação](../../../../connectors/marketing-automation/eloqua.md) para obter mais informações sobre essas credenciais. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde alguns segundos para estabelecer sua conexão.

![A Nova interface de conta com campos para detalhes de conexão de origem e credenciais de autenticação.](../../../../images/tutorials/create/eloqua/new.png)

## Selecionar dados

Use a interface de dados selecionada para selecionar a entidade [!DNL Eloqua] que deseja assimilar na Experience Platform.

>[!TIP]
>
>Ao selecionar dados, você observará que, exceto para campanhas, as outras entidades exibem dados representativos de amostra. Essa abordagem garante que você possa visualizar os campos e a estrutura disponíveis, já que [!DNL Eloqua] APIs públicas atualmente recuperam dados reais apenas para campanhas. Para as entidades restantes, dados de amostra são fornecidos para dar suporte ao fluxo de trabalho de configuração.

![A interface de seleção de dados mostrando entidades de dados Eloqua disponíveis.](../../../../images/tutorials/create/eloqua/select-data.png)

## Detalhes do conjunto de dados e do fluxo de dados {#details}

Em seguida, você deve fornecer informações sobre o conjunto de dados e o fluxo de dados. Durante essa etapa, é possível usar um conjunto de dados existente ou criar um novo. Além disso, você pode, opcionalmente, ativar seu conjunto de dados para assimilação no Perfil do cliente em tempo real durante essa etapa.

![Os detalhes do conjunto de dados e do fluxo de dados fazem interface com opções para configurar as propriedades do conjunto de dados.](../../../../images/tutorials/create/eloqua/details.png)

## Mapeamento {#mapping}

Os mapeamentos para [!DNL Eloqua] são organizados em quatro tipos de entidade principais:

* **Contas** - Registros de empresa/organização de [!DNL Eloqua].
* **Atividades** - Atividade de marketing e eventos de participação de [!DNL Eloqua].
* **Campanhas** - Registros de campanha de marketing de [!DNL Eloqua].
* **Contatos** - Registros de pessoa individual de [!DNL Eloqua].

Se você precisar de acesso a campos extras além daqueles fornecidos por padrão, poderá adicionar esses campos usando o processo de mapeamento Preparo de dados no Experience Platform. Se o esquema padrão não suportar alguns dos campos obrigatórios, você terá a opção de definir um esquema personalizado no Experience Platform. Use este recurso para criar e mapear os campos necessários para assimilar facilmente todos os dados relevantes do [!DNL Eloqua] na Experience Platform.

Resumo das próximas etapas:

* Revise os campos mapeados padrão disponíveis com a integração.
* Durante a etapa de mapeamento, inclua os campos adicionais necessários de [!DNL Eloqua].
* Se novos campos não estiverem presentes no esquema padrão, estenda ou crie um esquema personalizado no Experience Platform que inclua esses campos.
* Conclua o mapeamento para garantir que todos os dados desejados sejam assimilados.

Para garantir que as informações externas do CRM sejam refletidas com precisão, use a função de campo calculado em Preparo de dados para atualizar o espaço reservado `{CRM_INSTANCE_ID}` com a ID de instância do CRM específica no campo de dados de origem. Isso oferece a flexibilidade de adaptar a integração à configuração exclusiva de sua organização.

Para usar o editor de campo calculado, selecione o campo de origem que deseja atualizar.

![O campo de origem Eloqua com campos calculados.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

Para [!DNL Salesforce] usuários, use o editor de campo calculado e atualize o `{CRM_INSTANCE_ID}` com a ID de instância apropriada.

![O campo calculado para o Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

Para [!DNL Microsoft] usuários, use o editor de campo calculado e atualize o `{CRM_INSTANCE_ID}` com a ID de instância apropriada.

![O campo calculado para o Dynamics.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

Depois de terminar de atualizar os campos calculados, selecione **[!UICONTROL Next]** para continuar.

![A interface de mapeamento que mostra mapeamentos de campo para entidades de dados Eloqua.](../../../../images/tutorials/create/eloqua/mapping.png)

## Agendamento

>[!NOTE]
>
>A seguir estão os campos delta usados internamente para carregamento de dados incrementais:
>
>* **Contatos:** `C_DateModified`
>* **Contas:** `M_DateModified`
>* **Atividade:** `CreatedAt`
>* **Objetos Personalizados:** `UpdatedAt`
>* **Campanha:** `updatedAt`

Com o mapeamento concluído, agora é possível configurar um agendamento de assimilação para o fluxo de dados. Defina seu [!UICONTROL Frequency] como `Once` para configurar uma execução de assimilação única. Para assimilação incremental, você pode definir seu [!UICONTROL Frequency] como `Hour`, `Day` ou `Week`. Ao usar a assimilação incremental, você também deve configurar o [!UICONTROL Interval] para definir a quantidade de tempo que ocorre entre as execuções de assimilação. Por exemplo, uma frequência de assimilação definida como `Day` e um intervalo definido como `15` significa que o fluxo de dados está agendado para assimilar dados a cada 15 dias.

A frequência de assimilação por minuto não está disponível para a origem [!DNL Eloqua]. A programação mais frequente que você pode escolher é por hora. Selecione um agendamento que corresponda às suas necessidades de atualização de dados. Lembre-se de que a seleção de uma programação mais frequente aumentará os custos de computação.

![A interface de agendamento com opções para configurar a frequência e o intervalo de assimilação.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Revisar

Com o agendamento de assimilação configurado, use a interface [!UICONTROL Review] para confirmar os detalhes do fluxo de dados. Selecione **[!UICONTROL Finish]** para concluir a configuração e aguarde alguns minutos para que seu fluxo de dados seja iniciado.

![A interface de revisão exibindo um resumo da configuração do fluxo de dados antes da conclusão.](../../../../images/tutorials/create/eloqua/review.png)

## Monitorar

Depois que o fluxo de dados for selecionado, ele fará um preenchimento retroativo de dados único e a sincronização incremental subsequente no agendamento especificado. O status da sincronização pode ser monitorado navegando até o fluxo de dados. Para obter mais informações, leia o guia sobre [fluxos de dados de fontes de monitoramento na interface](../../../../../dataflows/ui/monitor-sources.md).

## Próximas etapas

Agora você concluiu a instalação e a configuração da origem do [!DNL Eloqua] no Experience Platform. Com o fluxo de dados estabelecido, os dados do [!DNL Eloqua] serão assimilados de acordo com o agendamento escolhido e mapeados para esquemas padrão do Experience Data Model (XDM). Continue monitorando seus fluxos de dados e explore seus dados assimilados na Platform para gerar insights e ativar seus casos de uso de marketing. Para obter configurações e soluções de problemas mais avançadas, consulte a documentação relacionada ou entre em contato com os recursos de suporte da Adobe.

Para obter informações adicionais, leia a seguinte documentação:

* [Visão geral das fontes](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
