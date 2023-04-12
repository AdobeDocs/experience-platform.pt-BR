---
keywords: Experience Platform, agendar um modelo, Data Science Workspace, tópicos populares, pontuação de agendamento, agendar treinamento
solution: Experience Platform
title: Programar um modelo na interface do usuário do Data Science Workspace
type: Tutorial
description: O Adobe Experience Platform Data Science Workspace permite que você configure execuções programadas de pontuação e treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um Serviço ao longo do tempo, acompanhando os padrões em seus dados.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Programar um modelo na interface do usuário do Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] permite que você configure execuções programadas de pontuação e treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, mantendo os padrões em seus dados.

Este tutorial percorre as etapas para configurar agendamentos de treinamento e pontuação em um serviço existente por meio do [!UICONTROL Galeria de Serviços]. Ele é dividido nas seguintes seções principais:

- [Configurar pontuação agendada](#configure-scheduled-scoring)
- [Configurar treinamento programado](#configure-scheduled-training)

## Introdução

Para concluir este tutorial, você deve ter acesso ao [!DNL Experience Platform]. Se você não tiver acesso a uma organização em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um serviço existente. Se você não tiver um serviço acessível para trabalhar, crie um seguindo o tutorial para [publicar um modelo como um serviço](./publish-model-service-ui.md).

## Configurar pontuação agendada {#configure-scheduled-scoring}

A pontuação do modelo pode ser configurada para ser um processo automatizado agendado. Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de pontuação:

No Adobe Experience Platform, selecione o **[!UICONTROL Serviços]** localizada na coluna de navegação esquerda para acessar o **[!DNL Service Gallery]**. Encontre o serviço em que deseja agendar a pontuação e selecione **[!UICONTROL Abrir]** para visualizar suas **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/select_service.png)

A página Visão geral exibe as informações de pontuação do Serviço. Selecione o **[!UICONTROL Atualizar Programação]** link para configurar um agendamento de pontuação.

![](../images/models-recipes/schedule/update_scoring.png)

Configure a frequência, a data de início, a data de término, o conjunto de dados de entrada e o conjunto de dados de saída para a programação de pontuação. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Criar]** para atualizar o agendamento de pontuação do serviço.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Seu agendamento de pontuação atualizado é mostrado no **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/scoring_set.png)

## Configurar treinamento programado {#configure-scheduled-training}

Configurar o treinamento programado é executado em um serviço garante que o modelo de aprendizado de máquina seja atualizado para os padrões de dados mais recentes. Sempre que uma execução de treinamento programada é concluída, o modelo treinado resultante é usado para alimentar o serviço até a próxima execução de treinamento programada.

Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de treinamento:

No Adobe Experience Platform, selecione o **[!UICONTROL Serviços]** localizada na coluna de navegação esquerda para acessar o **[!UICONTROL Galeria de Serviços]**. Encontre o serviço em que deseja agendar a execução do treinamento e selecione **[!UICONTROL Abrir]** para visualizar suas **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/select_service.png)

A página Visão geral exibe as informações de treinamento do serviço. Selecione o **[!UICONTROL Atualizar Programação]** link para configurar um cronograma de treinamento.

![](../images/models-recipes/schedule/update_training.png)

Configure a frequência, a data de início, a data de término e o conjunto de dados de entrada usados para o cronograma de treinamento. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Criar]** para atualizar o cronograma de treinamento do serviço.

![](../images/models-recipes/schedule/set_training_schedule.png)

Seu cronograma de treinamento atualizado é mostrado no **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/training_set.png)

## Próximas etapas

Ao seguir este tutorial, você agendou com sucesso o treinamento automatizado e a pontuação são executadas em um serviço e concluiu o [!DNL Data Science Workspace] fluxo de trabalho da interface do usuário do tutorial. Se ainda não o fez, considere [reiniciar o tutorial](./create-retails-sales-dataset.md) e siga o fluxo de trabalho da API para criar, treinar, pontuar e publicar um modelo.
