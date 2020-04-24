---
keywords: Experience Platform;machine learning model;Data Science Workspace;popular topics
solution: Experience Platform
title: Criar e publicar uma apresentação de modelo de aprendizado de máquina
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Criar e publicar uma apresentação de modelo de aprendizado de máquina

![](../images/models-recipes/model-walkthrough/objective.png)

Fingir que você possui um site de varejo online. Quando seus clientes fazem compras em seu site de varejo, você deseja apresentar a eles recomendações personalizadas de produtos para expor uma variedade de outros produtos suas ofertas comerciais. Durante a existência de seu site, você coletou continuamente os dados do cliente e deseja, de alguma forma, usar esses dados para gerar recomendações personalizadas de produtos.

A Adobe Experience Platform Data Science Workspace fornece os meios para atingir sua meta usando a Receita [de recomendações de](../pre-built-recipes/product-recommendations.md)produto pré-criada. Siga este tutorial para ver como você pode acessar e entender seus dados de varejo, criar e otimizar um Modelo de aprendizado de máquina e gerar insights na Data Science Workspace.

Este tutorial reflete o fluxo de trabalho da Data Science Workspace e aborda as seguintes etapas para criar um Modelo de aprendizado de máquina:

1. [Preparar seus dados](#prepare-your-data)
2. [Criar seu modelo](#author-your-model)
3. [Treinar e avaliar seu modelo](#train-and-evaluate-your-model)
4. [Operacionalizar seu modelo](#operationalize-your-model)

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:

* Acesso à Adobe Experience Platform. Se você não tiver acesso a uma organização IMS na plataforma Experience, fale com o administrador do sistema antes de prosseguir.

* Ativar ativos. Entre em contato com seu representante de conta para obter os seguintes itens fornecidos para você.
   * Receita de recomendações
   * Conjunto de dados de entrada do Recommendations
   * Schema de entrada do Recommendations
   * Conjunto de dados de saída do Recommendations
   * Schema de saída do Recommendations
   * PostValues do conjunto de dados dourados
   * Schema do conjunto de dados Golden

* Baixe os três arquivos necessários do Notebook Jupyter do repositório <a href="https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources/Notebooks-Thurs" target="_blank">público Git da</a>Adobe, eles serão usados para demonstrar o fluxo de trabalho do JupyterLab na Data Science Workspace.

* Um entendimento prático dos seguintes conceitos-chave usados neste tutorial:
   * [Modelo](../../xdm/home.md)de dados da experiência: O esforço de padronização realizado pela Adobe para definir schemas padrão, como Perfil e ExperienceEvent, para o Gerenciamento de experiência do cliente.
   * Conjuntos de dados: Uma construção de armazenamento e gerenciamento para dados reais. Uma instância física instanciada de um Schema [](../../xdm/schema/field-dictionary.md)XDM.
   * Lotes: Os conjuntos de dados são compostos de lotes. Um lote é um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade.
   * JupyterLab: O [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) é uma interface baseada na Web de código aberto para o Project Júpitter e é totalmente integrado à plataforma Experience.

## Preparar seus dados {#prepare-your-data}

Para criar um Modelo de aprendizado de máquina que faça recomendações personalizadas de produto para seus clientes, as compras anteriores de clientes em seu site devem ser analisadas. Esta seção explora como esses dados são ingeridos na Plataforma pelo Adobe Analytics e como eles são transformados em um conjunto de dados de recursos a ser usado pelo Modelo de aprendizado da máquina.

### Explore os dados e entenda os schemas

1. Faça logon na [Adobe Experience Platform](https://platform.adobe.com/) e clique em **Conjuntos** de dados para lista de todos os conjuntos de dados existentes e selecione o conjunto de dados que deseja explorar. Nesse caso, o conjunto de dados do Analytics **Golden Data Set postValues**.
   ![](../images/models-recipes/model-walkthrough/datasets_110.png)
2. Selecione Conjunto de dados de **Pré-visualização** próximo à parte superior direita para examinar os registros de amostra e clique em **Fechar**.
   ![](../images/models-recipes/model-walkthrough/golden_data_set_110.png)
3. Selecione o link em Schema no painel direito para visualização do schema do conjunto de dados e, em seguida, retorne à página de detalhes do conjunto de dados.&quot;
   ![](../images/models-recipes/model-walkthrough/golden_schema_110.png)

Os outros conjuntos de dados foram pré-preenchidos com lotes para fins de visualização. É possível visualização desses conjuntos de dados repetindo as etapas acima.

| Nome do conjunto de dados | Schema | Descrição |
| ----- | ----- | ----- |
| PostValues do conjunto de dados dourados | schema do conjunto de dados Golden | Dados de origem do Analytics do seu site |
| Conjunto de dados de entrada do Recommendations | Schema de entrada do Recommendations | Os dados do Analytics são transformados em um conjunto de dados de treinamento usando um pipeline de recursos. Esses dados são usados para treinar o Modelo de aprendizado da máquina do Product Recommendations. `itemid` e `userid` correspondem a um produto comprado por esse cliente. |
| Conjunto de dados de saída do Recommendations | Schema de saída do Recommendations | O conjunto de dados para o qual os resultados da pontuação são armazenados, conterá a lista de produtos recomendados para cada cliente. |

## Criar seu modelo {#author-your-model}

O segundo componente do ciclo de vida da Data Science Workspace envolve a criação de Fórmulas e Modelos. A Receita de recomendações de produto foi projetada para gerar recomendações de produto em escala utilizando dados de compra anteriores e aprendizado de máquina.

As receitas são a base para um Modelo, pois contêm algoritmos de aprendizado de máquina e lógica projetada para resolver problemas específicos. O mais importante é que as Fórmulas permitem que você democratize o aprendizado de máquina em toda a sua organização, permitindo que outros usuários acessem um Modelo para casos de uso diferentes sem gravar nenhum código.

### Explore a receita das recomendações do produto

1. Na plataforma Adobe Experience, navegue até **Modelos** na coluna de navegação esquerda e clique em **Receitas** na parte superior para visualização de uma lista de Receitas disponíveis para sua organização.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Localize e abra a Receita **do** Recommendations fornecida clicando em seu nome.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. No painel direito, clique em Schema **de entrada do** Recommendations para visualização no schema que alimenta a receita. Os campos de schema **itemId** e **userId** correspondem a um produto comprado (**integrationType**) por esse cliente em um horário específico (**carimbo de data e hora**). Siga as mesmas etapas para revisar os campos do Schema **de Saída do**Recommendations.
   ![](../images/models-recipes/model-walkthrough/preview_schemas.png)

Agora você revisou os schemas de entrada e saída exigidos pela Receita do Recommendations do Produto. Agora você pode continuar para a próxima seção para descobrir como criar, treinar e avaliar um Modelo de recomendações de produto.

## Treinar e avaliar seu modelo {#train-and-evaluate-your-model}

Agora que seus dados estão preparados e a Receita está pronta para ser usada, você pode criar, treinar e avaliar seu Modelo de aprendizado da máquina.

### Criar um modelo

Um Modelo é uma instância de uma Receita, permitindo que você treine e classifique com dados em escala.

1. Na plataforma Adobe Experience, navegue até **Modelos** na coluna de navegação esquerda e clique em **Fórmulas** na parte superior da página para exibir uma lista de todas as Fórmulas disponíveis para sua organização.
   ![](../images/models-recipes/model-walkthrough/browse_recipes.png)
2. Localize e abra a Receita **do** Recommendations fornecida clicando em seu nome, inserindo a página de visão geral da Receita. Clique em **Criar um modelo** no centro (se não houver Modelos existentes) ou no canto superior direito da página Visão geral da receita.
   ![](../images/models-recipes/model-walkthrough/recommendations_recipe_110.png)
3. Uma lista de conjuntos de dados de entrada disponíveis para treinamento é mostrada, selecione Conjunto de dados **de entrada do** Recommendations e clique em **Avançar**.
   ![](../images/models-recipes/model-walkthrough/select_dataset.png)
4. Forneça um nome para o Modelo, por exemplo, &quot;Modelo de recomendações do produto&quot;. As configurações disponíveis para o modelo são listadas, contendo as configurações para o treinamento padrão do Modelo e os comportamentos de pontuação. Nenhuma alteração é necessária, pois essas configurações são específicas da sua organização. Revise as configurações e clique em **Concluir**.
   ![](../images/models-recipes/model-walkthrough/configure_model.png)
5. O Modelo foi criado e a página *Visão geral* do Modelo é exibida em uma execução de treinamento recém-gerada. Uma execução de treinamento é gerada por padrão quando um Modelo é criado.
   ![](../images/models-recipes/model-walkthrough/model_post_creation.png)

Você pode optar por aguardar a conclusão da execução do treinamento ou continuar a criar uma nova execução de treinamento na seção a seguir.

### Treinar o modelo usando hiperparâmetros personalizados

1. Na página Visão geral *do* modelo, clique em **Treinar** perto da parte superior direita para criar uma nova execução de treinamento. Selecione o mesmo conjunto de dados de entrada que você usou ao criar o Modelo e clique em **Avançar**.
   ![](../images/models-recipes/model-walkthrough/training_select_dataset.png)
2. A página *Configuração* é exibida. Aqui você pode configurar o valor **num_Recomendações** da execução de treinamento, também conhecido como um Hiperparâmetro. Um Modelo treinado e otimizado utilizará os hiperparâmetros de melhor desempenho com base nos resultados da execução do treinamento.

   Hiperparâmetros não podem ser aprendidos, portanto, eles devem ser atribuídos antes que as execuções de treinamento ocorram. Ajustar hiperparâmetros pode alterar a precisão do modelo treinado. Como a otimização de um modelo é um processo iterativo, podem ser necessárias várias execuções de treinamento antes de se obter uma avaliação satisfatória.

   >[!TIP] Defina **num_Recomendações** como 10.

   ![](../images/models-recipes/model-walkthrough/configure_hyperparameter.png)
3. Um ponto de dados adicional aparecerá no gráfico de avaliação de Modelo quando a nova execução de treinamento for concluída, isso pode levar vários minutos.
   ![](../images/models-recipes/model-walkthrough/post_training_run.png)

### Avaliar o modelo

Sempre que uma execução de treinamento for concluída, você poderá visualização as métricas de avaliação resultantes para determinar o desempenho do Modelo.

1. Analise as métricas de avaliação (Precisão e Chamada) para cada execução de treinamento concluída clicando em na execução de treinamento.
2. Explore as informações fornecidas para cada métrica de avaliação. Quanto maior for a métrica, melhor será o desempenho do Modelo.
   ![](../images/models-recipes/model-walkthrough/evaluation_metrics.png)
3. Você pode ver o conjunto de dados, o schema e os parâmetros de configuração usados para cada execução de treinamento no painel direito.
4. Navegue até a página Modelo e identifique a execução de treinamento de melhor desempenho observando suas métricas de avaliação.

## Operacionalizar seu modelo {#operationalize-your-model}

A etapa final do fluxo de trabalho da Data Science é operacionalizar seu modelo para pontuar e consumir insights de seu armazenamento de dados.

### Pontuação e geração de insights

1. Na página *Visão geral* do modelo de recomendações de produto, clique no nome da execução de treinamento com melhor desempenho, com os valores mais altos de recuperação e precisão.
2. Na parte superior direita da página de detalhes da execução do treinamento, clique em **Pontuação**.
3. Selecione o Conjunto de Dados **de Entrada do** Recommendations como o conjunto de dados de entrada de pontuação, que é o mesmo conjunto de dados usado ao criar o Modelo e executar suas execuções de treinamento. Then, click **Next**.
   ![](../images/models-recipes/model-walkthrough/scoring_input.png)
4. Selecione o Conjunto de Dados **de Saída do** Recommendations como o conjunto de dados de saída de pontuação. Os resultados da pontuação serão armazenados neste conjunto de dados como um lote.
   ![](../images/models-recipes/model-walkthrough/scoring_output.png)
5. Revise as configurações de pontuação. Esses parâmetros contêm os conjuntos de dados de entrada e saída selecionados anteriormente, juntamente com os schemas apropriados. Clique em **Concluir** para iniciar a execução da pontuação. A execução pode levar vários minutos para ser concluída.
   ![](../images/models-recipes/model-walkthrough/scoring_configure.png)


### insights pontuados pela Visualização

Depois que a execução da pontuação for concluída com êxito, você poderá pré-visualização os resultados e visualização os insights gerados.

1. Na página de execuções de pontuação, clique na execução de pontuação concluída e, em seguida, clique em Conjunto de Dados **de Resultados de Pontuação de** Pré-visualização no painel direito.
   ![](../images/models-recipes/model-walkthrough/score_complete.png)
2. Na tabela pré-visualização, cada linha contém recomendações de produto para um cliente específico, rotuladas como **recomendações** e **userId** , respectivamente. Como o **hiperparâmetro num_Recomendações** foi definido como 10 nas capturas de tela de amostra, cada linha de recomendações pode conter até 10 identidades de produto delimitadas por um sinal de número (#).
   ![](../images/models-recipes/model-walkthrough/preview_score_results.png)

Muito bem, vocês geraram com sucesso recomendações de produtos!

Este tutorial apresentou você ao fluxo de trabalho da Data Science Workspace, demonstrando como os dados brutos não processados podem ser transformados em informações úteis por meio do aprendizado de máquina. Para saber mais sobre como usar a Data Science Workspace, continue com o próximo guia sobre como [criar o schema de vendas e o conjunto de dados](./create-retails-sales-dataset.md)de varejo.