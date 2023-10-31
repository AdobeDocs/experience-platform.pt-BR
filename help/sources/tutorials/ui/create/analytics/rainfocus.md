---
title: Conectar sua conta RainFocus ao Experience Platform usando a interface
description: Saiba como conectar sua conta RainFocus ao Experience Platform usando a interface do usuário.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 1%

---

# Conecte seu [!DNL RainFocus] conta para Experience Platform usando a interface do usuário

>[!NOTE]
>
>A variável [!DNL RainFocus] a fonte está na versão beta. Consulte a [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas sobre como conectar seus [!DNL RainFocus] gerenciamento de eventos de conta e transmissão e dados do analytics para a Adobe Experience Platform.

>[!IMPORTANT]
>
>Esse conector de origem e a página de documentação são criados e mantidos pelo [!DNL RainFocus] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente com o atendimento ao cliente<span>@rainfocus.com ou visite o [[!DNL RainFocus] Centro de ajuda](https://help.rainfocus.com/hc/en-us)

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Pré-requisitos

Antes de poder conectar seu [!DNL RainFocus] conta para Experience Platform, primeiro você deve concluir as seguintes tarefas de pré-requisito:

* [Coletar credenciais necessárias](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Criar um esquema XDM e definir o campo de identidade](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Criar um perfil de integração no RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Após concluir a configuração de pré-requisito, você pode prosseguir para as etapas descritas abaixo.

## Conectar sua conta RainFocus ao Experience Platform

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação à esquerda para acessar o espaço de trabalho de origens. A variável *[!UICONTROL Catálogo]* exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *[!UICONTROL Analytics]* categoria, selecione **[!UICONTROL Experiência do RainFocus]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do Experience Platform com a fonte RainFocus selecionada.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Selecionar dados

A etapa Selecionar dados é exibida, fornecendo uma interface para que você selecione os dados que traz para o Experience Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecionar **[!UICONTROL Fazer upload de arquivos]** para carregar um arquivo JSON do seu sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload no painel Arrastar e soltar arquivos.

Faça upload da amostra de carga JSON baixada de **RainFocus**.

![A etapa selecionar dados no fluxo de trabalho de fontes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário de campo Pesquisar para acessar itens específicos no esquema.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa de visualização de dados do fluxo de trabalho de fontes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Detalhes do fluxo de dados

A variável **Detalhes do fluxo de dados** A etapa é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próxima]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de origens.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Mapeamento {#mapping}

A etapa Mapeamento é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e campos calculados, consulte o [Guia da interface de preparação de dados](../../../../../data-prep/ui/mapping.md).

Depois que os dados de origem forem mapeados com sucesso, selecione **[!UICONTROL Próxima]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Consulte a seção

A variável **Revisão** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **Conexão**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **Atribuir conjunto de dados e mapear campos**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **Concluir** e aguarde algum tempo para criar o fluxo de dados.

![A etapa de revisão do fluxo de trabalho de origens.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Obter o URL do ponto de extremidade de streaming {#get-your-streaming-endpoint-url}

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para recuperar o ponto de extremidade de transmissão, acesse o *[!UICONTROL Atividade de fluxo de dados]* página do fluxo de dados que você acabou de criar e copie o ponto de extremidade da parte inferior do *[!UICONTROL Propriedades]* painel.

![A página de atividade do fluxo de dados no espaço de trabalho de origens, com o URL do ponto de extremidade de transmissão destacado.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Ativar seu perfil de integração no RainFocus

Quando o fluxo de dados estiver concluído e você tiver recuperado o URL do ponto de extremidade de streaming, será possível ativar o [!DNL Integration Profile] in [!DNL RainFocus].

* Faça logon na [[!DNL RainFocus] platform](https://app.rainfocus.com). Na navegação principal, selecione **[!DNL Libraries]** e **[!DNL Integration Profiles]**
* Abra o [!DNL Integration Profile] que você criou anteriormente como parte da [pré-requisitos](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Cole o **ID do fluxo de dados** e **Endpoint de transmissão** copiado do Fluxo de dados no Experience Platform e selecione **Salvar**

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão para o seu [!DNL RainFocus] fonte, permitindo que você transmita seus dados de análise e gerenciamento de eventos para o Experience Platform.

## Recursos adicionais

Os documentos a seguir fornecem orientações adicionais sobre as nuances relacionadas ao [!DNL RainFocus] origem.

* [Centro de ajuda do RainFocus](https://help.rainfocus.com/hc/en-us)
* [Criar uma conta de serviço da Adobe (JWT) no portal do Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Criar um esquema na API](../../../../../xdm/tutorials/create-schema-api.md)
* [Criar um esquema na interface](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definir campos de identidade na interface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
