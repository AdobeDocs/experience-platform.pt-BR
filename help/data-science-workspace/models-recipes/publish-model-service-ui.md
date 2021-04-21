---
keywords: Experience Platform, publicar um modelo, Data Science Workspace, tópicos populares, pontuar um serviço
solution: Experience Platform
title: Publicar um modelo como um serviço na interface do usuário do Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: O Adobe Experience Platform Data Science Workspace permite publicar seu Modelo como um Serviço treinado e avaliado, permitindo que os usuários em sua organização IMS marquem dados sem a necessidade de criar seus próprios Modelos.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Publicar um modelo como um serviço na interface do usuário do Data Science Workspace

O Adobe Experience Platform Data Science Workspace permite publicar seu Modelo como um Serviço treinado e avaliado, permitindo que os usuários em sua organização IMS marquem dados sem a necessidade de criar seus próprios Modelos.

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um Modelo existente com uma execução de treinamento bem-sucedida. Se você não tiver um Modelo publicável, siga o [Treinamento e avalie um Modelo no tutorial da interface do usuário](./train-evaluate-model-ui.md) antes de continuar.

Se preferir publicar um Modelo usando APIs de aprendizado de máquina do Sensei, consulte o [tutorial de API](./publish-model-service-api.md).

## Publicar um modelo {#publish-a-model}

No Adobe Experience Platform, selecione **[!UICONTROL Models]** localizado na coluna de navegação esquerda e selecione a guia **[!UICONTROL Browse]** para listar todos os Modelos existentes. Selecione o nome do Modelo que deseja publicar como um Serviço.

![](../images/models-recipes/publish-model/browse_model.png)

Selecione **[!UICONTROL Publish]** próximo ao canto superior direito da página Visão geral do modelo para iniciar um processo de criação de Serviço.

![](../images/models-recipes/publish-model/view_training.png)

Insira um nome desejado para o Serviço e, opcionalmente, forneça uma Descrição do Serviço, selecione **[!UICONTROL Next]** quando terminar.

![](../images/models-recipes/publish-model/configure_training.png)

Todos os treinamentos bem-sucedidos executados para o Modelo são listados. O novo Serviço herdará configurações de treinamento e pontuação da execução de treinamento selecionada.

![](../images/models-recipes/publish-model/select_training_run.png)

Selecione **[!UICONTROL Finish]** para criar o Serviço e redirecionar para **[!UICONTROL Service Gallery]** para mostrar todos os Serviços disponíveis, incluindo o Serviço recém-criado.

![](../images/models-recipes/publish-model/service_gallery.png)

## Pontuação usando um Serviço {#access-a-service}

No Adobe Experience Platform, selecione a guia **[!UICONTROL Services]** localizada na coluna de navegação esquerda para acessar o **[!UICONTROL Service Gallery]**. Encontre o Serviço que deseja usar e selecione **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

Na página de visão geral do serviço, selecione **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Selecione um conjunto de dados de entrada apropriado para a execução da pontuação e selecione **[!UICONTROL Next]**. Você deve fazer a mesma etapa para o conjunto de dados de pontuação. Depois de selecionar o conjunto de dados de entrada e saída, você pode atualizar as configurações.

![](../images/models-recipes/publish-model/select_datasets.png)

Quando um Serviço é criado, ele herda as configurações de pontuação padrão. Você pode revisar essas configurações e ajustá-las conforme necessário clicando duas vezes nos valores. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Finish]** para iniciar a execução da pontuação.

![](../images/models-recipes/publish-model/scoring_configs.png)

Na página **Visão Geral** do Serviço, os detalhes do novo trabalho de pontuação e seu progresso são mostrados. Quando o trabalho for concluído, o cabeçalho **[!UICONTROL Most Recent]** no contêiner **[!UICONTROL Scoring]** será atualizado.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você publicou com sucesso um Modelo como um Serviço acessível e classificou dados usando o novo Serviço pelo [!UICONTROL Service Gallery]. Prossiga para o próximo tutorial para saber como [agendar a execução de treinamentos e pontuações automatizadas em um Serviço](./schedule-models-ui.md).
