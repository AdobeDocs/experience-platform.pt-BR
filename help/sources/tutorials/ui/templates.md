---
description: A Adobe Experience Platform fornece modelos pré-configurados que você pode usar para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, regras de mapeamento, identidades, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma origem para o Experience Platform.
title: (Beta) Criar um fluxo de dados de fontes usando modelos na interface do
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# (Beta) Criar um fluxo de dados de fontes usando modelos na interface do

>[!IMPORTANT]
>
>Os modelos estão na versão beta e são compatíveis com as seguintes fontes:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>A documentação e as funcionalidades estão sujeitas a alterações.

A Adobe Experience Platform fornece modelos pré-configurados que você pode usar para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, identidades, regras de mapeamento, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma origem para o Experience Platform.

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
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=pt-BR" text="Visão geral do Real-Time CDP"

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
>abstract="A geração de todos os ativos pode levar até cinco minutos. Se você optar por sair da página, receberá uma notificação para retornar assim que os ativos forem concluídos. Você pode revisar os ativos depois que eles forem gerados e fazer configurações adicionais para seu fluxo de dados a qualquer momento."

A variável [!UICONTROL Revisar ativos do modelo] A página exibe os ativos gerados automaticamente como parte do modelo. Nesta página, você pode exibir os esquemas, conjuntos de dados, namespaces de identidade e fluxos de dados gerados automaticamente associados à conexão de origem. A geração de todos os ativos pode levar até cinco minutos. Se você optar por sair da página, receberá uma notificação para retornar assim que os ativos forem concluídos. Você pode revisar os ativos depois que eles forem gerados e fazer configurações adicionais para seu fluxo de dados a qualquer momento.

Os fluxos de dados gerados automaticamente são ativados por padrão. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Visualizar mapeamentos]** para ver os conjuntos de mapeamento criados para o fluxo de dados.

![Uma janela suspensa com a opção de visualização de mapeamentos selecionada.](../../images/tutorials/templates/preview.png)

Uma página de visualização é exibida, permitindo que você inspecione a relação de mapeamento entre os campos de dados de origem e os campos de esquema de destino. Depois de visualizar os mapeamentos do fluxo de dados. Selecionar **[!UICONTROL Entendi.]**

![A janela de visualização do mapeamento.](../../images/tutorials/templates/preview-mappings.png)

Você pode atualizar seus fluxos de dados a qualquer momento após a execução. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**. Você é levado para a página de fluxo de trabalho de origens, onde é possível atualizar os detalhes do fluxo de dados, incluindo configurações para assimilação parcial, diagnósticos de erro e notificações de alerta, bem como o mapeamento do fluxo de dados.

Você pode usar a visualização do editor de esquemas para atualizar o esquema gerado automaticamente. Visite o guia em [uso do editor de esquema](../../../xdm/tutorials/create-schema-ui.md) para obter mais informações.

![Uma janela suspensa com a opção atualizar fluxos de dados selecionada.](../../images/tutorials/templates/update.png)

## Próximas etapas

Seguindo este tutorial, você criou fluxos de dados, bem como ativos como esquemas, conjuntos de dados e namespaces de identidade usando modelos. Para obter informações gerais sobre fontes, visite o [visão geral das origens](../../home.md).

## Apêndice

A seção a seguir fornece informações adicionais sobre templates.

### Use o painel notificações para retornar à página de revisão

Os modelos são compatíveis com alertas do Adobe Experience Platform e você pode usar o painel de notificações para receber atualizações sobre o status dos ativos e também para navegar de volta para a página de revisão.

Selecione o ícone de notificação no cabeçalho superior da interface do Platform e selecione o alerta de status para ver os ativos que deseja revisar.

![O painel de notificações na interface da Platform com uma notificação alertando um fluxo de dados com falha foi destacado.](../../images/tutorials/templates/notifications.png)
