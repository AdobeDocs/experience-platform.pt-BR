---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics;recipes;ui;create engine
solution: Experience Platform
title: Importar uma receita empacotada (IU)
topic: Tutorial
description: Este tutorial fornece informações sobre como configurar e importar uma receita empacotada usando o exemplo de Vendas de Varejo fornecido. Até o final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo na Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 0%

---


# Importar uma receita empacotada (IU)

Este tutorial fornece informações sobre como configurar e importar uma receita empacotada usando o exemplo de Vendas de Varejo fornecido. Até o final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

## Pré-requisitos

Este tutorial requer uma fórmula empacotada na forma de um URL de imagem do Docker. Consulte o tutorial sobre como [agrupar arquivos de origem em uma Receita](./package-source-files-recipe.md) para obter mais informações.

## Fluxo de trabalho da interface

A importação de uma fórmula empacotada para [!DNL Data Science Workspace] requer configurações de fórmula específicas, compiladas em um único arquivo JSON (JavaScript Object Notation), essa compilação de configurações de fórmula é chamada de arquivo **de** configuração. Uma fórmula embalada com um conjunto específico de configurações é chamada de instância **da** fórmula. Uma fórmula pode ser usada para criar várias instâncias de fórmula em [!DNL Data Science Workspace].

O fluxo de trabalho para importar uma fórmula de pacote consiste nas seguintes etapas:
- [Configurar uma fórmula](#configure)
- [Importar fórmula baseada no Docker - Python](#python)
- [Importar fórmula baseada no Docker - R](#r)
- [Importar fórmula baseada no Docker - PySpark](#pyspark)
- [Importar fórmula baseada no Docker - Scala](#scala)

### Configurar uma fórmula {#configure}

Cada instância da receita em [!DNL Data Science Workspace] é acompanhada de um conjunto de configurações que adaptam a instância da receita para atender a um caso de uso específico. Os arquivos de configuração definem os comportamentos padrão de treinamento e pontuação de um Modelo criado usando essa instância da fórmula.

>[!NOTE]
>
>Os arquivos de configuração são específicos para cada fórmula e maiúsculas e minúsculas.

Abaixo está um exemplo de arquivo de configuração mostrando os comportamentos padrão de treinamento e pontuação para a receita de vendas de varejo.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Tecla Parameter | Tipo | Descrição |
| ----- | ----- | ----- |
| `learning_rate` | Número | Escalar para multiplicação de gradiente. |
| `n_estimators` | Número | Número de árvores na floresta para Classificador Random Forest. |
| `max_depth` | Número | Profundidade máxima de uma árvore no Classificador Random Forest. |
| `ACP_DSW_INPUT_FEATURES` | String | Lista de atributos de schema de entrada separados por vírgulas. |
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de schema de saída separados por vírgulas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída são modificáveis |
| `tenantId` | String | Essa ID garante que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para localizar sua ID de locatário. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | O schema de entrada usado para treinar um Modelo. Deixe isso vazio ao importar na interface do usuário, substitua por SchemaID de treinamento ao importar usando a API. |
| `evaluation.labelColumn` | String | Rótulo de coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O schema de saída usado para marcar um Modelo. Deixe isso vazio ao importar na interface do usuário, substitua por SchemaID de pontuação ao importar usando a API. |

Para a finalidade deste tutorial, você pode deixar os arquivos de configuração padrão para a receita de Vendas de varejo na [!DNL Data Science Workspace] Referência da forma como eles são.

### Importar fórmula baseada no Docker - [!DNL Python] {#python}

Start navegando e selecionando **[!UICONTROL Workflows]** localizados na parte superior esquerda da [!DNL Platform] interface do usuário. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Iniciar]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Digite um nome e uma descrição para a fórmula e selecione **[!UICONTROL Próximo]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Encapsulamento de arquivos de origem em um tutorial de Recipe), um URL de Docker foi fornecido no final da criação da receita de vendas de varejo usando arquivos de origem Python.

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando arquivos [!DNL Python] de origem no campo URL **[!UICONTROL de]** origem. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecione **[!UICONTROL Python]** na lista suspensa *Tempo de execução* e **[!UICONTROL Classificação]** na lista suspensa *Tipo* . Depois que tudo estiver preenchido, clique em **[!UICONTROL Avançar]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
>
> *O tipo* suporta **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando Recurso **[!UICONTROL de]** entrada ou Recurso **[!UICONTROL de]** Público alvo na janela Propriedades **[!UICONTROL do]** campo direita. Para a finalidade deste tutorial, defina **[!UICONTROL semanalmenteSales]** como o Recurso **[!UICONTROL do]** Público alvo e tudo o mais como Recurso **[!UICONTROL de]** entrada. Clique em **[!UICONTROL Avançar]** para revisar sua nova fórmula configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **[!UICONTROL Concluir]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Vá para as [próximas etapas](#next-steps) para descobrir como criar um Modelo [!DNL Data Science Workspace] usando a fórmula recém-criada de Vendas de Varejo.

### Importar fórmula baseada no Docker - R {#r}

Start navegando e selecionando **[!UICONTROL Workflows]** localizados na parte superior esquerda da [!DNL Platform] interface do usuário. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Iniciar]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Digite um nome e uma descrição para a fórmula e selecione **[!UICONTROL Próximo]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Arquivos de origem do pacote), um URL do Docker foi fornecido no final da criação da receita de vendas de varejo usando arquivos de origem R.

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem R no campo URL **[!UICONTROL de]** origem. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecione **[!UICONTROL R]** no menu suspenso *Tempo de execução* e **[!UICONTROL Classificação]** no menu suspenso *Tipo* . Depois que tudo estiver preenchido, clique em **[!UICONTROL Avançar]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
>
> *O tipo* suporta **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando Recurso **[!UICONTROL de]** entrada ou Recurso **[!UICONTROL de]** Público alvo na janela Propriedades **[!UICONTROL do]** campo direita. Para a finalidade deste tutorial, defina **[!UICONTROL semanalmenteSales]** como o Recurso **[!UICONTROL do]** Público alvo e tudo o mais como Recurso **[!UICONTROL de]** entrada. Clique em **[!UICONTROL Avançar]** para revisar sua nova receita configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **Concluir** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Vá para as [próximas etapas](#next-steps) para descobrir como criar um Modelo [!DNL Data Science Workspace] usando a fórmula recém-criada de Vendas de Varejo.

### Importar fórmula baseada no Docker - PySpark {#pyspark}

Start navegando e selecionando **[!UICONTROL Workflows]** localizados na parte superior esquerda da [!DNL Platform] interface do usuário. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Iniciar]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Arquivos de origem do pacote), um URL de Docker foi fornecido no final da criação da receita de vendas de varejo usando arquivos de origem PySpark.

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem do PySpark no campo URL **[!UICONTROL de]** origem. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecione **[!UICONTROL PySpark]** no menu suspenso *Runtime* . Depois que o tempo de execução PySpark é selecionado, o artefato padrão é preenchido automaticamente para o **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Classificação]** no menu suspenso *Tipo* . Depois que tudo estiver preenchido, clique em **[!UICONTROL Avançar]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
>
> *O tipo* suporta **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando Recurso **[!UICONTROL de]** entrada ou Recurso **[!UICONTROL de]** Público alvo na janela Propriedades **[!UICONTROL do]** campo direita. Para a finalidade deste tutorial, defina **[!UICONTROL semanalmenteSales]** como o Recurso **[!UICONTROL do]** Público alvo e tudo o mais como Recurso **[!UICONTROL de]** entrada. Clique em **[!UICONTROL Avançar]** para revisar sua nova fórmula configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **[!UICONTROL Concluir]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Vá para as [próximas etapas](#next-steps) para descobrir como criar um Modelo [!DNL Data Science Workspace] usando a fórmula recém-criada de Vendas de Varejo.

### Importar fórmula baseada no Docker - Scala {#scala}

Start navegando e selecionando **[!UICONTROL Workflows]** localizados na parte superior esquerda da [!DNL Platform] interface do usuário. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Iniciar]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Encapsulamento de arquivos de origem em um tutorial de Receita), um URL de Docker foi fornecido no final da criação da receita de Vendas de Varejo usando arquivos de origem Scala ([!DNL Spark]).

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem do Scala no campo URL *de* origem. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecione **[!UICONTROL Spark]** no menu suspenso *Runtime* . Depois que o tempo de execução é selecionado, o artefato padrão é preenchido automaticamente para o [!DNL Spark] Docker ****. Em seguida, selecione **[!UICONTROL Regressão]** no menu suspenso *Tipo* . Depois que tudo estiver preenchido, clique em **[!UICONTROL Avançar]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
>
> *O tipo* suporta **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando Recurso **[!UICONTROL de]** entrada ou Recurso **[!UICONTROL de]** Público alvo na janela Propriedades **[!UICONTROL do]** campo direita. Para a finalidade deste tutorial, defina **[!UICONTROL semanalmenteSales]** como o Recurso **[!UICONTROL do]** Público alvo e tudo o mais como Recurso **[!UICONTROL de]** entrada. Clique em **[!UICONTROL Avançar]** para revisar sua nova fórmula configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **[!UICONTROL Concluir]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Vá para as [próximas etapas](#next-steps) para descobrir como criar um Modelo [!DNL Data Science Workspace] usando a fórmula recém-criada de Vendas de Varejo.

## Próximas etapas {#next-steps}

Este tutorial forneceu informações sobre como configurar e importar uma receita para [!DNL Data Science Workspace]. Agora você pode criar, treinar e avaliar um Modelo usando a fórmula recém-criada.

- [Treinar e avaliar um modelo na interface do usuário](./train-evaluate-model-ui.md)
- [Treinar e avaliar um modelo usando a API](./train-evaluate-model-api.md)