---
keywords: Experience Platform;agendar um modelo;Data Science Workspace;tópicos populares;pontuação de agendamento;agendar treinamento
solution: Experience Platform
title: Agendar um modelo na interface do Espaço de trabalho de ciência de dados
type: Tutorial
description: O Espaço de trabalho de ciência de dados da Adobe Experience Platform permite configurar a pontuação programada e as execuções de treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um Serviço ao longo do tempo, acompanhando os padrões dos seus dados.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Agendar um modelo na interface do Espaço de trabalho de ciência de dados

Adobe Experience Platform [!DNL Data Science Workspace] permite configurar a pontuação programada e as execuções de treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e de pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões dos seus dados.

Este tutorial aborda as etapas para configurar programações de treinamento e pontuação em um serviço existente por meio do [!UICONTROL Galeria de Serviços]. Ela está dividida nas seguintes seções principais:

- [Configurar pontuação programada](#configure-scheduled-scoring)
- [Configurar treinamento programado](#configure-scheduled-training)

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar.

Este tutorial requer um serviço existente. Se você não tiver um serviço acessível para trabalhar, poderá criar um seguindo o tutorial para [publicação de um modelo como um serviço](./publish-model-service-ui.md).

## Configurar pontuação programada {#configure-scheduled-scoring}

A pontuação do modelo pode ser configurada para ser um processo automatizado de forma programada. Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um agendamento de pontuação:

No Adobe Experience Platform, selecione a variável **[!UICONTROL Serviços]** localizada na coluna de navegação à esquerda para acessar a **[!DNL Service Gallery]**. Localize o serviço no qual deseja programar execuções de pontuação e selecione **[!UICONTROL Abertura]** para visualizar suas **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/select_service.png)

A página Visão Geral exibe as informações de pontuação do Serviço. Selecione o **[!UICONTROL Atualizar programação]** link para configurar uma programação de pontuação.

![](../images/models-recipes/schedule/update_scoring.png)

Configure a frequência, a data de início, a data de término, o conjunto de dados de entrada e o conjunto de dados de saída para a programação de pontuação. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Criar]** para atualizar a programação de pontuação do serviço.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Sua programação de pontuação atualizada é mostrada no campo **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/scoring_set.png)

## Configurar treinamento programado {#configure-scheduled-training}

A configuração da execução programada do treinamento em um serviço garante que o modelo de aprendizado de máquina seja atualizado para os padrões de dados mais recentes. Sempre que uma execução de treinamento programada é concluída, o modelo treinado resultante é usado para potencializar o serviço até a próxima execução de treinamento programada.

Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um cronograma de treinamento:

No Adobe Experience Platform, selecione a variável **[!UICONTROL Serviços]** localizada na coluna de navegação à esquerda para acessar a **[!UICONTROL Galeria de Serviços]**. Encontre o serviço no qual deseja agendar execuções de treinamento e selecione **[!UICONTROL Abertura]** para visualizar suas **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/select_service.png)

A página Visão Geral exibe as informações de treinamento do serviço. Selecione o **[!UICONTROL Atualizar programação]** link para configurar uma programação de treinamento.

![](../images/models-recipes/schedule/update_training.png)

Configure a frequência, a data de início, a data de término e o conjunto de dados de entrada usados para a programação de treinamento. Quando estiver satisfeito com as configurações, selecione **[!UICONTROL Criar]** para atualizar a programação de treinamento do serviço.

![](../images/models-recipes/schedule/set_training_schedule.png)

Sua programação de treinamento atualizada é mostrada no **[!UICONTROL Visão geral]** página.

![](../images/models-recipes/schedule/training_set.png)

## Próximas etapas

Ao seguir este tutorial, você agendou com êxito as execuções de treinamento automatizado e pontuação em um serviço e concluiu o [!DNL Data Science Workspace] fluxo de trabalho da interface do tutorial. Se ainda não tiver feito isso, considere [reiniciar o tutorial](./create-retails-sales-dataset.md) e siga o fluxo de trabalho da API para criar, treinar, pontuar e publicar um modelo.
