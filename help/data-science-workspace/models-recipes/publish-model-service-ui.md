---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics;score a service
solution: Experience Platform
title: Publicar um modelo como um serviço (UI)
topic: Tutorial
description: A Adobe Experience Platform Data Science Workspace permite que você publique seu Modelo treinado e avaliado como um Serviço, permitindo que os usuários na organização IMS pontuem dados sem a necessidade de criar seus próprios Modelos.
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# Publicar um modelo como um serviço (UI)

A Adobe Experience Platform Data Science Workspace permite que você publique seu Modelo treinado e avaliado como um Serviço, permitindo que os usuários na organização IMS pontuem dados sem a necessidade de criar seus próprios Modelos.

## Introdução

Para concluir este tutorial, é necessário ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de prosseguir.

Este tutorial requer um Modelo existente com uma execução de treinamento bem-sucedida. Se você não tiver um Modelo publicável, siga o [Train e avalie um Modelo no tutorial da interface do usuário](./train-evaluate-model-ui.md) antes de continuar.

Se preferir publicar um Modelo usando APIs de aprendizado de máquina, consulte o tutorial [da](./publish-model-service-api.md)API.

## Publicar um modelo {#publish-a-model}

1. No Adobe Experience Platform, clique no link **[!UICONTROL Modelos]** localizado na coluna de navegação esquerda para lista de todos os modelos existentes. Localize e clique no nome do Modelo a ser publicado como um Serviço.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Clique em **[!UICONTROL Publicar]** próximo à parte superior direita da página de visão geral do Modelo para start de um processo de criação do Serviço.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Insira um nome desejado para o Serviço e, opcionalmente, forneça uma descrição do Serviço, clique em **[!UICONTROL Avançar]** ao terminar.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Todos os treinamentos bem-sucedidos executados para o Modelo são listados. O novo Serviço herdará configurações de treinamento e pontuação da execução de treinamento selecionada.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Clique em **[!UICONTROL Concluir]** para criar o Serviço e redirecionar para a Galeria **[!UICONTROL de]** serviços para mostrar todos os Serviços disponíveis, incluindo o Serviço recém-criado.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Pontuação usando um serviço {#access-a-service}

1. No Adobe Experience Platform, clique na guia **[!UICONTROL Serviços]** localizada na coluna de navegação esquerda para acessar a *[!UICONTROL Service Gallery]*. Localize o Serviço que deseja usar e clique em **[!UICONTROL Pontuação]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Selecione um conjunto de dados de entrada apropriado para a execução de pontuação e clique em **[!UICONTROL Avançar]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Selecione um conjunto de dados de saída apropriado para os resultados da pontuação e clique em **[!UICONTROL Avançar]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Quando um Serviço é criado, ele herda configurações de pontuação padrão. Você pode revisar essas configurações e ajustá-las conforme necessário clicando com o duplo nos valores. Quando estiver satisfeito com as configurações, clique em **[!UICONTROL Concluir]** para começar a execução da pontuação.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Na página *Visão geral* do serviço, os detalhes do novo trabalho de pontuação e seu progresso são mostrados. Quando o trabalho for concluído, o trabalho de pontuação **[!UICONTROL mais recente]** será atualizado.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você publicou com êxito um Modelo como um Serviço acessível e marcou dados usando o novo Serviço por meio da *[!UICONTROL Service Gallery]*. Continue para o próximo tutorial para saber como [agendar execuções de treinamento e pontuação automatizadas em um Serviço](./schedule-models-ui.md).
