---
keywords: Experience Platform; home; tópicos populares;
description: O Adobe Experience Platform fornece modelos pré-configurados que podem ser usados para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, regras de mapeamento, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma fonte para o Experience Platform.
title: (Alfa) Criar um fluxo de dados de fontes usando modelos na interface do usuário
hide: true
hidefromtoc: true
source-git-commit: a0ca9cff43b6f8276268467fecf944c664992950
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---

# (Alfa) Criar um fluxo de dados de fontes usando modelos na interface do usuário

>[!IMPORTANT]
>
>Os modelos estão em Alfa e atualmente só são compatíveis com a variável [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md). A documentação e as funcionalidades estão sujeitas a alterações.

O Adobe Experience Platform fornece modelos pré-configurados que podem ser usados para acelerar o processo de assimilação de dados. Os modelos incluem ativos gerados automaticamente, como esquemas, conjuntos de dados, regras de mapeamento, namespaces de identidade e fluxos de dados que você pode usar ao trazer dados de uma fonte para o Experience Platform.

Com modelos, você pode:

* Reduza o tempo para o valor da assimilação por meio da aceleração da criação de ativos com base em ML.
* Minimize erros que podem ocorrer durante o processo manual de assimilação de dados.
* Atualize os ativos gerados automaticamente em qualquer ponto para atender aos seus casos de uso.

O tutorial a seguir fornece etapas sobre como usar modelos na interface do usuário da plataforma usando o [[!DNL Marketo Engage] source](../../connectors/adobe-applications/marketo/marketo.md).

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

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes que podem ser usadas para criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Aplicativos Adobe] categoria , selecione **[!UICONTROL Marketo Engage]** e depois selecione **[!UICONTROL Adicionar dados]**.

![Um catálogo da área de trabalho de origens com a origem de Marketo Engage realçada.](../../images/tutorials/templates/catalog.png)

Uma janela pop-up é exibida apresentando a opção de navegar pelos modelos ou usar esquemas e conjuntos de dados existentes. Para usar ativos gerados automaticamente, selecione **[!UICONTROL Procurar modelos]** e depois selecione **[!UICONTROL Selecionar]**.

![Uma janela pop-up com opções para procurar modelos ou usar ativos existentes.](../../images/tutorials/templates/browse-templates.png)

### Autenticação

A etapa de autenticação é exibida, solicitando que você crie uma nova conta ou use uma conta existente.

#### Conta existente

Para usar uma conta existente, selecione [!UICONTROL Conta existente] e selecione a conta que deseja usar na lista exibida.

![A página de seleção de uma conta existente com uma lista de contas existentes que você pode acessar.](../../images/tutorials/templates/existing-account.png)

#### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça os detalhes da conexão de origem e as credenciais de autenticação da conta. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e permitir que a nova conexão seja estabelecida.

![A página de autenticação de uma nova conta com detalhes da conexão de origem e credenciais de autenticação da conta.](../../images/tutorials/templates/new-account.png)

### Selecionar modelos

Depois de autenticar e selecionar sua conta, uma lista de modelos é exibida. Selecione o ícone de visualização ao lado do nome do modelo para visualizar os dados de amostra do modelo.

![Uma lista de modelos com o ícone de visualização realçado.](../../images/tutorials/templates/templates.png)

A janela de pré-visualização é exibida, permitindo explorar e inspecionar dados de amostra de seu modelo. Quando terminar, selecione **[!UICONTROL Entendi]**.

![A janela de pré-visualização de dados de amostra.](../../images/tutorials/templates/preview-sample-data.png)

Em seguida, selecione o template que deseja usar na lista. Você pode selecionar vários modelos e criar vários fluxos de dados de uma só vez. No entanto, um template só pode ser usado uma vez por conta. Após selecionar seus modelos, selecione **[!UICONTROL Concluir]** e permitir que alguns minutos os ativos sejam gerados.

![A lista de modelos com o modelo de Função de Contato de Oportunidade selecionado.](../../images/tutorials/templates/select-template.png)

### Revisar ativos {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="Revisar os ativos gerados automaticamente"
>abstract="Pode levar até cinco minutos para gerar todos os ativos. Se você optar por sair da página, receberá uma notificação para retornar depois que os ativos forem concluídos. Você pode revisar os ativos depois que eles são gerados e fazer configurações adicionais ao seu fluxo de dados a qualquer momento."

O [!UICONTROL Revisar ativos do modelo] exibe os ativos gerados automaticamente como parte do modelo. Nesta página, você pode visualizar os esquemas, conjuntos de dados, namespaces de identidade e fluxos de dados gerados automaticamente associados à conexão de origem.

Os fluxos de dados gerados automaticamente são ativados por padrão. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Visualizar mapeamentos]** para ver os conjuntos de mapeamento criados para o fluxo de dados.

![Uma janela suspensa com a opção preview mappings selecionada.](../../images/tutorials/templates/preview.png)

Uma página de visualização é exibida, permitindo inspecionar a relação de mapeamento entre os campos de dados de origem e os campos de esquema de destino. Depois de visualizar os mapeamentos do seu fluxo de dados. Selecionar **[!UICONTROL Entendi.]**

![A janela de pré-visualização de mapeamento.](../../images/tutorials/templates/preview-mappings.png)

Você pode atualizar seus fluxos de dados a qualquer momento após a execução. Selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**. Você é levado à página de fluxo de trabalho de fontes, onde é possível atualizar os detalhes do fluxo de dados, incluindo as configurações de assimilação parcial, diagnósticos de erros e notificações de alertas, bem como o mapeamento do fluxo de dados.

![Uma janela suspensa com a opção atualizar fluxos de dados selecionada.](../../images/tutorials/templates/update.png)

## Próximas etapas

Ao seguir este tutorial, você criou fluxos de dados, bem como ativos como esquemas, conjuntos de dados e namespaces de identidade usando modelos. Para obter informações gerais sobre fontes, visite o [visão geral das fontes](../../home.md).