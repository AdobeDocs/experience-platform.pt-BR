---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics;create a model;create a training run
solution: Experience Platform
title: Treinar e avaliar um modelo (IU)
topic: Tutorial
description: Na Adobe Experience Platform Data Science Workspace, um Modelo de aprendizado de máquina é criado pela incorporação de uma Receita existente adequada à intenção do Modelo. O Modelo é então treinado e avaliado para otimizar sua eficiência e eficiência operacional ajustando seus hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados para fins específicos com uma única Receita.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 2%

---


# Treinar e avaliar um modelo (IU)

Na Adobe Experience Platform Data Science Workspace, um Modelo de aprendizado de máquina é criado pela incorporação de uma Receita existente adequada à intenção do Modelo. O Modelo é então treinado e avaliado para otimizar sua eficiência e eficiência operacional ajustando seus hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados para fins específicos com uma única Receita.

Este tutorial percorre as etapas para criar, treinar e avaliar um Modelo.

## Introdução

Para concluir este tutorial, é necessário ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de prosseguir.

Este tutorial requer uma Receita existente. Se você não tiver uma Receita, siga o tutorial [Importar uma Receita empacotada na interface do usuário](./import-packaged-recipe-ui.md) antes de continuar.

## Criar um modelo

1. No Adobe Experience Platform, clique no link **[!UICONTROL Modelos]** localizado na coluna de navegação esquerda para lista de todos os modelos existentes. Clique em **[!UICONTROL Criar modelo]** próximo à parte superior direita da página para iniciar um processo de criação do modelo.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Navegue pela lista de Receitas existentes, localize e selecione a Receita a ser usada para criar o Modelo e clique em **[!UICONTROL Avançar]**.
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. Selecione um conjunto de dados de entrada apropriado e clique em **[!UICONTROL Avançar]**. Isso definirá o conjunto de dados de treinamento de entrada padrão para o Modelo.
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. Forneça um nome para o Modelo e reveja as configurações padrão do Modelo. As configurações padrão foram aplicadas durante a criação da Receita, a análise e a modificação dos valores de configuração clicando nos valores com o duplo. Para fornecer um novo conjunto de configurações, clique em **[!UICONTROL Carregar nova configuração]** e arraste um arquivo JSON que contém configurações de Modelo para a janela do navegador. Clique em **[!UICONTROL Concluir]** para criar o Modelo.

   >[!NOTE]
   >
   >As configurações são exclusivas e específicas para a Receita pretendida, o que significa que as configurações para a Receita de Vendas de Varejo não funcionarão para a Receita Recommendations do Produto. Consulte a seção de [referência](#reference) para obter uma lista das configurações de Receita de vendas de varejo.

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Criar uma execução de treinamento

1. No Adobe Experience Platform, clique no link **[!UICONTROL Modelos]** localizado na coluna de navegação esquerda para lista de todos os modelos existentes. Localize e clique no nome do Modelo a ser treinado.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Todas as execuções de treinamento existentes com seus status de treinamento atuais são listadas. Para Modelos criados usando a interface do [!DNL Data Science Workspace] usuário, uma execução de treinamento é gerada e executada automaticamente usando as configurações padrão e o conjunto de dados de treinamento de entrada.
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. Crie uma nova execução de treinamento clicando em **[!UICONTROL Treinar]** próximo ao canto superior direito da página de visão geral do Modelo.
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. Selecione o conjunto de dados de entrada de treinamento para a execução de treinamento e clique em **[!UICONTROL Avançar]**.
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. As configurações padrão fornecidas durante a criação do Modelo são mostradas, alteram-as e modificam-nas de acordo, clicando nos valores com o duplo. Clique em **[!UICONTROL Concluir]** para criar e executar a execução do treinamento.

   >[!NOTE]
   >
   >As configurações são exclusivas e específicas para a Receita pretendida, o que significa que as configurações para a Receita de Vendas de Varejo não funcionarão para a Receita Recommendations do Produto. Consulte a seção de [referência](#reference) para obter uma lista das configurações de Receita de vendas de varejo.

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## Avaliar o modelo

1. No Adobe Experience Platform, clique no link **[!UICONTROL Modelos]** localizado na coluna de navegação esquerda para lista de todos os modelos existentes. Localize e clique no nome do Modelo a ser avaliado.
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. Todas as execuções de treinamento existentes com seus status de treinamento atuais são listadas. Com várias execuções de treinamento concluídas, as métricas de avaliação podem ser comparadas em diferentes execuções de treinamento no gráfico de avaliação do Modelo, selecione uma métrica de avaliação usando a lista suspensa acima do gráfico.

   A métrica Erro médio absoluto de porcentagem (MAPE) expressa a precisão como uma porcentagem do erro. Isso é usado para identificar o Experimento de melhor desempenho. Quanto menor a MAPE, melhor.

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   A métrica &quot;Precisão&quot; descreve a porcentagem de Instâncias relevantes comparada ao total de Instâncias *recuperadas* . A precisão pode ser vista como a probabilidade de um resultado selecionado aleatoriamente estar correto.
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   Clique em uma execução de treinamento específica para visualização dos detalhes dessa execução. Isso pode ser feito mesmo antes da execução ser concluída. Na página de detalhes da execução, você pode ver outras métricas de avaliação, parâmetros de configuração e visualizações específicas para a execução do treinamento. Você também pode baixar registros de atividades para ver os detalhes da execução. Os registros são particularmente úteis para execuções com falha para ver o que deu errado.
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. Hiperparâmetros não podem ser treinados e um Modelo deve ser otimizado testando diferentes combinações de Hiperparâmetros. Repita esse processo de treinamento e avaliação do Modelo até chegar a um Modelo otimizado.

## Próximas etapas

Este tutorial o orientou pela criação, treinamento e avaliação de um Modelo em [!DNL Data Science Workspace]. Depois de chegar a um Modelo otimizado, você pode usar o Modelo treinado para gerar insights seguindo a [Pontuação a modelo no tutorial da interface do usuário](./score-model-ui.md) .

## Referência {#reference}

### Configurações de receita de vendas de varejo

Os hiperparâmetros determinam o comportamento de treinamento do Modelo, modificando os hiperparâmetros afetará a precisão e precisão do Modelo:

| Hiperparâmetro | Descrição | Intervalo recomendado |
--- | --- | ---
| learning_rate | A taxa de aprendizado reduz a contribuição de cada árvore por learning_rate. Há uma compensação entre o learning_rate e o n_estimators. | 0.1 | [2 - 10] / número de estimadores |
| n_estimatadores | O número de estágios de inicialização a serem executados. O aumento de gradiente é bastante robusto para ajustar demais, então um grande número geralmente resulta em melhor desempenho. | 100 | 100 - 1000 |
| max_depth | Profundidade máxima dos estimadores de regressão individuais. A profundidade máxima limita o número de nós na árvore. Ajuste esse parâmetro para obter o melhor desempenho; o melhor valor depende da interação das variáveis de entrada. | 3 | 4 - 10 |

Parâmetros adicionais determinam as propriedades técnicas do Modelo:

| Tecla Parameter | Tipo | Descrição |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | String | Lista de atributos de schema de entrada separados por vírgulas. |
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de schema de saída separados por vírgulas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída são modificáveis |
| `tenantId` | String | Essa ID garante que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para localizar sua ID de locatário. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | O schema de entrada usado para treinar um Modelo. |
| `evaluation.labelColumn` | String | Rótulo de coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O schema de saída usado para marcar um Modelo. |