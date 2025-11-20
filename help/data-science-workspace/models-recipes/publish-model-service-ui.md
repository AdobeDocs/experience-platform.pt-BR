---
keywords: Experience Platform;publicar um modelo;Data Science Workspace;tópicos populares;pontuação de um serviço;;publish a model;Data Science;popular topics;score a service
solution: Experience Platform
title: Publicar um modelo como um serviço na interface do usuário do Data Science Workspace
type: Tutorial
description: O Adobe Experience Platform Data Science Workspace permite publicar seu Modelo como um serviço treinado e avaliado, permitindo que os usuários em sua organização marquem dados sem a necessidade de criar seus próprios modelos.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 4%

---

# Publicar um modelo como um serviço na interface do usuário do Espaço de trabalho de ciência de dados {#publish-a-model-as-a-service}

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Publicar um modelo como um serviço"
>abstract=""

O Adobe Experience Platform Data Science Workspace permite publicar seu Modelo como um serviço treinado e avaliado, permitindo que os usuários em sua organização marquem dados sem a necessidade de criar seus próprios modelos.

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um modelo existente com uma execução de treinamento bem-sucedida. Se você não tiver um Modelo publicável, siga o [Treinar e avalie um Modelo na interface do usuário](./train-evaluate-model-ui.md) antes de continuar.

Se preferir publicar um Modelo usando as APIs do Sensei Machine Learning, consulte o [tutorial sobre API](./publish-model-service-api.md).

## Publicar um modelo {#publish-a-model}

No Adobe Experience Platform, selecione **[!UICONTROL Models]**, localizado na coluna de navegação à esquerda, e depois selecione a guia **[!UICONTROL Browse]** para listar todos os Modelos existentes. Selecione o nome do Modelo que deseja publicar como um Serviço.

![](../images/models-recipes/publish-model/browse_model.png)

Selecione **[!UICONTROL Publish]** próximo à parte superior direita da página Visão geral do modelo para iniciar um processo de criação de serviço.

![](../images/models-recipes/publish-model/view_training.png)

Insira um nome desejado para o Serviço e, opcionalmente, forneça uma Descrição do serviço. Selecione **[!UICONTROL Next]** quando terminar.

![](../images/models-recipes/publish-model/configure_training.png)

Todas as execuções de treinamento bem-sucedidas para o Modelo são listadas. O novo Serviço herdará as configurações de treinamento e pontuação da execução de treinamento selecionada.

![](../images/models-recipes/publish-model/select_training_run.png)

Selecione **[!UICONTROL Finish]** para criar o Serviço e redirecionar para **[!UICONTROL Service Gallery]** para mostrar todos os Serviços disponíveis, incluindo o Serviço recém-criado.

![](../images/models-recipes/publish-model/service_gallery.png)

## Pontuação usando um serviço {#access-a-service}

No Adobe Experience Platform, selecione a guia **[!UICONTROL Services]**, localizada na coluna de navegação à esquerda, para acessar o **[!UICONTROL Service Gallery]**. Localize o Serviço que deseja usar e selecione **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Na página de visão geral do serviço, selecione **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Selecione um conjunto de dados de entrada apropriado para a execução de pontuação e, em seguida, selecione **[!UICONTROL Next]**. Você será solicitado a fazer a mesma etapa para o conjunto de dados de pontuação. Após selecionar o conjunto de dados de entrada e saída, você pode atualizar as configurações.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando um Serviço é criado, ele herda as configurações de pontuação padrão. É possível revisar essas configurações e ajustá-las conforme necessário, clicando duas vezes nos valores. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Finish]** para começar a execução de pontuação.

![](../images/models-recipes/publish-model/scoring_configs.png)

Na página **Visão geral** do serviço, os detalhes do novo trabalho de pontuação e seu progresso são mostrados. Quando o trabalho for concluído, o cabeçalho **[!UICONTROL Most Recent]** no container **[!UICONTROL Scoring]** será atualizado.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Próximas etapas {#next-steps}

Seguindo este tutorial, você publicou com êxito um Modelo como um Serviço acessível e pontuou os dados usando o novo Serviço por meio do [!UICONTROL Service Gallery]. Prossiga para o próximo tutorial para saber como você pode [agendar treinamentos automatizados e execuções de pontuação em um Serviço](./schedule-models-ui.md).
