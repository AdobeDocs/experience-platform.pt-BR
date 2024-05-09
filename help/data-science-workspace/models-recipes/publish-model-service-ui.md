---
keywords: Experience Platform;publicar um modelo;Espaço de trabalho de ciência de dados;tópicos populares;pontuar um serviço
solution: Experience Platform
title: Publicar um modelo como um serviço na interface do usuário do Espaço de trabalho de ciência de dados
type: Tutorial
description: O Espaço de trabalho de ciência de dados da Adobe Experience Platform permite publicar seu Modelo como um serviço treinado e avaliado, permitindo que os usuários em sua organização marquem dados sem a necessidade de criar seus próprios modelos.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: d6a4b149b911cd6e7dbbd6c1289fce64be76b506
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Publicar um modelo como um serviço na interface do usuário do Data Science Workspace {#publish-a-model-as-a-service}

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Publicar um modelo como um serviço"
>abstract=""

O Espaço de trabalho de ciência de dados da Adobe Experience Platform permite publicar seu Modelo como um serviço treinado e avaliado, permitindo que os usuários em sua organização marquem dados sem a necessidade de criar seus próprios modelos.

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar.

Este tutorial requer um modelo existente com uma execução de treinamento bem-sucedida. Se você não tiver um Modelo publicável, siga as instruções [Treinar e avaliar um modelo na interface do usuário](./train-evaluate-model-ui.md) tutorial antes de continuar.

Se preferir publicar um Modelo usando as APIs do Sensei Machine Learning, consulte o [Tutorial de API](./publish-model-service-api.md).

## Publicar um modelo {#publish-a-model}

No Adobe Experience Platform, selecione **[!UICONTROL Modelos]** localizado na coluna de navegação à esquerda, selecione a variável **[!UICONTROL Procurar]** para listar todos os Modelos existentes. Selecione o nome do Modelo que deseja publicar como um Serviço.

![](../images/models-recipes/publish-model/browse_model.png)

Selecionar **[!UICONTROL Publish]** Próximo à parte superior direita da página Visão geral do modelo para iniciar um processo de criação de serviço.

![](../images/models-recipes/publish-model/view_training.png)

Insira um nome desejado para o Serviço e, opcionalmente, forneça uma Descrição do Serviço, selecione **[!UICONTROL Próxima]** quando terminar.

![](../images/models-recipes/publish-model/configure_training.png)

Todas as execuções de treinamento bem-sucedidas para o Modelo são listadas. O novo Serviço herdará as configurações de treinamento e pontuação da execução de treinamento selecionada.

![](../images/models-recipes/publish-model/select_training_run.png)

Selecionar **[!UICONTROL Concluir]** para criar o Serviço e redirecionar para a **[!UICONTROL Galeria de Serviços]** para mostrar todos os Serviços disponíveis, incluindo o Serviço recém-criado.

![](../images/models-recipes/publish-model/service_gallery.png)

## Pontuação usando um serviço {#access-a-service}

No Adobe Experience Platform, selecione a variável **[!UICONTROL Serviços]** localizada na coluna de navegação à esquerda para acessar a **[!UICONTROL Galeria de Serviços]**. Localize o Serviço que deseja usar e selecione **[!UICONTROL Abertura]**.

![](../images/models-recipes/publish-model/open_service.png)

Na página de visão geral do serviço, selecione **[!UICONTROL Pontuação]**.

![](../images/models-recipes/publish-model/score_service.png)

Selecione um conjunto de dados de entrada apropriado para a execução de pontuação e selecione **[!UICONTROL Próxima]**. Você será solicitado a fazer a mesma etapa para o conjunto de dados de pontuação. Após selecionar o conjunto de dados de entrada e saída, você pode atualizar as configurações.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando um Serviço é criado, ele herda as configurações de pontuação padrão. É possível revisar essas configurações e ajustá-las conforme necessário, clicando duas vezes nos valores. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Concluir]** para iniciar a execução da pontuação.

![](../images/models-recipes/publish-model/scoring_configs.png)

No do Serviço **Visão geral** detalhes do novo trabalho de pontuação e seu progresso são mostrados. Quando o processo for concluído, a variável **[!UICONTROL Mais recente]** cabeçalho dentro do **[!UICONTROL Pontuação]** o contêiner é atualizado.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Próximas etapas {#next-steps}

Seguindo este tutorial, você publicou com êxito um Modelo como um Serviço acessível e pontuou os dados usando o novo Serviço por meio da [!UICONTROL Galeria de Serviços]. Continue com o próximo tutorial para saber como você pode [agendar execuções de treinamento e pontuação automatizados em um Serviço](./schedule-models-ui.md).
