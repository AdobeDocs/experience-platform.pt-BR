---
keywords: Experience Platform;treinar e avaliar;Data Science Workspace;tópicos populares;criar um modelo;criar uma execução de treinamento
solution: Experience Platform
title: Treinar e avaliar um modelo na interface do usuário do Espaço de trabalho de ciência de dados
type: Tutorial
description: No Espaço de trabalho de ciência de dados do Adobe Experience Platform, um modelo de aprendizado de máquina é criado ao incorporar uma fórmula existente que é apropriada para a intenção do modelo. O modelo é então treinado e avaliado para otimizar sua eficiência operacional e eficácia ajustando seus Hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e personalizados para fins específicos com uma única Fórmula.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Treinar e avaliar um modelo na interface do usuário do Espaço de trabalho de ciência de dados

No Espaço de trabalho de ciência de dados do Adobe Experience Platform, um modelo de aprendizado de máquina é criado ao incorporar uma fórmula existente que é apropriada para a intenção do modelo. O modelo é então treinado e avaliado para otimizar sua eficiência operacional e eficácia ajustando seus Hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e personalizados para fins específicos com uma única Fórmula.

Este tutorial percorre as etapas para criar, treinar e avaliar um Modelo.

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar.

Este tutorial requer uma fórmula existente. Se você não tiver uma fórmula, siga as instruções [Importar uma fórmula empacotada na interface do usuário](./import-packaged-recipe-ui.md) tutorial antes de continuar.

## Criar um modelo

No Experience Platform, selecione a variável **[!UICONTROL Modelos]** localizada na navegação à esquerda e, em seguida, selecione a guia procurar para visualizar seus Modelos existentes. Selecionar **[!UICONTROL Criar modelo]** Próximo à parte superior direita da página para iniciar um processo de criação de Modelo.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Navegue pela lista de receitas existentes, localize e selecione a fórmula a ser usada para criar o modelo e selecione **[!UICONTROL Próxima]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Selecione um conjunto de dados de entrada apropriado e selecione **[!UICONTROL Próxima]**. Isso definirá o conjunto de dados de treinamento de entrada padrão para o Modelo.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Forneça um nome para o Modelo e revise as configurações padrão do Modelo. As configurações padrão foram aplicadas durante a criação da fórmula, revise e modifique os valores de configuração clicando duas vezes nos valores.

Para fornecer um novo conjunto de configurações, selecione **[!UICONTROL Carregar nova configuração]** e arraste um arquivo JSON contendo configurações de modelo para a janela do navegador. Selecionar **[!UICONTROL Concluir]** para criar o Modelo.

>[!NOTE]
>
>As configurações são exclusivas e específicas para a fórmula desejada. Isso significa que as configurações para a fórmula de vendas de varejo não funcionarão para a fórmula do Recommendations do produto. Consulte a [referência](#reference) seção para obter uma lista de configurações de Receita de Vendas de Varejo.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Criar uma execução de treinamento

No Experience Platform, selecione a variável **[!UICONTROL Modelos]** localizada na navegação à esquerda e, em seguida, selecione a guia procurar para visualizar seus Modelos existentes. Localize e selecione o hiperlink anexado ao nome do Modelo que deseja treinar.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Todas as execuções de treinamento existentes com seus status de treinamento atuais são listadas. Para modelos criados usando o [!DNL Data Science Workspace] uma execução de treinamento é gerada e executada automaticamente usando as configurações padrão e o conjunto de dados de treinamento de entrada.

Crie uma nova execução de treinamento selecionando **[!UICONTROL Treinamento]** próximo à parte superior direita da página Visão geral do modelo.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Selecione o conjunto de dados de entrada de treinamento para a execução de treinamento e selecione **[!UICONTROL Próxima]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

As configurações padrão fornecidas durante a criação do Modelo são mostradas, alteradas e modificadas de acordo clicando duas vezes nos valores. Selecionar **[!UICONTROL Concluir]** para criar e executar o treinamento.

>[!NOTE]
>
>As configurações são exclusivas e específicas para a fórmula desejada. Isso significa que as configurações para a fórmula de vendas de varejo não funcionarão para a fórmula do Recommendations do produto. Consulte a [referência](#reference) seção para obter uma lista de configurações de Receita de Vendas de Varejo.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Avaliar o modelo

No Experience Platform, selecione a variável **[!UICONTROL Modelos]** localizada na navegação à esquerda e, em seguida, selecione a guia procurar para visualizar seus Modelos existentes. Localize e selecione o hiperlink anexado ao nome do Modelo que deseja avaliar.

![selecionar modelo](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Todas as execuções de treinamento existentes com seus status de treinamento atuais são listadas. Com várias execuções de treinamento concluídas, as métricas de avaliação podem ser comparadas entre diferentes execuções de treinamento no gráfico Avaliação de modelo. Selecione uma métrica de avaliação usando a lista suspensa acima do gráfico.

A métrica Erro Percentual Absoluto Médio (MAPE) expressa a precisão como uma porcentagem do erro. Isso é usado para identificar o experimento com melhor desempenho. Quanto mais baixo o MAPE, melhor.

![visão geral das execuções de treinamento](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

A métrica &quot;Precisão&quot; descreve a porcentagem de Instâncias relevantes em comparação com o total *recuperado* Instâncias. A precisão pode ser vista como a probabilidade de um resultado selecionado aleatoriamente estar correto.

![execução de várias execuções](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Selecionar uma execução de treinamento específica fornece os detalhes dessa execução abrindo a página de avaliação. Isso pode ser feito antes mesmo da execução ser concluída. Na página de avaliação, é possível ver outras métricas de avaliação, parâmetros de configuração e visualizações específicas para a execução do treinamento.

![visualizar logs](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Você também pode baixar logs de atividades para ver os detalhes da execução. Os logs são particularmente úteis para execuções com falha para ver o que deu errado.

![logs de atividades](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hiperparâmetros não podem ser treinados e um modelo deve ser otimizado testando combinações diferentes de Hiperparâmetros. Repita este processo de treinamento e avaliação do modelo até chegar a um modelo otimizado.

## Próximas etapas

Este tutorial guiou você pela criação, treinamento e avaliação de um Modelo no [!DNL Data Science Workspace]. Depois de chegar a um modelo otimizado, você pode usar o modelo treinado para gerar insights seguindo o [Pontuação de um modelo na interface do](./score-model-ui.md) tutorial.

## Referência {#reference}

### Configurações de Receita de Venda de Varejo

Os hiperparâmetros determinam o comportamento de treinamento do modelo. Modificar os hiperparâmetros afetará a precisão e a precisão do modelo:

| Hiperparâmetro | Descrição | Intervalo recomendado |
| --- | --- | --- |
| learning_rate | A taxa de aprendizado reduz a contribuição de cada árvore por learning_rate. Há uma compensação entre learning_rate e n_estimators. | 0.1 |
| n_estimadores | O número de estágios de reforço a serem executados. O aumento de gradiente é bastante robusto para ajuste excessivo, de modo que um número grande geralmente resulta em melhor desempenho. | 100 |
| max_depth | Profundidade máxima dos estimadores de regressão individuais. A profundidade máxima limita o número de nós na árvore. Ajuste esse parâmetro para obter o melhor desempenho; o melhor valor depende da interação das variáveis de entrada. | 3 |

Parâmetros adicionais determinam as propriedades técnicas do modelo:

| Chave de parâmetro | Tipo | Descrição |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | String | Lista de atributos de esquema de entrada separados por vírgula. |
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de esquema de saída separados por vírgulas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída são modificáveis |
| `tenantId` | String | Essa ID garante que os recursos criados tenham o namespace adequado e estejam contidos na Organização IMS. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar sua ID de locatário. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | O esquema de entrada usado para treinar um Modelo. |
| `evaluation.labelColumn` | String | Rótulo da coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O esquema de saída usado para pontuar um Modelo. |
