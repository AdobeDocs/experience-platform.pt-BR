---
keywords: Experience Platform, agendar um modelo, Data Science Workspace, tópicos populares, pontuação de agendamento, agendar treinamento
solution: Experience Platform
title: Programar um modelo na interface do usuário do Data Science Workspace
topic: tutorial
type: Tutorial
description: O Adobe Experience Platform Data Science Workspace permite que você configure execuções programadas de pontuação e treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um Serviço ao longo do tempo, acompanhando os padrões em seus dados.
translation-type: tm+mt
source-git-commit: 8f5b7018a52d4c5860e03cec3108435ede8815f1
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Programar um modelo na interface do usuário do Data Science Workspace

O Adobe Experience Platform [!DNL Data Science Workspace] permite que você configure a pontuação agendada e a execução do treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, mantendo os padrões em seus dados.

Este tutorial percorre as etapas para configurar agendamentos de treinamento e pontuação em um serviço existente por meio do [!UICONTROL Service Gallery]. Ele é dividido nas seguintes seções principais:

- [Configurar pontuação agendada](#configure-scheduled-scoring)
- [Configurar treinamento programado](#configure-scheduled-training)

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um serviço existente. Se você não tiver um serviço acessível para trabalhar, crie um seguindo o tutorial para [publicar um modelo como um serviço](./publish-model-service-ui.md).

## Configurar pontuação agendada {#configure-scheduled-scoring}

A pontuação do modelo pode ser configurada para ser um processo automatizado de forma programada. Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de pontuação:

No Adobe Experience Platform, selecione a guia **[!UICONTROL Services]** localizada na coluna de navegação esquerda para acessar o **[!DNL Service Gallery]**. Encontre o serviço que deseja agendar a execução da pontuação e selecione **[!UICONTROL Open]** para visualizar a página **[!UICONTROL Overview]**.

![](../images/models-recipes/schedule/select_service.png)

A página Visão geral exibe as informações de pontuação do Serviço. Selecione o link **[!UICONTROL Update Schedule]** para configurar um agendamento de pontuação.

![](../images/models-recipes/schedule/update_scoring.png)

Configure a frequência, a data de início, a data de término, o conjunto de dados de entrada e o conjunto de dados de saída para a programação de pontuação. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Create]** para atualizar o agendamento de pontuação do serviço.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

O agendamento de pontuação atualizado é mostrado na página **[!UICONTROL Overview]** do serviço.

![](../images/models-recipes/schedule/scoring_set.png)

## Configurar o treinamento agendado {#configure-scheduled-training}

Configurar o treinamento programado é executado em um serviço garante que o modelo de aprendizado de máquina seja atualizado para os padrões de dados mais recentes. Sempre que uma execução de treinamento programada é concluída, o modelo treinado resultante é usado para alimentar o serviço até a próxima execução de treinamento programada.

Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de treinamento:

No Adobe Experience Platform, selecione a guia **[!UICONTROL Services]** localizada na coluna de navegação esquerda para acessar o **[!UICONTROL Service Gallery]**. Encontre o serviço que deseja agendar a execução do treinamento e selecione **[!UICONTROL Open]** para visualizar sua página **[!UICONTROL Overview]**.

![](../images/models-recipes/schedule/select_service.png)

A página Visão geral exibe as informações de treinamento do serviço. Selecione o link **[!UICONTROL Update Schedule]** para configurar um cronograma de treinamento.

![](../images/models-recipes/schedule/update_training.png)

Configure a frequência, a data de início, a data de término e o conjunto de dados de entrada usados para o cronograma de treinamento. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Create]** para atualizar o cronograma de treinamento do serviço.

![](../images/models-recipes/schedule/set_training_schedule.png)

Seu cronograma de treinamento atualizado é mostrado na página **[!UICONTROL Overview]** do serviço.

![](../images/models-recipes/schedule/training_set.png)

## Próximas etapas

Ao seguir este tutorial, você agendou com êxito a execução de treinamento e pontuação automatizadas em um serviço e concluiu o fluxo de trabalho da interface do usuário do tutorial [!DNL Data Science Workspace]. Se ainda não tiver feito isso, considere [reiniciar o tutorial](./create-retails-sales-dataset.md) e siga o fluxo de trabalho da API para criar, treinar, pontuar e publicar um modelo.
