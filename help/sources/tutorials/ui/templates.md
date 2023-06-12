---
description: Saiba como usar modelos na interface do usuário do Adobe Experience Platform para acelerar seu processo de assimilação de dados para dados B2B.
title: Criar um fluxo de dados de fontes usando modelos na interface
badge1: "Beta"
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: deca8300ebbada548a409de9c6a7b7178d0032e0
workflow-type: tm+mt
source-wordcount: '2258'
ht-degree: 10%

---

# Criar um fluxo de dados de fontes usando modelos na interface {#create-a-sources-dataflow-using-templates-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_marketo_mapping"
>title="Modelos para fontes na interface da Platform"
>abstract="Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, identidades, regras de mapeamento, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma fonte para a Experience Platform. É possível atualizar ativos gerados automaticamente para personalização de acordo com seus casos de uso."

>[!IMPORTANT]
>
>Os modelos estão na versão beta e são compatíveis com as seguintes fontes:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>A documentação e as funcionalidades estão sujeitas a alterações.

A Adobe Experience Platform fornece modelos pré-configurados que você pode usar para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, identidades, regras de mapeamento, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma fonte para a Experience Platform.

Com os modelos, é possível:

* Reduza o tempo de implantação da assimilação por meio da aceleração da criação de ativos modelados.
* Minimize os erros que podem ocorrer durante o processo manual de assimilação de dados.
* Atualize ativos gerados automaticamente em qualquer ponto para atender aos seus casos de uso.

O tutorial a seguir fornece etapas sobre como usar modelos na interface do usuário da Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Origens](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Sandboxes](../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Usar modelos na interface do Platform {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Selecionar tipo de empresa"
>abstract="Selecione o tipo de empresa apropriado para seu caso de uso. O acesso pode variar dependendo da conta de assinatura da Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=pt-BR" text="Visão geral da Real-Time CDP"

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] e veja um catálogo de fontes disponíveis no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica do catálogo.

Vá para a [!UICONTROL aplicativos Adobe] categoria para ver o [!DNL Marketo Engage] e, em seguida, selecione [!UICONTROL Adicionar dados] para começar.

![Um catálogo do espaço de trabalho de origens com a origem de Marketo Engage realçada.](../../images/tutorials/templates/catalog.png)

Uma janela pop-up é exibida, apresentando a opção de procurar modelos ou usar esquemas e conjuntos de dados existentes.

* **Procurar modelos**: os modelos de origens criam esquemas, identidades, conjuntos de dados e fluxos de dados automaticamente com regras de mapeamento para você. Você pode personalizar esses ativos conforme necessário.
* **Usar meus ativos existentes**: assimile seus dados usando conjuntos de dados e esquemas existentes que você criou. Você também pode criar novos conjuntos de dados e esquemas, se necessário.

Para usar ativos gerados automaticamente, selecione **[!UICONTROL Procurar modelos]** e selecione **[!UICONTROL Selecionar]**.

![Uma janela pop-up com opções para procurar modelos ou usar ativos existentes.](../../images/tutorials/templates/browse-templates.png)

### Autenticação

A etapa de autenticação é exibida, solicitando que você crie uma nova conta ou use uma conta existente.

>[!BEGINTABS]

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione [!UICONTROL Conta existente] e, em seguida, selecione a conta que deseja usar na lista exibida.

![A página de seleção de uma conta existente com uma lista de contas existentes que você pode acessar.](../../images/tutorials/templates/existing-account.png)

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça os detalhes da conexão de origem e as credenciais de autenticação da conta. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e espere algum tempo para que a nova conexão seja estabelecida.

![A página de autenticação de uma nova conta com detalhes da conexão de origem e credenciais de autenticação da conta.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Selecionar modelos

Com sua conta autenticada, agora é possível selecionar o modelo que deseja usar para o fluxo de dados.

+++[!DNL Marketo Engage] modelos A tabela a seguir descreve os modelos disponíveis para a [!DNL Marketo Engage] origem.

| [!DNL Marketo Engage] modelos | Descrição |
| --- | --- |
| Atividades | O modelo de Atividades captura instantâneos baseados em eventos de atividades, como interações por email, interações de site e chamadas de vendas. |
| Empresas | O modelo Empresas captura detalhes da conta comercial, como informações firmográficas, localização e informações de faturamento da empresa. |
| Contas Nomeadas | O modelo Contas Nomeadas captura detalhes de contas que foram determinadas como contas de destino a serem seguidas. |
| Oportunidades | O modelo de Oportunidades captura detalhes da oportunidade comercial, como tipo, estágio de vendas e contas relacionadas. |
| Funções do contato da oportunidade | O modelo Funções de contato da oportunidade captura detalhes sobre as funções para clientes potenciais associadas a uma oportunidade específica. |
| Pessoas | O modelo Pessoas captura atributos de pessoas individuais, como detalhes demográficos, informações de contato e preferências de consentimento. |
| Associações ao programa | O modelo de Associações de programa captura detalhes para contatos associados a uma campanha comercial, incluindo cadências de criação e respostas de contato. |
| Programas | O modelo Programas captura detalhes da campanha comercial como status, canais, linhas do tempo e custos. |
| Associações de Lista Estáticas | O modelo Associações de lista estática captura as relações entre as pessoas e suas associações em listas estáticas. |
| Listas Estáticas | O modelo Lista estática captura listas instanciadas de pessoas para casos de uso específicos. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] Modelos B2B A tabela a seguir descreve os modelos B2B disponíveis para o [!DNL Salesforce] origem.

| [!DNL Salesforce] Modelos B2B | Descrição |
| --- | --- |
| Relação de contato da conta | O modelo de Relação de Contato de Conta captura a relação entre um contato e uma ou mais contas. |
| Contas | O modelo de Conta captura detalhes da conta comercial, como informações firmográficas, locais e informações de faturamento da empresa. |
| Membros da campanha | O modelo Membros da campanha captura a relação entre um lead ou contato individual e um perfil [!DNL Salesforce] campanha. |
| Campanhas | O modelo Campanhas captura detalhes da conta de negócios, como informações firmográficas, localização e informações de faturamento da empresa. |
| Contatos | O modelo Contato captura atributos para contatos, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |
| Clientes potenciais | O modelo de Clientes potenciais captura atributos para clientes potenciais, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |
| Oportunidades | O modelo de Oportunidades captura detalhes da oportunidade comercial, como tipo, estágio de vendas e conta relacionada. |
| Funções do contato da oportunidade | O modelo Funções de contato da oportunidade captura detalhes sobre as funções para clientes potenciais associadas a uma oportunidade específica. |

{style="table-layout:auto"}

+++

+++[!DNL Salesforce] Modelos B2C A tabela a seguir descreve os modelos B2C disponíveis para o [!DNL Salesforce] origem.

| [!DNL Salesforce] Modelos B2C | Descrição |
| --- | --- |
| Contato | O modelo Contato captura atributos para contatos, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |
| Cliente potencial | O modelo de cliente potencial captura atributos para clientes potenciais, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] Modelos B2B A tabela a seguir descreve os modelos B2B disponíveis para o [!DNL Microsoft Dynamics] origem.

| [!DNL Microsoft Dynamics] Modelos B2B | Descrição |
| --- | --- |
| Contas | O modelo de Conta captura detalhes da conta comercial, como informações firmográficas, locais e informações de faturamento da empresa. |
| Campanhas | O modelo Campanhas captura detalhes da conta de negócios, como informações firmográficas, localização e informações de faturamento da empresa. |
| Contatos | O modelo Contato captura atributos para contatos, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |
| Clientes potenciais | O modelo de Clientes potenciais captura atributos para clientes potenciais, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |
| Lista de marketing | O modelo de Lista de marketing captura um grupo de clientes existentes ou em potencial criado para uma campanha de marketing ou outros fins de vendas. |
| Membros da lista de marketing | Os Membros da Lista de marketing capturam os detalhes de qualquer tipo de registro de cliente, como clientes potenciais, contas ou contatos, em uma lista de marketing. |
| Oportunidades | O modelo de Oportunidades captura detalhes da oportunidade comercial, como tipo, estágio de vendas e conta relacionada. |
| Funções do contato da oportunidade | O modelo Funções de contato da oportunidade captura detalhes sobre as funções para clientes potenciais associadas a uma oportunidade específica. |

{style="table-layout:auto"}

+++

+++[!DNL Microsoft Dynamics] Modelos B2C A tabela a seguir descreve os modelos B2C disponíveis para o [!DNL Microsoft Dynamics] origem.

| [!DNL Microsoft Dynamics] Modelos B2C | Descrição |
| --- | --- |
| Contato | O modelo Contato captura atributos para contatos, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |
| Cliente potencial | O modelo de cliente potencial captura atributos para clientes potenciais, como detalhes demográficos, informações de contato e entidades comerciais relacionadas. |

{style="table-layout:auto"}

+++

Dependendo do tipo de negócio selecionado, uma lista de modelos é exibida. Selecione o ícone de visualização ![ícone de visualização](../../images/tutorials/templates/preview-icon.png) ao lado de um nome de template para visualizar dados de amostra do template.

![Uma lista de modelos com o ícone de visualização realçado.](../../images/tutorials/templates/templates.png)

A janela de pré-visualização é exibida, permitindo explorar e inspecionar dados de amostra do seu modelo. Quando terminar, selecione **[!UICONTROL Entendi]**.

![A janela de dados da amostra de visualização.](../../images/tutorials/templates/preview-sample-data.png)

Em seguida, selecione o template que deseja usar na lista. Você pode selecionar vários modelos e criar vários fluxos de dados de uma só vez. No entanto, um template só pode ser usado uma vez por conta. Após selecionar seus modelos, selecione **[!UICONTROL Concluir]** e aguarde alguns instantes para que os ativos sejam gerados.

Se você selecionar um item ou itens parciais da lista de modelos disponíveis, todos os esquemas B2B e namespaces de identidade ainda serão gerados para garantir que os relacionamentos B2B entre esquemas sejam configurados corretamente.

>[!NOTE]
>
>Os modelos que já foram usados serão desativados a partir da seleção.

![A lista de modelos com o modelo de Função do Contato da Oportunidade selecionado.](../../images/tutorials/templates/select-template.png)

### Definir um cronograma

A variável [!DNL Microsoft Dynamics] e a variável [!DNL Salesforce] As origens oferecem suporte à programação de fluxos de dados.

Use a interface de programação para configurar uma programação de assimilação para seus fluxos de dados. Defina a frequência de assimilação como **Uma vez** para criar uma assimilação única.

![A interface de agendamento para modelos do Dynamics e do Salesforce.](../../images/tutorials/templates/schedule.png)

Como alternativa, você pode definir a frequência de assimilação como **Minuto**, **Hora**, **Dia** ou **Semana**. Se você agendar seu fluxo de dados para várias assimilações, deverá definir um intervalo para estabelecer um intervalo de tempo entre cada assimilação. Por exemplo, uma frequência de assimilação definida como **Hora** e um intervalo definido como **15** significa que seu fluxo de dados está programado para assimilar dados a cada **15 horas**.

Durante essa etapa, você também pode ativar **preenchimento retroativo** e definir uma coluna para a assimilação incremental de dados. O preenchimento retroativo é usado para assimilar dados históricos, enquanto a coluna definida para assimilação incremental permite que novos dados sejam diferenciados dos dados existentes.

Depois de concluir a configuração da programação de assimilação, selecione **[!UICONTROL Concluir]**.

![A interface de agendamento para modelos do Dynamics e do Salesforce com preenchimento retroativo ativado.](../../images/tutorials/templates/backfill.png)

### Revisar ativos {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Revisar os ativos gerados automaticamente"
>abstract="Pode levar até cinco minutos para gerar todos os ativos. Se você optar por sair da página, receberá uma notificação para retornar depois que os ativos forem concluídos. Você pode revisar os ativos depois que eles são gerados e fazer configurações adicionais ao seu fluxo de dados a qualquer momento."

A variável [!UICONTROL Revisar ativos do modelo] A página exibe os ativos gerados automaticamente como parte do modelo. Nesta página, você pode exibir os esquemas, conjuntos de dados, namespaces de identidade e fluxos de dados gerados automaticamente associados à conexão de origem. Pode levar até cinco minutos para gerar todos os ativos. Se você optar por sair da página, receberá uma notificação para retornar depois que os ativos forem concluídos. Você pode revisar os ativos depois que eles são gerados e fazer configurações adicionais ao seu fluxo de dados a qualquer momento.

Por padrão, os fluxos de dados gerados automaticamente são definidos como um estado de rascunho para permitir mais personalização em configurações, como regras de mapeamento ou frequências programadas. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Visualizar mapeamentos]** para ver os conjuntos de mapeamento criados para o fluxo de dados de rascunho.

![Uma janela suspensa com a opção de visualização de mapeamentos selecionada.](../../images/tutorials/templates/preview.png)

Uma página de visualização é exibida, permitindo que você inspecione a relação de mapeamento entre os campos de dados de origem e os campos de esquema de destino. Depois de visualizar os mapeamentos do fluxo de dados. Selecionar **[!UICONTROL Entendi.]**

![A janela de visualização do mapeamento.](../../images/tutorials/templates/preview-mappings.png)

Você pode atualizar seus fluxos de dados a qualquer momento após a execução. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**. Você é levado para a página de fluxo de trabalho de origens, onde é possível atualizar os detalhes do fluxo de dados, incluindo configurações para assimilação parcial, diagnósticos de erro e notificações de alerta, bem como o mapeamento do fluxo de dados.

Você pode usar a visualização do editor de esquemas para atualizar o esquema gerado automaticamente. Visite o guia em [uso do editor de esquema](../../../xdm/tutorials/create-schema-ui.md) para obter mais informações.

![Uma janela suspensa com a opção atualizar fluxos de dados selecionada.](../../images/tutorials/templates/update.png)

>[!TIP]
>
>Você pode acessar seu fluxo de dados de rascunho por meio da [!UICONTROL Fluxos de dados] página de catálogo no espaço de trabalho de origens. Selecionar **[!UICONTROL Fluxos de dados]** no cabeçalho superior e selecione na lista o fluxo de dados que deseja atualizar.
>
>![Uma lista de fluxos de dados existentes no catálogo de fluxos de dados do espaço de trabalho de origens.](../../images/tutorials/templates/dataflows.png)

### Publicar seu fluxo de dados

Comece o processo de publicação navegando pelo fluxo de trabalho de origens. Depois de selecionar [!UICONTROL Atualizar fluxo de dados], você será levado para a *[!UICONTROL Adicionar dados]* etapa do fluxo de trabalho. Selecionar **[!UICONTROL Próxima]** para continuar.

![A etapa adicionar dados para um fluxo de dados de rascunho](../../images/tutorials/templates/continue-draft.png)

Em seguida, confirme os detalhes do fluxo de dados e defina as configurações para diagnósticos de erro, assimilação parcial e notificações de alerta. Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa de detalhes do fluxo de dados para um fluxo de dados de rascunho.](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>É possível selecionar **[!UICONTROL Salvar como rascunho]** a qualquer momento para interromper e salvar as alterações feitas no fluxo de dados.

A etapa de mapeamento é exibida. Durante essa etapa, você pode reconfigurar as configurações de mapeamento do fluxo de dados. Para obter um guia abrangente sobre as funções de preparação de dados usadas para mapeamento, visite o [guia da interface de preparação de dados](../../../data-prep/ui/mapping.md).

![A etapa de mapeamento para um fluxo de dados de rascunho.](../../images/tutorials/templates/mapping.png)

Por fim, revise os detalhes do fluxo de dados e selecione **[!UICONTROL Salvar e assimilar]** para publicar seu rascunho.

![A etapa de revisão para um fluxo de dados de rascunho.](../../images/tutorials/templates/review.png)

## Próximas etapas

Seguindo este tutorial, você criou fluxos de dados, bem como ativos como esquemas, conjuntos de dados e namespaces de identidade usando modelos. Para obter informações gerais sobre fontes, visite o [visão geral das origens](../../home.md).

## Alertas e notificações {#alerts-and-notifications}

Os modelos são compatíveis com os Alertas do Adobe Experience Platform e você pode usar o painel de notificações para receber atualizações sobre o status dos ativos e também para navegar de volta para a página de revisão.

Selecione o ícone de notificação no cabeçalho superior da interface do Platform e selecione o alerta de status para ver os ativos que deseja revisar.

![O painel de notificações na interface da Platform com uma notificação alertando um fluxo de dados com falha foi destacado.](../../images/tutorials/templates/notifications.png)

Você pode atualizar as configurações de alerta de seus modelos para receber notificações por email e na plataforma sobre o status dos fluxos de dados. Para obter mais informações sobre a configuração de alertas, leia o manual no [como assinar alertas para fluxos de dados de origens](../ui/alerts.md).