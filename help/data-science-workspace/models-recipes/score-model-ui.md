---
keywords: Experience Platform; pontuar um modelo; Data Science Workspace; tópicos populares; interface do usuário; execução de pontuação; resultados de pontuação
solution: Experience Platform
title: Pontuar um modelo na interface do usuário do Data Science Workspace
topic: tutorial
type: Tutorial
description: 'A pontuação no Adobe Experience Platform Data Science Workspace pode ser obtida ao alimentar os dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote. '
translation-type: tm+mt
source-git-commit: 7feda18351061600b05dc7be8afbbfb9a0fa7ec1
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---


# Pontuar um modelo na interface do usuário do Data Science Workspace

A pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser alcançada ao alimentar os dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.

Este tutorial demonstra as etapas necessárias para pontuar um Modelo na interface do usuário [!DNL Data Science Workspace].

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um Modelo treinado. Se você não tiver um Modelo treinado, siga o [trem e avalie um Modelo no tutorial da interface do usuário](./train-evaluate-model-ui.md) antes de continuar.

## Criar uma nova execução de pontuação

Uma execução de pontuação é criada usando configurações otimizadas de uma execução de treinamento previamente concluída e avaliada. O conjunto de configurações ideais para um Modelo normalmente é determinado pela análise de métricas de avaliação de execução de treinamento.

Encontre a execução de treinamento mais ideal para usar suas configurações para pontuação. Em seguida, abra a execução de treinamento desejada selecionando o hiperlink anexado ao seu nome.

![Selecionar execução de treinamento](../images/models-recipes/score/select-run.png)

Na guia de execução de treinamento **[!UICONTROL Evaluation]**, selecione **[!UICONTROL Score]** localizada na parte superior direita da tela. Um novo fluxo de trabalho de pontuação é iniciado.

![](../images/models-recipes/score/training_run_overview.png)

Selecione o conjunto de dados de pontuação de entrada e selecione **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_input.png)

Selecione o conjunto de dados de pontuação de saída, esse é o conjunto de dados de saída dedicado no qual os resultados da pontuação são armazenados. Confirme sua seleção e selecione **[!UICONTROL Next]**.

![](../images/models-recipes/score/scoring_results.png)

A etapa final no fluxo de trabalho solicita configurar a execução da pontuação. Essas configurações são usadas pelo modelo para a execução de pontuação.
Observe que não é possível remover parâmetros herdados que foram definidos durante a criação dos modelos. Você pode editar ou reverter parâmetros não herdados clicando duas vezes no valor ou selecionando o ícone reverter ao passar o mouse sobre a entrada.

![configuração](../images/models-recipes/score/configuration.png)

Revise e confirme as configurações de pontuação e selecione **[!UICONTROL Finish]** para criar e executar a execução da pontuação. Você é direcionado para a guia **[!UICONTROL Scoring Runs]** e a nova execução da pontuação com o status **[!UICONTROL Pending]** é mostrada.

![guia execução de pontuação](../images/models-recipes/score/scoring_runs_tab.png)

Uma execução de pontuação pode ser exibida com um dos seguintes status:
- Pending
- Concluído
- Falha
- Em execução

Os status são atualizados automaticamente. Prossiga para a próxima etapa se o status for **[!UICONTROL Complete]** ou **[!UICONTROL Failed]**.

## Exibir resultados de pontuação

Para visualizar os resultados da pontuação, comece selecionando uma execução de treinamento.

![Selecionar execução de treinamento](../images/models-recipes/score/select-run.png)

Você é redirecionado para a página de execuções de treinamento **[!UICONTROL Evaluation]**. Próximo à parte superior da página de avaliação da execução do treinamento, selecione a guia **[!UICONTROL Scoring Runs]** para exibir uma lista de execuções de pontuação existentes.

![página avaliação](../images/models-recipes/score/view_scoring_runs.png)

Em seguida, selecione uma execução de pontuação para exibir os detalhes da execução.

![executar detalhes](../images/models-recipes/score/view_details.png)

Se a execução de pontuação selecionada tiver um status &quot;Concluído&quot; ou &quot;Falha&quot;, o link **[!UICONTROL View Activity Logs]** será disponibilizado. Se uma execução de pontuação falhar, os logs de execução poderão fornecer informações úteis para determinar o motivo da falha. Para baixar os logs de execução, selecione **[!UICONTROL View Activity Logs]**.

![Selecionar logs de visualização](../images/models-recipes/score/view_logs.png)

A janela **[!UICONTROL View activity logs]** é exibida. Selecione um URL para baixar automaticamente os logs associados.

![](../images/models-recipes/score/activity_logs.png)

Você também tem a opção de exibir seus resultados de pontuação selecionando **[!UICONTROL Preview scoring results dataset]**.

![Selecionar resultados da visualização](../images/models-recipes/score/view_results.png)

É fornecida uma pré-visualização do conjunto de dados de saída.

![resultados da visualização](../images/models-recipes/score/preview_results.png)

Para o conjunto completo de resultados da pontuação, selecione o link **[!UICONTROL Scoring Results Dataset]** encontrado na coluna direita.

## Próximas etapas

Este tutorial o orientou pelas etapas para pontuar dados usando um Modelo treinado em [!DNL Data Science Workspace]. Siga o tutorial em [publicar um modelo como um serviço na interface do usuário](./publish-model-service-ui.md) para permitir que os usuários em sua organização marquem dados fornecendo acesso fácil a um serviço de aprendizado de máquina.
