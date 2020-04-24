---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importar uma receita empacotada (IU)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Importar uma receita empacotada (IU)

Este tutorial fornece informações sobre como configurar e importar uma receita empacotada usando o exemplo de Vendas de Varejo fornecido. Até o final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo na Adobe Experience Platform Data Science Workspace.

## Pré-requisitos

Este tutorial requer uma fórmula empacotada na forma de um URL de imagem do Docker. Consulte o tutorial sobre como [agrupar arquivos de origem em uma Receita](./package-source-files-recipe.md) para obter mais informações.

## Fluxo de trabalho da interface

A importação de uma fórmula empacotada para a Data Science Workspace requer configurações específicas de fórmula, compiladas em um único arquivo JSON (JavaScript Object Notation), essa compilação de configurações de fórmula é chamada de arquivo **de** configuração. Uma fórmula embalada com um conjunto específico de configurações é chamada de instância **da** fórmula. Uma fórmula pode ser usada para criar várias instâncias de fórmula na Data Science Workspace.

O fluxo de trabalho para importar uma fórmula de pacote consiste nas seguintes etapas:
- [Configurar uma fórmula](#configure)
- [Importar fórmula baseada no Docker - Python](#python)
- [Importar fórmula baseada no Docker - R](#r)
- [Importar fórmula baseada no Docker - PySpark](#pyspark)
- [Importar fórmula baseada no Docker - Scala](#scala)

workflows obsoletos:
- [Importar fórmula com base em binários - PySpark](#pyspark-deprecated)
- [Importar fórmula baseada em binários - Scala Spark](#scala-deprecated)

### Configurar uma fórmula {#configure}

Cada instância da fórmula na Data Science Workspace é acompanhada de um conjunto de configurações que adaptam a instância da fórmula para atender a um caso de uso específico. Os arquivos de configuração definem os comportamentos padrão de treinamento e pontuação de um Modelo criado usando essa instância da fórmula.

>[!NOTE] Os arquivos de configuração são específicos para cada fórmula e maiúsculas e minúsculas.

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
| `evaluation.metrics` | String | lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O schema de saída usado para marcar um Modelo. Deixe isso vazio ao importar na interface do usuário, substitua por SchemaID de pontuação ao importar usando a API. |

Para a finalidade deste tutorial, você pode deixar os arquivos de configuração padrão para a receita de Vendas de varejo na Referência da área de trabalho da Data Science da forma como eles são.

### Importar fórmula baseada no Docker - Python {#python}

Start navegando e selecionando **[!UICONTROL Workflows]** localizado na parte superior esquerda da interface do usuário da plataforma. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Insira um nome e uma descrição para a receita e selecione-a **[!UICONTROL Next]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Encapsulamento de arquivos de origem em um tutorial de Recipe), um URL de Docker foi fornecido no final da criação da receita de vendas de varejo usando arquivos de origem Python.

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem Python no **[!UICONTROL Source URL]** campo. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecione **[!UICONTROL Python]** na lista suspensa *Tempo de execução* e **[!UICONTROL Classification]** na lista suspensa *Tipo* . Depois que tudo estiver preenchido, clique **[!UICONTROL Next]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
> *O tipo *suporta **[!UICONTROL Classification]**e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela direita **[!UICONTROL Field Properties]** . Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como o **[!UICONTROL Target Feature]** e tudo o mais como **[!UICONTROL Input Feature]**. Clique **[!UICONTROL Next]** para revisar sua nova fórmula configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **[!UICONTROL Finish]** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Siga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo na Data Science Workspace usando a fórmula de vendas a varejo recém-criada.

### Importar fórmula baseada no Docker - R {#r}

Start navegando e selecionando **[!UICONTROL Workflows]** localizado na parte superior esquerda da interface do usuário da plataforma. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Insira um nome e uma descrição para a receita e selecione-a **[!UICONTROL Next]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Arquivos de origem do pacote), um URL do Docker foi fornecido no final da criação da receita de vendas de varejo usando arquivos de origem R.

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem R no **[!UICONTROL Source URL]** campo. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecione **[!UICONTROL R]** no menu suspenso *Tempo de execução* e **[!UICONTROL Classification]** no menu suspenso *Tipo* . Depois que tudo estiver preenchido, clique **[!UICONTROL Next]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
> *O tipo *suporta **[!UICONTROL Classification]**e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela direita **[!UICONTROL Field Properties]** . Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como o **[!UICONTROL Target Feature]** e tudo o mais como **[!UICONTROL Input Feature]**. Clique **[!UICONTROL Next]** para revisar sua nova receita configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **Concluir** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Siga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo na Data Science Workspace usando a fórmula de vendas a varejo recém-criada.

### Importar fórmula baseada no Docker - PySpark {#pyspark}

Start navegando e selecionando **[!UICONTROL Workflows]** localizado na parte superior esquerda da interface do usuário da plataforma. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Next]** no canto superior direito para continuar.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> No [Package source files to a Recipe](./package-source-files-recipe.md) tutorial (Arquivos de origem do pacote), um URL de Docker foi fornecido no final da criação da receita de vendas de varejo usando arquivos de origem PySpark.

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem do PySpark no **[!UICONTROL Source URL]** campo. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecione **[!UICONTROL PySpark]** no menu suspenso *Tempo de execução* . Depois que o tempo de execução do PySpark é selecionado, o artefato padrão é preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Classification]** no menu suspenso *Tipo* . Depois que tudo estiver preenchido, clique **[!UICONTROL Next]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
> *O tipo *suporta **[!UICONTROL Classification]**e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela direita **[!UICONTROL Field Properties]** . Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como o **[!UICONTROL Target Feature]** e tudo o mais como **[!UICONTROL Input Feature]**. Clique **[!UICONTROL Next]** para revisar sua nova fórmula configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **[!UICONTROL Finish]** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Siga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo na Data Science Workspace usando a fórmula de vendas a varejo recém-criada.

### Importar fórmula baseada no Docker - Scala {#scala}

Start navegando e selecionando **[!UICONTROL Workflows]** localizado na parte superior esquerda da interface do usuário da plataforma. Em seguida, selecione *Importar fórmula* e clique em **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página *Configurar* para o fluxo de trabalho da fórmula *Importar* é exibida. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Next]** no canto superior direito para continuar.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> No [Package source files to a Recipe tutorial (Encapsulamento de arquivos de origem para um tutorial de Receita](./package-source-files-recipe.md) ), um URL de Docker foi fornecido no final da criação da receita de Vendas de Varejo usando os arquivos de origem Scala (Spark).

Quando estiver na página *Selecionar origem* , cole o URL do Docker correspondente à fórmula empacotada criada usando os arquivos de origem do Scala no campo URL *de* origem. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecione **[!UICONTROL Spark]** no menu suspenso *Tempo de execução* . Quando o tempo de execução do Spark é selecionado, o artefato padrão é preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Regression]** no menu suspenso *Tipo* . Depois que tudo estiver preenchido, clique **[!UICONTROL Next]** no canto superior direito para prosseguir para *Gerenciar schemas*.

>[!NOTE]
> *O tipo *suporta **[!UICONTROL Classification]**e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Em seguida, selecione os schemas de entrada e saída do Retail Sales na seção *Gerenciar Schemas*, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção Gerenciamento *de* recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela direita **[!UICONTROL Field Properties]** . Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como o **[!UICONTROL Target Feature]** e tudo o mais como **[!UICONTROL Input Feature]**. Clique **[!UICONTROL Next]** para revisar sua nova fórmula configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **[!UICONTROL Finish]** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Siga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo na Data Science Workspace usando a fórmula de vendas a varejo recém-criada.

## Próximas etapas {#next-steps}

Este tutorial forneceu insight sobre como configurar e importar uma receita para a Data Science Workspace. Agora você pode criar, treinar e avaliar um Modelo usando a fórmula recém-criada.

- [Treinar e avaliar um modelo na interface do usuário](./train-evaluate-model-ui.md)
- [Treinar e avaliar um modelo usando a API](./train-evaluate-model-api.md)

## workflows obsoletos

>[!CAUTION]
>A importação de fórmulas baseadas em binários não é mais suportada no PySpark 3 (Spark 2.4) e no Scala (Spark 2.4).

### Importar fórmula com base em binários - PySpark {#pyspark-deprecated}

Nos arquivos de origem do [pacote em um tutorial de Receita](./package-source-files-recipe.md) , um arquivo binário **EGG** foi criado usando os arquivos de origem do Retail Sales PySpark.

1. No [Adobe Experience Platform](https://platform.adobe.com/), localize o painel de navegação esquerdo e clique em **Workflows**. Na interface de Workflows, **inicie** um novo processo **Importar receita do arquivo** de origem.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Insira um nome adequado para a receita de Vendas de varejo. Por exemplo, &quot;Fórmula de vendas de varejo PySpark&quot;. Opcionalmente, inclua uma descrição da fórmula e um URL da documentação. Clique em **Avançar** quando terminar.
   ![](../images/models-recipes/import-package-ui/recipe_info.png)
3. Importe a receita PySpark Retail Sales que foi criada nos arquivos de origem do [pacote para um tutorial de Receita](./package-source-files-recipe.md) arrastando e soltando ou use o **navegador** do sistema de arquivos. A receita embalada deve estar localizada em `experience-platform-dsw-reference/recipes/pyspark/dist`.
Da mesma forma, importe o arquivo de configuração fornecido arrastando e soltando ou use o **Navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/pyspark/pipeline.json`. Clique em **Avançar** quando ambos os arquivos tiverem sido fornecidos.
   ![](../images/models-recipes/import-package-ui/recipe_source.png)
4. Você pode encontrar erros neste ponto. É um comportamento normal e é de esperar. Selecione os schemas de entrada e saída do Retail Sales na seção **Gerenciar Schemas**, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Na seção Gerenciamento **de** recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando Recurso **de** entrada ou Recurso **de** Público alvo na janela Propriedades **do** campo direita. Para a finalidade deste tutorial, defina **semanalmenteSales** como o Recurso **do** Público alvo e tudo o mais como Recurso **de** entrada. Clique em **Avançar** para revisar sua nova fórmula configurada.
5. Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **Concluir** para criar a fórmula.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Siga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo na Data Science Workspace usando a fórmula de vendas a varejo recém-criada.


### Importar fórmula baseada em binários - Scala Spark {#scala-deprecated}

Nos arquivos de origem do [pacote em um tutorial de Receita](./package-source-files-recipe.md) , um arquivo binário **JAR** foi criado usando os arquivos de origem do Scala Spark de vendas de varejo.

1. No [Adobe Experience Platform](https://platform.adobe.com/), localize o painel de navegação esquerdo e clique em **Workflows**. Na interface de Workflows, **inicie** um novo processo **Importar receita do arquivo** de origem.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Insira um nome adequado para a receita de Vendas de varejo. Por exemplo, &quot;Scala Spark da receita de Vendas de Varejo&quot;. Opcionalmente, inclua uma descrição da fórmula e um URL da documentação. Clique em **Avançar** quando terminar.
   ![](../images/models-recipes/import-package-ui/recipe_info_scala.png)
3. Importe a receita de vendas de varejo do Scala Spark criada nos arquivos de origem do [pacote para um tutorial de Receita](./package-source-files-recipe.md) arrastando e soltando ou use o **navegador** do sistema de arquivos. A fórmula empacotada **com dependências** está localizada em `experience-platform-dsw-reference/recipes/scala/target`. Da mesma forma, importe o arquivo de configuração fornecido arrastando e soltando ou use o **Navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/scala/src/main/resources/pipelineservice.json`. Clique em **Avançar** quando ambos os arquivos tiverem sido fornecidos.
   ![](../images/models-recipes/import-package-ui/recipe_source_scala.png)
4. Você pode encontrar erros neste ponto. É um comportamento normal e é de esperar. Selecione os schemas de entrada e saída do Retail Sales na seção **Gerenciar Schemas**, eles foram criados usando o script de inicialização fornecido no tutorial de [criação do schema de vendas de varejo e do conjunto de dados](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
Na seção Gerenciamento **de** recursos, clique na identificação do locatário no visualizador de schemas para expandir o schema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando Recurso **de** entrada ou Recurso **de** Público alvo na janela Propriedades **do** campo direita. Para a finalidade deste tutorial, defina **semanalmenteSales** como o Recurso **do** Público alvo e tudo o mais como Recurso **de** entrada. Clique em **Avançar** para revisar sua nova fórmula configurada.
5. Revise a receita, adicione, modifique ou remova configurações conforme necessário. Clique em **Concluir** para criar a fórmula.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Siga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo na Data Science Workspace usando a fórmula de vendas a varejo recém-criada.