---
keywords: Experience Platform;pontuação de um modelo;Data Science Workspace;tópicos populares;iu;pontuação executar;pontuação resultados
solution: Experience Platform
title: Pontuar um modelo na interface do usuário do Data Science Workspace
type: Tutorial
description: A pontuação no Adobe Experience Platform Data Science Workspace pode ser obtida ao alimentar dados de entrada em um modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# Pontuar um modelo na interface do usuário do Data Science Workspace

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

A pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser obtida alimentando dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.

Este tutorial demonstra as etapas necessárias para pontuar um Modelo na interface do usuário [!DNL Data Science Workspace].

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Este tutorial requer um modelo treinado. Se você não tiver um Modelo treinado, siga o [treinamento e avalie um Modelo na interface do usuário](./train-evaluate-model-ui.md) tutorial antes de continuar.

## Criar uma nova execução de pontuação

Uma execução de pontuação é criada usando configurações otimizadas de uma execução treinamento previamente concluída e avaliada. O conjunto de configurações ideais para um Modelo é normalmente determinado pela revisão treinamento executar métricas de avaliação.

Encontre o melhor treinamento executado para usar suas configurações para pontuação. Em seguida, abra a execução de treinamento desejada selecionando o hiperlink anexado ao seu nome.

![Selecionar execução de treinamento](../images/models-recipes/score/select-run.png)

Na guia **[!UICONTROL Avaliação]** da execução de treinamento, selecione **[!UICONTROL Pontuação]**, localizado na parte superior direita da tela. Um novo fluxo de trabalho de pontuação é iniciado.

![](../images/models-recipes/score/training_run_overview.png)

Selecione o conjunto de dados de pontuação de entrada e selecione **[!UICONTROL Próximo]**.

![](../images/models-recipes/score/scoring_input.png)

Selecione o conjunto de dados de pontuação de saída, esse é o conjunto de dados de saída dedicado em que os resultados da pontuação são armazenados. Confirme sua seleção e selecione **[!UICONTROL Próximo]**.

![](../images/models-recipes/score/scoring_results.png)

A etapa final no fluxo de trabalho solicita que você configure a execução de pontuação. Essas configurações são usadas pelo modelo para a execução de pontuação.
Observe que não é possível remover parâmetros herdados que foram definidos durante a criação dos modelos. Você pode editar ou reverter parâmetros não herdados clicando duas vezes no valor ou selecionando o ícone de reversão enquanto passa o mouse sobre a entrada.

![configuração](../images/models-recipes/score/configuration.png)

Revise e confirme as configurações de pontuação e selecione **[!UICONTROL Concluir]** para criar e executar a execução de pontuação. Você será direcionado para a guia **[!UICONTROL Execuções de Pontuação]** e a nova execução de pontuação com o status **[!UICONTROL Pendente]** será exibida.

![guia de execuções de pontuação](../images/models-recipes/score/scoring_runs_tab.png)

Uma execução de pontuação pode ser exibida com um dos seguintes status:
- Pending
- Concluído
- Com falha
- Executando

Os status são atualizados automaticamente. Vá para a próxima etapa se o status for **[!UICONTROL Concluído]** ou **[!UICONTROL Falha]**.

## resultados de pontuação Exibir

Para visualização pontuação de resultados, start selecionando uma treinamento corrida.

![Selecionar treinamento execução](../images/models-recipes/score/select-run.png)

Você é redirecionado para a página de execuções de treinamento **[!UICONTROL Avaliação]**. Próximo à parte superior da página de avaliação da execução de treinamento, selecione a guia **[!UICONTROL Execuções de Pontuação]** para exibir uma lista de execuções de pontuação existentes.

![página de avaliação](../images/models-recipes/score/view_scoring_runs.png)

Em seguida, selecione uma execução de pontuação para exibir os detalhes da execução.

![detalhes da execução](../images/models-recipes/score/view_details.png)

Se a execução de pontuação selecionada tiver um status de &quot;Concluído&quot; ou &quot;Falha&quot;, o link **[!UICONTROL Exibir Logs de Atividade]** será disponibilizado. Se uma execução de pontuação falhar, os logs de execução podem fornecer informações úteis para determinar o motivo da falha. Para baixar os logs de execução, selecione **[!UICONTROL Exibir Logs de Atividades]**.

![Selecionar logs de exibição](../images/models-recipes/score/view_logs.png)

O popover **[!UICONTROL Exibir logs de atividades]** é exibido. Selecione um URL para baixar automaticamente os logs associados.

![](../images/models-recipes/score/activity_logs.png)

Você também tem a opção de exibir seus resultados de pontuação selecionando **[!UICONTROL Visualizar conjunto de dados de resultados de pontuação]**.

![Selecionar resultados da visualização](../images/models-recipes/score/view_results.png)

É fornecida uma pré-visualização do conjunto de dados de saída.

![visualizar resultados](../images/models-recipes/score/preview_results.png)

Para o conjunto completo de resultados de pontuação, selecione o link **[!UICONTROL Conjunto de Dados de Resultados de Pontuação]**, localizado na coluna direita.

## Próximas etapas

Isso tutorial o orientaram pelas etapas de pontuação de dados usando um modelo treinado em [!DNL Data Science Workspace]. Siga o tutorial na [publicação de um modelo como um serviço no interface](./publish-model-service-ui.md) para permitir que os usuários de sua organização marquem dados, fornecendo fácil acesso a um Serviço de aprendizado de máquina.
