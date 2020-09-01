---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics;schedule scoring;schedule training
solution: Experience Platform
title: Agendar um modelo (UI)
topic: Tutorial
description: A Adobe Experience Platform Data Science Workspace permite que você configure execuções programadas de pontuação e treinamento em um serviço de aprendizado de máquina. Automatizar o processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões em seus dados.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Agendar um modelo (UI)

A Adobe Experience Platform [!DNL Data Science Workspace] permite que você configure execuções programadas de pontuação e treinamento em um Serviço de aprendizado de máquina. Automatizar o processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões em seus dados.

Este tutorial percorre as etapas para configurar os agendamentos de treinamento e pontuação em um Serviço existente por meio da Galeria **[!UICONTROL de]** serviços. Ele é dividido nas seguintes seções principais:

- [Configurar pontuação programada](#configure-scheduled-scoring)
- [Configurar treinamento agendado](#configure-scheduled-training)

## Introdução

Para concluir este tutorial, é necessário ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de prosseguir.

Este tutorial requer um Serviço existente. Se você não tiver um Serviço acessível para trabalhar, poderá criar um seguindo o tutorial [Publicar seu modelo como um serviço na interface do usuário](./publish-model-service-ui.md) .

## Configurar pontuação programada {#configure-scheduled-scoring}

A pontuação do modelo pode ser configurada para ser um processo automatizado em uma base programada. Depois que um Serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de pontuação:

1. No Adobe Experience Platform, clique na guia **[!UICONTROL Serviços]** localizada na coluna de navegação esquerda para acessar o *[!DNL Service Gallery]*. Localize o Serviço no qual você deseja agendar a pontuação e clique em **[!UICONTROL Abrir]** para visualização na página *Visão geral* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. A página Visão geral exibe as informações de pontuação do Serviço. Clique no link **[!UICONTROL Atualizar agendamento]** para configurar um agendamento de pontuação.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Configure a frequência, a data do start, a data de término, o conjunto de dados de entrada e o conjunto de dados de saída para a programação de pontuação. Quando estiver satisfeito com as configurações, clique em **[!UICONTROL Criar]** para atualizar o agendamento de pontuação do Serviço.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Seu agendamento de pontuação atualizado é mostrado na página *Visão geral* do serviço.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Configurar treinamento agendado {#configure-scheduled-training}

A configuração de execuções de treinamento programado em um Serviço garante que o Modelo de aprendizado da máquina seja atualizado para os padrões de dados mais recentes. Sempre que uma execução de treinamento programada for concluída, o Modelo treinado resultante será usado para alimentar o Serviço até a próxima execução de treinamento programada.

Depois que um Serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de treinamento:

1. No Adobe Experience Platform, clique na guia **[!UICONTROL Serviços]** localizada na coluna de navegação esquerda para acessar a **[!UICONTROL Service Gallery]**. Localize o Serviço no qual você deseja programar a execução do treinamento e clique em **[!UICONTROL Abrir]** para visualização na página *Visão geral* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. A página Visão geral exibe as informações de treinamento do Serviço. Clique no link **[!UICONTROL Atualizar agendamento]** para configurar um agendamento de treinamento.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Configure a frequência, a data do start, a data de término e o conjunto de dados de entrada usados para a programação de treinamento. Quando estiver satisfeito com as configurações, clique em **[!UICONTROL Criar]** para atualizar a programação de treinamento do Serviço.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Seu cronograma de treinamento atualizado é mostrado na página *Visão geral* do serviço.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Próximas etapas

Ao seguir este tutorial, você agendou com êxito as execuções de treinamento e pontuação automatizadas em um Serviço e concluiu o fluxo de trabalho da interface do [!DNL Data Science Workspace] tutorial. Caso ainda não o tenha feito, considere [reiniciar o tutorial](./create-retails-sales-dataset.md) e seguir o fluxo de trabalho da API para criar, treinar, marcar e publicar um Modelo.
