---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicar um modelo como um serviço (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Publicar um modelo como um serviço (UI)

A Adobe Experience Platform Data Science Workspace permite que você publique seu Modelo treinado e avaliado como um Serviço, permitindo que os usuários em sua organização IMS pontuem dados sem a necessidade de criar seus próprios Modelos.

Este tutorial percorre as etapas para publicar um Modelo como um Serviço e pontuar dados usando um Serviço pela Galeria *de* Serviços. Ele é dividido nas seguintes seções principais:

- [Publicar um modelo](#publish-a-model)
- [Pontuação usando um serviço](#access-a-service)

## Introdução

Para concluir este tutorial, é necessário ter acesso à plataforma Experience. Se você não tiver acesso a uma organização IMS na plataforma Experience, fale com o administrador do sistema antes de prosseguir.

Este tutorial requer um Modelo existente com uma execução de treinamento bem-sucedida. Se você não tiver um Modelo publicável, siga o [Train e avalie um Modelo no tutorial da interface do usuário](./train-evaluate-model-ui.md) antes de continuar.

Se preferir publicar um Modelo usando APIs de aprendizado de máquina, consulte o tutorial [da](./publish-model-service-api.md)API.

## Publicar um modelo {#publish-a-model}

1. Na Adobe Experience Platform, clique no **[!UICONTROL Models]** link localizado na coluna de navegação esquerda para lista de todos os modelos existentes. Localize e clique no nome do Modelo a ser publicado como um Serviço.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Clique **[!UICONTROL Publish]** próximo à parte superior direita da página Visão geral do Modelo para start de um processo de criação do Serviço.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Insira um nome desejado para o Serviço e, opcionalmente, forneça uma descrição do Serviço, clique **[!UICONTROL Next]** quando terminar.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Todos os treinamentos bem-sucedidos executados para o Modelo são listados. O novo Serviço herdará configurações de treinamento e pontuação da execução de treinamento selecionada.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Clique em **[!UICONTROL Finish]** para criar o Serviço e redirecionar para **[!UICONTROL Service Gallery]** para mostrar todos os Serviços disponíveis, incluindo o Serviço recém-criado.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Pontuação usando um serviço {#access-a-service}

1. No Adobe Experience Platform, clique na **[!UICONTROL Services]** guia localizada na coluna de navegação esquerda para acessar a *Service Gallery*. Localize o Serviço que deseja usar e clique em **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Selecione um conjunto de dados de entrada apropriado para a execução de pontuação e clique em **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Selecione um conjunto de dados de saída apropriado para os resultados da pontuação e clique em **[!UICONTROL Next]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Quando um Serviço é criado, ele herda configurações de pontuação padrão. Você pode revisar essas configurações e ajustá-las conforme necessário clicando com o duplo nos valores. Quando estiver satisfeito com as configurações, clique em **[!UICONTROL Finish]** para começar a execução da pontuação.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Na página *Visão geral* do serviço, os detalhes do novo trabalho de pontuação e seu progresso são mostrados. Quando a tarefa for concluída, a tarefa de **[!UICONTROL Most Recent]** pontuação será atualizada.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você publicou com êxito um Modelo como um Serviço acessível e marcou dados usando o novo Serviço por meio da *Service Gallery*. Continue para o próximo tutorial para saber como [agendar execuções de treinamento e pontuação automatizadas em um Serviço](./schedule-models-ui.md).
