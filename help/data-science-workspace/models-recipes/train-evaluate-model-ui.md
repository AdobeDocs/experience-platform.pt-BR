---
keywords: Experience Platform;treinar e avaliar;Data Science Workspace;tópicos populares;criar um modelo;criar uma execução de treinamento
solution: Experience Platform
title: Treinar e avaliar um modelo na interface do usuário do Data Science Workspace
type: Tutorial
description: No Adobe Experience Platform Data Science Workspace, um modelo de aprendizado de máquina é criado ao incorporar uma fórmula existente que é apropriada à intenção do modelo. O modelo é então treinado e avaliado para otimizar sua eficiência operacional e eficácia ajustando seus Hiperparâmetros associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e personalizados para fins específicos com uma única Fórmula.
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# Treinar e avaliar um modelo na interface do usuário do Data Science Workspace

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

No Adobe Experience Platform Data Science Área de trabalho, um Modelo de aprendizagem de máquina é criado incorporando uma Receita existente que é apropriada para a intenção do Modelo. O modelo é então treinado e avaliado para otimizar sua eficiência operacional e eficácia, ajustando seus hiperparameters associados. As receitas são reutilizáveis, o que significa que vários Modelos podem ser criados e adaptados a propósitos específicos com uma única receita.

Este tutorial percorre as etapas para criar, treinar e avaliar um Modelo.

## Introdução

No solicitar para concluir esta tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Esta tutorial requer uma Receita existente. Se você não tiver uma Receita, seguir a [Importar uma Receita embalada na interface](./import-packaged-recipe-ui.md) tutorial antes de continuar.

## Criar um modelo

Em Experience Platform, selecione os **[!UICONTROL Modelos]** guia localizados na navegação esquerda e selecione a guia de navegação para visualização seus Modelos existentes. Selecione **[!UICONTROL Criar modelo]** próximo à parte superior direita da página para iniciar um processo de criação de modelo.

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

Navegue pela lista de Receitas existentes, localize e selecione a Receita a ser usada para criar o Modelo e selecione **[!UICONTROL Próximo]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

Selecione um conjunto de dados de entrada apropriado e selecione **[!UICONTROL Próximo]**. Isso definirá o conjunto de dados de treinamento de entrada padrão para o Modelo.
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

Forneça um nome para o Modelo e revise as configurações padrão do Modelo. As configurações padrão foram aplicadas durante a criação da fórmula, revise e modifique os valores de configuração clicando duas vezes nos valores.

Para fornecer um novo conjunto de configurações, selecione **[!UICONTROL Carregar nova configuração]** e arraste um arquivo JSON contendo configurações de modelo para a janela do navegador. Selecione **[!UICONTROL Concluir]** para criar o modelo.

>[!NOTE]
>
>As configurações são exclusivas e específicas para a fórmula desejada. Isso significa que as configurações para a fórmula de vendas de varejo não funcionarão para a fórmula do Recommendations do produto. Consulte a seção [reference](#reference) para obter uma lista de configurações de receitas de vendas de varejo.

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## Criar uma execução de treinamento

No Experience Platform, selecione a guia **[!UICONTROL Modelos]**, localizada na navegação à esquerda, e selecione a guia Procurar para exibir seus Modelos existentes. Localize e selecione o hiperlink anexado ao nome do Modelo que deseja treinar.

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Todas as execuções de treinamento existentes com seus status de treinamento atuais são listadas. Para modelos criados usando a interface do [!DNL Data Science Workspace] usuário, uma treinamento execução é gerada e executada automaticamente usando as configurações padrão e os treinamento conjunto de dados de entrada.

Criar um novo treinamento executado selecionando **[!UICONTROL Train]** perto do canto superior direito da visão geral do Modelo página.

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

Selecione o treinamento conjunto de dados de entrada para a execução do treinamento e selecione **[!UICONTROL Próximo]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

As configurações padrão fornecidas durante a criação do Modelo são mostradas, alteram e modificá-las adequadamente ao clicar duplo os valores. Selecione **[!UICONTROL Concluir]** para criar e executar a treinamento execução.

>[!NOTE]
>
>Configurações são exclusivas e específicas de sua Receita pretendida, isso significa que as configurações da Receita de Vendas no Varejo não funcionarão para a Receita de recomendações do produto. Consulte a [seção de referência](#reference) para obter uma lista das configurações de Receita de vendas no varejo.

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## Avaliar o modelo

No Experience Platform, selecione a guia **[!UICONTROL Modelos]**, localizada na navegação à esquerda, e selecione a guia Procurar para exibir seus Modelos existentes. Encontre e selecione o hiperlink anexado ao nome do modelo que deseja avaliar.

![selecionar modelo](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

Todas as treinamento existentes são executadas com os status treinamento atuais são listadas. Com várias treinamento corridas concluídas, as métricas de avaliação podem ser comparadas em diferentes treinamento de execução no gráfico de avaliação do Modelo. Selecione uma métrica de avaliação usando a lista suspensa acima do gráfico.

A métrica Erro Percentual Absoluto Médio (MAPE) expressa a precisão como uma porcentagem do erro. Isso é usado para identificar o experimento com melhor desempenho. Quanto mais baixo o MAPE, melhor.

![visão geral das execuções de treinamento](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

A métrica &quot;Precisão&quot; descreve a porcentagem de Instâncias relevantes em comparação com o total de *Instâncias* recuperadas. A precisão pode ser vista como a probabilidade de um resultado selecionado aleatoriamente estar correto.

![executando várias execuções](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

Selecionar uma treinamento execução específica fornece os detalhes da execução abrindo o página de avaliação. Isso pode ser feito antes mesmo da execução ser concluída. Na página de avaliação, é possível ver outras métricas de avaliação, parâmetros de configuração e visualizações específicas para a execução do treinamento.

![visualizar logs](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

Você também pode baixar logs de atividades para ver os detalhes da execução. Os logs são particularmente úteis para execuções com falha para ver o que deu errado.

![logs de atividades](../images/models-recipes/train-evaluate-ui/activity_logs.png)

Hiperparâmetros não podem ser treinados e um modelo deve ser otimizado testando combinações diferentes de Hiperparâmetros. Repita esse processo de treinamento e avaliação de modelo até chegar a um Modelo otimizado.

## Próximas etapas

Isso tutorial o orientava a criar, treinamento e avaliar um modelo em [!DNL Data Science Workspace]. Depois de chegar a um Modelo otimizado, você pode usar o Modelo treinado para gerar insights seguindo a [Pontuação de um Modelo no interface](./score-model-ui.md) tutorial.

## Referência {#reference}

### Configurações de Receita de Venda de Varejo

Os hiperparâmetros determinam o comportamento de treinamento do modelo. Modificar os hiperparâmetros afetará a precisão e a precisão do modelo:

| Hiperparâmetro | Descrição | Intervalo recomendado |
| --- | --- | --- |
| learning_rate | A taxa de aprendizagem reduz em learning_rate a contribuição de cada árvore. Há uma compensação entre learning_rate e n_estimators. | 0,1 |
| n_estimadores | O número de estágios de reforço a serem executados. O aumento de gradiente é bastante robusto para ajuste excessivo, de modo que um número grande geralmente resulta em melhor desempenho. | 100 |
| max_depth | Profundidade máxima dos estimadores de regressão individuais. A profundidade máxima limita o número de nós na árvore. Ajuste este parâmetro para obter o melhor desempenho; o melhor valor depende da interação das variáveis de entrada. | 3 |

Parâmetros adicionais determinam as propriedades técnicas do modelo:

| Chave de parâmetro | Tipo | Descrição |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | String | Lista de entradas separadas por vírgulas schema atributos. |
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de esquema de saída separados por vírgulas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída são modificáveis |
| `tenantId` | String | Essa ID garante que os recursos criados tenham o namespace adequado e estejam contidos na organização. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar sua ID do inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | O esquema de entrada usado para treinar um Modelo. |
| `evaluation.labelColumn` | String | Rótulo da coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista de avaliação separadas por vírgulas a serem usadas para avaliar um modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | A saída schema usada para marcar um Modelo. |
