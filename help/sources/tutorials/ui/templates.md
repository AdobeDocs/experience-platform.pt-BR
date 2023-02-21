---
description: O Adobe Experience Platform fornece modelos pré-configurados que podem ser usados para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, regras de mapeamento, identidades, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma fonte para o Experience Platform.
title: (Beta) Criar um fluxo de dados de origens usando modelos na interface do usuário
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# (Beta) Criar um fluxo de dados de origens usando modelos na interface do usuário

>[!IMPORTANT]
>
>Os modelos estão em beta e são compatíveis com as seguintes fontes:
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>A documentação e as funcionalidades estão sujeitas a alterações.

O Adobe Experience Platform fornece modelos pré-configurados que podem ser usados para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, identidades, regras de mapeamento, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma fonte para o Experience Platform.

Com modelos, você pode:

* Reduza o tempo para o valor da assimilação por meio da aceleração da criação de ativos modelos.
* Minimize erros que podem ocorrer durante o processo manual de assimilação de dados.
* Atualize os ativos gerados automaticamente em qualquer ponto para atender aos seus casos de uso.

O tutorial a seguir fornece etapas sobre como usar modelos na interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Sandboxes](../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Usar modelos na interface do usuário da plataforma {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="Selecionar tipo de negócio"
>abstract="Selecione o tipo de negócio apropriado para seu caso de uso. O acesso pode variar dependendo da conta de assinatura da Real-time Customer Data Platform."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=pt-BR" text="Visão geral do Real-Time CDP"

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] e veja um catálogo de fontes disponível no Experience Platform.

Use o *[!UICONTROL Categorias]* para filtrar fontes por categoria. Como alternativa, insira um nome de origem na barra de pesquisa para localizar uma origem específica no catálogo.

Vá para o [!UICONTROL Aplicativos Adobe] para ver a [!DNL Marketo Engage] cartão de origem e, em seguida, selecione [!UICONTROL Adicionar dados] para começar.

![Um catálogo da área de trabalho de origens com a origem de Marketo Engage realçada.](../../images/tutorials/templates/catalog.png)

Uma janela pop-up é exibida apresentando a opção de navegar pelos modelos ou usar esquemas e conjuntos de dados existentes.

* **Procurar modelos**: Os modelos de origens criam esquemas, identidades, conjuntos de dados e fluxos de dados automaticamente com regras de mapeamento para você. Você pode personalizar esses ativos conforme necessário.
* **Usar meus ativos existentes**: Assimile seus dados usando conjuntos de dados e esquemas existentes que você criou. Você também pode criar novos conjuntos de dados e esquemas, se necessário.

Para usar ativos gerados automaticamente, selecione **[!UICONTROL Procurar modelos]** e depois selecione **[!UICONTROL Selecionar]**.

![Uma janela pop-up com opções para procurar modelos ou usar ativos existentes.](../../images/tutorials/templates/browse-templates.png)

### Autenticação

A etapa de autenticação é exibida, solicitando que você crie uma nova conta ou use uma conta existente.

>[!BEGINTABS]

>[!TAB Usar uma conta existente]

Para usar uma conta existente, selecione [!UICONTROL Conta existente] e selecione a conta que deseja usar na lista exibida.

![A página de seleção de uma conta existente com uma lista de contas existentes que você pode acessar.](../../images/tutorials/templates/existing-account.png)

>[!TAB Criar uma nova conta]

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça os detalhes da conexão de origem e as credenciais de autenticação da conta. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e permitir que a nova conexão seja estabelecida.

![A página de autenticação de uma nova conta com detalhes da conexão de origem e credenciais de autenticação da conta.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### Selecionar modelos

Dependendo do tipo de negócio selecionado, é exibida uma lista de modelos. Selecione o ícone de visualização ![ícone de visualização](../../images/tutorials/templates/preview-icon.png) ao lado de um nome de modelo para visualizar dados de amostra do modelo.

![Uma lista de modelos com o ícone de visualização realçado.](../../images/tutorials/templates/templates.png)

A janela de pré-visualização é exibida, permitindo explorar e inspecionar dados de amostra de seu modelo. Quando terminar, selecione **[!UICONTROL Entendi]**.

![A janela de pré-visualização de dados de amostra.](../../images/tutorials/templates/preview-sample-data.png)

Em seguida, selecione o template que deseja usar na lista. Você pode selecionar vários modelos e criar vários fluxos de dados de uma só vez. No entanto, um template só pode ser usado uma vez por conta. Após selecionar seus modelos, selecione **[!UICONTROL Concluir]** e permitir que alguns minutos os ativos sejam gerados.

Se você selecionar um ou mais itens parciais da lista de modelos disponíveis, todos os esquemas B2B e namespaces de identidade ainda serão gerados para garantir que os relacionamentos B2B entre esquemas sejam configurados corretamente.

>[!NOTE]
>
>Os modelos que já foram usados serão desativados na seleção.

![A lista de modelos com o modelo de Função de Contato de Oportunidade selecionado.](../../images/tutorials/templates/select-template.png)

### Definir um agendamento

O [!DNL Microsoft Dynamics] e [!DNL Salesforce] ambas as fontes oferecem suporte para fluxos de dados de agendamento.

Use a interface de agendamento para configurar um agendamento de assimilação para seus fluxos de dados. Defina sua frequência de assimilação como **Uma vez** para criar uma assimilação única.

![A interface de agendamento para modelos do Dynamics e Salesforce.](../../images/tutorials/templates/schedule.png)

Como alternativa, você pode definir sua frequência de assimilação como **Minuto**, **Hora**, **Dia** ou **Semana**. Se agendar seu fluxo de dados para várias assimilações, você deverá definir um intervalo para estabelecer um intervalo de tempo entre cada ingestão. Por exemplo, uma frequência de assimilação definida como **Hora** e um intervalo definido como **15.** significa que o fluxo de dados está agendado para assimilar dados a cada **15 horas**.

Durante essa etapa, também é possível ativar **preenchimento retroativo** e defina uma coluna para a assimilação incremental de dados. O preenchimento retroativo é usado para assimilar dados históricos, enquanto a coluna definida para assimilação incremental permite que novos dados sejam diferenciados dos dados existentes.

Depois de concluir a configuração do agendamento de ingestão, selecione **[!UICONTROL Concluir]**.

![A interface de agendamento para modelos do Dynamics e Salesforce com preenchimento retroativo ativado.](../../images/tutorials/templates/backfill.png)

### Revisar ativos {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Revisar os ativos gerados automaticamente"
>abstract="Pode levar até cinco minutos para gerar todos os ativos. Se você optar por sair da página, receberá uma notificação para retornar depois que os ativos forem concluídos. Você pode revisar os ativos depois que eles são gerados e fazer configurações adicionais ao seu fluxo de dados a qualquer momento."

O [!UICONTROL Revisar ativos do modelo] exibe os ativos gerados automaticamente como parte do modelo. Nesta página, você pode visualizar os esquemas, conjuntos de dados, namespaces de identidade e fluxos de dados gerados automaticamente associados à conexão de origem. Pode levar até cinco minutos para gerar todos os ativos. Se você optar por sair da página, receberá uma notificação para retornar depois que os ativos forem concluídos. Você pode revisar os ativos depois que eles são gerados e fazer configurações adicionais ao seu fluxo de dados a qualquer momento.

Os fluxos de dados gerados automaticamente são ativados por padrão. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Visualizar mapeamentos]** para ver os conjuntos de mapeamento criados para o fluxo de dados.

![Uma janela suspensa com a opção preview mappings selecionada.](../../images/tutorials/templates/preview.png)

Uma página de visualização é exibida, permitindo inspecionar a relação de mapeamento entre os campos de dados de origem e os campos de esquema de destino. Depois de visualizar os mapeamentos do seu fluxo de dados. Selecionar **[!UICONTROL Entendi.]**

![A janela de pré-visualização de mapeamento.](../../images/tutorials/templates/preview-mappings.png)

Você pode atualizar seus fluxos de dados a qualquer momento após a execução. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**. Você é levado à página de fluxo de trabalho de fontes, onde é possível atualizar os detalhes do fluxo de dados, incluindo as configurações de assimilação parcial, diagnósticos de erros e notificações de alertas, bem como o mapeamento do fluxo de dados.

Você pode usar a visualização do editor de esquema para fazer atualizações no esquema gerado automaticamente. Visite o guia em [uso do editor de esquema](../../../xdm/tutorials/create-schema-ui.md) para obter mais informações.

![Uma janela suspensa com a opção atualizar fluxos de dados selecionada.](../../images/tutorials/templates/update.png)

## Próximas etapas

Ao seguir este tutorial, você criou fluxos de dados, bem como ativos como esquemas, conjuntos de dados e namespaces de identidade usando modelos. Para obter informações gerais sobre fontes, visite o [visão geral das fontes](../../home.md).

## Apêndice

A seção a seguir fornece informações adicionais sobre modelos.

### Usar o painel de notificações para retornar à página de revisão

Os alertas do Adobe Experience Platform dão suporte a modelos e você pode usar o painel de notificações para receber atualizações sobre o status de seus ativos e também para navegar de volta para a página de revisão.

Selecione o ícone de notificação no cabeçalho superior da interface do usuário da plataforma e selecione o alerta de status para ver os ativos que deseja revisar.

![O painel de notificações na interface do usuário da plataforma com uma notificação alertando um fluxo de dados com falha foi realçado.](../../images/tutorials/templates/notifications.png)
