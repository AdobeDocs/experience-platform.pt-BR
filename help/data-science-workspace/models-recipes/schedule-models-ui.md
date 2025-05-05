---
keywords: Experience Platform;agendar um modelo;Data Science Workspace;tópicos populares;pontuação de agendamento;agendar treinamento
solution: Experience Platform
title: Programar um modelo na interface do usuário do Data Science Workspace
type: Tutorial
description: O Adobe Experience Platform Data Science Workspace permite configurar a pontuação programada e as execuções de treinamento em um serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um Serviço ao longo do tempo, acompanhando os padrões dos seus dados.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Programar um modelo na interface do usuário do Data Science Workspace

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

[!DNL Data Science Workspace] Adobe Experience Platform permite configurar a pontuação agendada e treinamento é executado em um serviço de aprendizado de máquina. Automatizar o processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço com o tempo, mantendo os padrões dentro de seus dados.

Este tutorial percorre as etapas de configuração de treinamento e agendamentos de pontuação em um serviço existente através da [!UICONTROL Galeria] de serviços. Ele é dividido nas seguintes seções principais:

- [Configurar a pontuação agendada](#configure-scheduled-scoring)
- [Configurar treinamento agendados](#configure-scheduled-training)

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um serviço existente. Se você não tiver um serviço acessível para trabalhar, poderá criar um seguindo o tutorial para [publicar um modelo como um serviço](./publish-model-service-ui.md).

## Configurar a pontuação agendada {#configure-scheduled-scoring}

A pontuação de modelo pode ser configurada para ser um processo automatizado com base em programação. Após criar um serviço, você pode seguir as etapas abaixo para configurar e aplicar um cronograma de pontuação:

Em Adobe Experience Platform, selecione o **[!UICONTROL Guia de Serviços]** localizado na coluna de navegação esquerda para acessar o **[!DNL Service Gallery]**. Localize o serviço em que deseja agendar as corridas de pontuação e selecione **[!UICONTROL Abrir]** para visualização sua **[!UICONTROL visão geral]** página.

![](../images/models-recipes/schedule/select_service.png)

O página Visão geral exibe as informações de pontuação do Serviço. Selecione o **[!UICONTROL link Atualizar agendamento]** para configurar um cronograma de pontuação.

![](../images/models-recipes/schedule/update_scoring.png)

Configure as frequência, start data, data de término, conjunto de dados de entrada e conjunto de dados de saída para o cronograma de pontuação. Depois de estar satisfeito com as configurações, selecione **[!UICONTROL Criar]** para atualizar o cronograma de pontuação do serviço.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

O cronograma de pontuação atualizado é mostrado na página Visão geral **do** serviço.

![](../images/models-recipes/schedule/scoring_set.png)

## Configurar treinamento programado {#configure-scheduled-training}

A configuração da execução programada do treinamento em um serviço garante que o modelo de aprendizado de máquina seja atualizado para os padrões de dados mais recentes. Sempre que uma execução de treinamento programada é concluída, o modelo treinado resultante é usado para potencializar o serviço até a próxima execução de treinamento programada.

Depois que um serviço é criado, você pode seguir as etapas abaixo para configurar e aplicar um cronograma de treinamento:

Em Adobe Experience Platform, selecione o **[!UICONTROL guia serviços]** localizado na coluna de navegação esquerda para acessar a **[!UICONTROL Galeria de serviços]**. Localize o serviço que deseja agendar treinamento executado e selecione **[!UICONTROL Abrir]** para visualização seu **[!UICONTROL página de Visão geral]** .

![](../images/models-recipes/schedule/select_service.png)

A página Visão geral exibe as informações de treinamento do serviço. Selecione o **[!UICONTROL link de agendamento]** de atualização para configurar um cronograma treinamento.

![](../images/models-recipes/schedule/update_training.png)

Configure a frequência, a data start, a data de término e a conjunto de dados de entrada usadas para o agendamento treinamento. Depois de estar satisfeito com as configurações, selecione **[!UICONTROL Criar]** para atualizar o cronograma treinamento do serviço.

![](../images/models-recipes/schedule/set_training_schedule.png)

Sua programação treinamento atualizada é mostrada na página Visão geral **do** serviço.

![](../images/models-recipes/schedule/training_set.png)

## Próximas etapas

Ao seguir este tutorial, você agendou com êxito as execuções de treinamento automatizado e pontuação em um serviço e concluiu o fluxo de trabalho da interface do usuário do tutorial [!DNL Data Science Workspace]. Caso ainda não o tenha feito, considere [reiniciar o tutorial](./create-retails-sales-dataset.md) e siga o fluxo de trabalho da API para criar, treinar, pontuar e publicar um modelo.
