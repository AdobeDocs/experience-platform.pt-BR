---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics;ui;scoring run;scoring results
solution: Experience Platform
title: Pontuação de um modelo (IU)
topic: Tutorial
description: 'A pontuação na Adobe Experience Platform Data Science Workspace pode ser alcançada ao alimentar dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizáveis em um conjunto de dados de saída especificado como um novo lote. '
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---


# Pontuação de um modelo (IU)

A pontuação no Adobe Experience Platform [!DNL Data Science Workspace] pode ser alcançada com a alimentação de dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizáveis em um conjunto de dados de saída especificado como um novo lote.

Este tutorial demonstra as etapas necessárias para marcar um Modelo na interface do [!DNL Data Science Workspace] usuário.

## Introdução

Para concluir este tutorial, é necessário ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de prosseguir.

Este tutorial requer um Modelo treinado. Se você não tiver um Modelo treinado, siga o [trem e avalie um Modelo no tutorial da interface do usuário](./train-evaluate-model-ui.md) antes de continuar.

## Criar uma nova execução de pontuação

Uma execução de pontuação é criada usando configurações otimizadas de uma execução de treinamento previamente concluída e avaliada. O conjunto de configurações ideais para um Modelo geralmente é determinado pela análise das métricas de avaliação da execução do treinamento.

1. Encontre a execução de treinamento mais ideal para usar suas configurações para pontuação. Abra a execução de treinamento desejada clicando em seu nome.

2. Na guia Training Run **[!UICONTROL Evaluation]** (Avaliação **[!UICONTROL de execução de treinamento), clique no botão]** Score(Pontuação) na parte superior direita da tela. Isso iniciará um novo fluxo de trabalho *Executar Pontuação* .
   ![](../images/models-recipes/score/training_run_overview.png)

3. Selecione o conjunto de dados de pontuação de entrada e clique em **[!UICONTROL Avançar]**.
   ![](../images/models-recipes/score/scoring_input.png)

4. Selecione o conjunto de dados de pontuação de saída, este é o conjunto de dados de saída dedicado no qual os resultados de pontuação são armazenados. Confirme sua seleção e clique em **[!UICONTROL Avançar]**.
   ![](../images/models-recipes/score/scoring_results.png)

5. A etapa final do fluxo de trabalho solicita que você configure sua execução de pontuação. Essas configurações são usadas pelo Modelo para a execução de pontuação.
Observe que não será possível remover parâmetros herdados que foram definidos durante a criação do Modelo. Você pode editar ou reverter parâmetros não herdados clicando no duplo ou clicando no ícone reverter ao passar o mouse sobre a entrada.
   ![](../images/models-recipes/score/configuration.png)
Revise e confirme as configurações de pontuação e clique em **[!UICONTROL Concluir]** para criar e executar a execução da pontuação. Você será direcionado para a guia Execuções de **[!UICONTROL Pontuação]** e a nova execução de pontuação mostrará um status.
   ![](../images/models-recipes/score/scoring_runs_tab.png)
Uma execução de pontuação exibirá um dos quatro status a seguir: Pendente, Concluído, Falha ou Em Execução e são atualizados automaticamente. Vá para a próxima etapa se o status for &quot;Concluído&quot; ou &quot;Falha&quot;.

## Resultados da pontuação da visualização

1. Encontre a execução de treinamento que foi usada para a execução de pontuação e clique no nome para visualização na página **[!UICONTROL Avaliação]** .

2. Próximo à parte superior da página de avaliação da execução de treinamento, clique na guia **[!UICONTROL Execuções]** de Pontuação para visualização de uma lista de execuções de pontuação existentes. Clique na lista de pontuação para visualização dos detalhes na coluna direita.
   ![](../images/models-recipes/score/view_details.png)

3. Se a execução de pontuação selecionada tiver um status &quot;Concluído&quot; ou &quot;Falha&quot;, o link Logs **[!UICONTROL de Atividade de]** Visualização encontrado na coluna direita estará ativo. Clique no link para visualização ou baixe os registros de execução. Se uma execução de pontuação falhou, os logs de execução podem fornecer informações úteis para determinar o motivo da falha.
   ![](../images/models-recipes/score/activity_logs.png)

4. Clique no link Conjunto de Dados **[!UICONTROL de Resultados da Pontuação de]** Pré-visualização encontrado na coluna direita. Você poderá ver uma pré-visualização do conjunto de dados de saída da execução de pontuação.
   ![](../images/models-recipes/score/preview_results.png)

5. Para obter o conjunto completo de resultados de pontuação, clique no link **[!UICONTROL Scoring Results Dataset]** encontrado na coluna direita.

## Próximas etapas

Este tutorial o orientou pelas etapas para pontuar dados usando um Modelo treinado em [!DNL Data Science Workspace]. Siga o tutorial sobre como [publicar um modelo como um serviço na interface do usuário](./publish-model-service-ui.md) para permitir que os usuários em sua organização pontuem dados fornecendo acesso fácil a um serviço de aprendizado de máquina.
