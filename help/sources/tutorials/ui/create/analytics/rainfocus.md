---
title: Conectar sua conta RainFocus à Experience Platform usando a interface
description: Saiba como conectar sua conta RainFocus ao Experience Platform usando a interface do usuário.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# Conectar sua conta do [!DNL RainFocus] à Experience Platform usando a interface

>[!NOTE]
>
>A origem [!DNL RainFocus] está na versão beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas sobre como conectar o gerenciamento de eventos e dados de análise da sua conta do [!DNL RainFocus] e do gerenciamento de fluxos de dados do Adobe Experience Platform.

>[!IMPORTANT]
>
>Este conector de origem e página de documentação são criados e mantidos pela equipe [!DNL RainFocus]. Para fazer consultas ou solicitações de atualização, entre em contato diretamente com o clientcare<span>@rainfocus.com ou visite a [[!DNL RainFocus] Central de ajuda](https://help.rainfocus.com/hc/en-us)

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Pré-requisitos

Antes de conectar a conta do [!DNL RainFocus] à Experience Platform, primeiro você deve concluir as seguintes tarefas de pré-requisito:

* [Coletar credenciais necessárias](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Criar um esquema XDM e definir o campo de identidade](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Criar um perfil de integração no RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Após concluir a configuração de pré-requisito, você pode prosseguir para as etapas descritas abaixo.

## Conectar sua conta RainFocus à Experience Platform

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho de fontes. A tela *[!UICONTROL Catálogo]* exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Analytics]*, selecione **[!UICONTROL RainFocus Experience]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do Experience Platform com a fonte RainFocus selecionada.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Selecionar dados

A etapa Selecionar dados é exibida, fornecendo uma interface para que você selecione os dados que trará para o Experience Platform.

* A parte esquerda da interface é um navegador que permite visualizar os fluxos de dados disponíveis em sua conta;
* A parte direita da interface permite visualizar até 100 linhas de dados de um arquivo JSON.

Selecione **[!UICONTROL Carregar arquivos]** para carregar um arquivo JSON do sistema local. Como alternativa, você pode arrastar e soltar o arquivo JSON que deseja fazer upload no painel Arrastar e soltar arquivos.

Carregue a amostra de carga JSON baixada de **RainFocus**.

![A etapa de seleção de dados no fluxo de trabalho de fontes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Depois que o arquivo for carregado, a interface de visualização será atualizada para exibir uma visualização do esquema carregado. A interface de visualização permite inspecionar o conteúdo e a estrutura de um arquivo. Você também pode usar o utilitário de campo Pesquisar para acessar itens específicos no esquema.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de visualização de dados do fluxo de trabalho de fontes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Detalhes do fluxo de dados

A etapa **Detalhes do fluxo de dados** é exibida, fornecendo opções para usar um conjunto de dados existente ou estabelecer um novo para o fluxo de dados, bem como uma oportunidade de fornecer um nome e uma descrição para o fluxo de dados. Durante essa etapa, você também pode definir configurações para Assimilação de perfil, diagnóstico de erro, assimilação parcial e alertas.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Mapeamento {#mapping}

A etapa Mapeamento é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](../../../../../data-prep/ui/mapping.md).

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![A etapa de mapeamento do fluxo de trabalho de origens.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Revisar

A etapa **Revisão** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **Conexão**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **Atribuir campos de conjunto de dados e mapa**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.

Depois de revisar o fluxo de dados, selecione **Concluir** e aguarde algum tempo para que o fluxo de dados seja criado.

![A etapa de revisão do fluxo de trabalho de fontes.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Obter o URL do ponto de extremidade de streaming {#get-your-streaming-endpoint-url}

Com o fluxo de dados de transmissão criado, agora é possível recuperar o URL do ponto de extremidade de transmissão. Esse endpoint será usado para assinar seu webhook, permitindo que a fonte de streaming se comunique com o Experience Platform.

Para recuperar o ponto de extremidade de streaming, vá para a página *[!UICONTROL Atividade de fluxo de dados]* do fluxo de dados que você acabou de criar e copie o ponto de extremidade da parte inferior do painel *[!UICONTROL Propriedades]*.

![A página de atividade de fluxo de dados no espaço de trabalho de fontes, com a URL do ponto de extremidade de streaming realçada.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Ativar seu perfil de integração no RainFocus

Quando o fluxo de dados estiver concluído e você tiver recuperado a URL do ponto de extremidade de streaming, será possível ativar o [!DNL Integration Profile] em [!DNL RainFocus].

* Faça logon na [[!DNL RainFocus] plataforma](https://app.rainfocus.com). Na navegação principal, selecione **[!DNL Libraries]** e **[!DNL Integration Profiles]**
* Abra o [!DNL Integration Profile] criado anteriormente como parte dos [pré-requisitos](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Cole a **ID do Fluxo de Dados** e o **Ponto de Extremidade de Streaming** copiados do Fluxo de Dados no Experience Platform e selecione **Salvar**

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão para a origem [!DNL RainFocus], permitindo que transmita os dados de análise e gerenciamento de eventos para a Experience Platform.

## Recursos adicionais

Os documentos a seguir fornecem orientações adicionais sobre nuances em torno da origem [!DNL RainFocus].

* [Central de ajuda do RainFocus](https://help.rainfocus.com/hc/en-us)
* [Criar uma Conta de Serviço (JWT) da Adobe no Portal do Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Criar um esquema na API](../../../../../xdm/tutorials/create-schema-api.md)
* [Criar um esquema na interface](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definir Campos de Identidade na Interface do Usuário](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
