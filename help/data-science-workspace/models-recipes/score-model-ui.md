---
keywords: Experience Platform;pontuação de um modelo;Data Science Workspace;tópicos populares;iu;pontuação executar;pontuação resultados
solution: Experience Platform
title: Pontuar um modelo na interface do Espaço de trabalho de ciência de dados
type: Tutorial
description: A pontuação no Espaço de trabalho de ciência de dados da Adobe Experience Platform pode ser obtida ao alimentar dados de entrada em um modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---

# Pontuar um modelo na interface do Espaço de trabalho de ciência de dados

Pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser obtida alimentando dados de entrada em um modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.

Este tutorial demonstra as etapas necessárias para pontuar um Modelo na [!DNL Data Science Workspace] interface do usuário.

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar.

Este tutorial requer um modelo treinado. Se você não tiver um Modelo treinado, siga as instruções [treinar e avaliar um modelo na interface do usuário](./train-evaluate-model-ui.md) tutorial antes de continuar.

## Criar uma nova execução de pontuação

Uma execução de pontuação é criada usando configurações otimizadas de uma execução de treinamento concluída e avaliada anteriormente. O conjunto de configurações ideais para um Modelo é normalmente determinado pela revisão das métricas de avaliação da execução de treinamento.

Encontre o melhor treinamento executado para usar suas configurações para pontuação. Em seguida, abra a execução de treinamento desejada selecionando o hiperlink anexado ao seu nome.

![Selecionar execução de treinamento](../images/models-recipes/score/select-run.png)

A partir da execução do treinamento **[!UICONTROL Avaliação]** selecione **[!UICONTROL Pontuação]** localizado na parte superior direita da tela. Um novo fluxo de trabalho de pontuação é iniciado.

![](../images/models-recipes/score/training_run_overview.png)

Selecione o conjunto de dados de pontuação de entrada e selecione **[!UICONTROL Próxima]**.

![](../images/models-recipes/score/scoring_input.png)

Selecione o conjunto de dados de pontuação de saída, esse é o conjunto de dados de saída dedicado em que os resultados da pontuação são armazenados. Confirme a seleção e selecione **[!UICONTROL Próxima]**.

![](../images/models-recipes/score/scoring_results.png)

A etapa final no fluxo de trabalho solicita que você configure a execução de pontuação. Essas configurações são usadas pelo modelo para a execução de pontuação.
Observe que não é possível remover parâmetros herdados que foram definidos durante a criação dos modelos. Você pode editar ou reverter parâmetros não herdados clicando duas vezes no valor ou selecionando o ícone de reversão enquanto passa o mouse sobre a entrada.

![configuração](../images/models-recipes/score/configuration.png)

Revise e confirme as configurações de pontuação e selecione **[!UICONTROL Concluir]**  para criar e executar a execução de pontuação. Você é direcionado para o **[!UICONTROL Execuções de Pontuação]** e a nova execução de pontuação com o **[!UICONTROL Pending]** O status é exibido.

![guia execuções de pontuação](../images/models-recipes/score/scoring_runs_tab.png)

Uma execução de pontuação pode ser exibida com um dos seguintes status:
- Pending
- Concluir
- Falha
- Executando

Os status são atualizados automaticamente. Vá para a próxima etapa se o status for **[!UICONTROL Concluído]** ou **[!UICONTROL Failed]**.

## Exibir resultados de pontuação

Para exibir os resultados da pontuação, comece selecionando uma execução de treinamento.

![Selecionar execução de treinamento](../images/models-recipes/score/select-run.png)

Você é redirecionado para as execuções de treinamento **[!UICONTROL Avaliação]** página. Próximo à parte superior da página de avaliação da execução de treinamento, selecione a **[!UICONTROL Execuções de Pontuação]** para exibir uma lista de execuções de pontuação existentes.

![página de avaliação](../images/models-recipes/score/view_scoring_runs.png)

Em seguida, selecione uma execução de pontuação para exibir os detalhes da execução.

![detalhes da execução](../images/models-recipes/score/view_details.png)

Se a execução de pontuação selecionada tiver um status &quot;Concluído&quot; ou &quot;Falha&quot;, a variável **[!UICONTROL Exibir logs de atividades]** é disponibilizado. Se uma execução de pontuação falhar, os logs de execução podem fornecer informações úteis para determinar o motivo da falha. Para baixar os logs de execução, selecione **[!UICONTROL Exibir logs de atividades]**.

![Selecionar exibir logs](../images/models-recipes/score/view_logs.png)

A variável **[!UICONTROL Exibir logs de atividades]** popover é exibido. Selecione um URL para baixar automaticamente os logs associados.

![](../images/models-recipes/score/activity_logs.png)

Você também tem a opção de exibir os resultados da pontuação selecionando  **[!UICONTROL Visualizar conjunto de dados de resultados da pontuação]**.

![Selecionar resultados da visualização](../images/models-recipes/score/view_results.png)

É fornecida uma pré-visualização do conjunto de dados de saída.

![visualizar resultados](../images/models-recipes/score/preview_results.png)

Para obter o conjunto completo de resultados de pontuação, selecione o **[!UICONTROL Conjunto de dados de resultados da pontuação]** link encontrado na coluna à direita.

## Próximas etapas

Este tutorial guiou você pelas etapas para pontuar dados usando um Modelo treinado no [!DNL Data Science Workspace]. Siga o tutorial em [publicação de um Modelo como um serviço na interface](./publish-model-service-ui.md) para permitir que os usuários em sua organização pontuem dados fornecendo acesso fácil a um Serviço de aprendizado de máquina.
