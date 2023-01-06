---
keywords: Experience Platform, importar receita empacotada, Data Science Workspace, tópicos populares, receitas, interface do usuário, criar mecanismo
solution: Experience Platform
title: Importar uma Receita Empacotada na Interface do Usuário do Data Science Workspace
type: Tutorial
description: Este tutorial fornece informações sobre como configurar e importar uma receita empacotada usando o exemplo de Vendas de varejo fornecido. Ao final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 0%

---

# Importar uma receita empacotada na interface do usuário do Data Science Workspace

Este tutorial fornece informações sobre como configurar e importar uma receita empacotada usando o exemplo de Vendas de varejo fornecido. Ao final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

## Pré-requisitos

Este tutorial requer uma fórmula empacotada na forma de um URL de imagem Docker. Consulte o tutorial sobre como [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md) para obter mais informações.

## Fluxo de trabalho da interface do usuário

Importar uma receita empacotada para [!DNL Data Science Workspace] requer configurações de receita específicas, compiladas em um único arquivo JSON (JavaScript Object Notation), essa compilação de configurações de receita é chamada de arquivo de configuração. Uma fórmula empacotada com um conjunto específico de configurações é chamada de instância de receita. Uma receita pode ser usada para criar muitas instâncias de receita em [!DNL Data Science Workspace].

O fluxo de trabalho para importar uma receita de pacote consiste nas seguintes etapas:
- [Configurar uma receita](#configure)
- [Importar receita baseada no Docker - Python](#python)
- [Importar receita baseada no Docker - R](#r)
- [Importar receita baseada no Docker - PySpark](#pyspark)
- [Importar receita baseada no Docker - Scala](#scala)

### Configurar uma receita {#configure}

Cada instância da receita em [!DNL Data Science Workspace] é acompanhado por um conjunto de configurações que adaptam a instância da receita para atender a um caso de uso específico. Os arquivos de configuração definem os comportamentos padrão de treinamento e pontuação de um Modelo criado usando essa instância de receita.

>[!NOTE]
>
>Os arquivos de configuração são específicos de receita e maiúsculas e minúsculas.

Abaixo está um exemplo de arquivo de configuração que mostra os comportamentos padrão de treinamento e pontuação para a receita de Vendas de varejo.

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

| Chave de parâmetro | Tipo | Descrição |
| ----- | ----- | ----- |
| `learning_rate` | Número | Escalar para multiplicação de gradiente. |
| `n_estimators` | Número | Número de árvores na floresta para o Classificador Random Forest. |
| `max_depth` | Número | Profundidade máxima de uma árvore no Classificador Random Forest. |
| `ACP_DSW_INPUT_FEATURES` | String | Lista de atributos de esquema de entrada separados por vírgula. |
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de esquema de saída separados por vírgula. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída são modificáveis |
| `tenantId` | String | Essa ID garante que os recursos criados sejam namespacados corretamente e contidos na organização IMS. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar a ID do locatário. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | O schema de entrada usado para treinar um Modelo. Deixe isso em branco ao importar na interface do usuário, substitua por SchemaID de treinamento ao importar usando a API. |
| `evaluation.labelColumn` | String | Rótulo de coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O schema de saída usado para pontuar um Modelo. Deixe em branco ao importar na interface do usuário, substitua por SchemaID de pontuação ao importar usando a API. |

Para a finalidade deste tutorial, você pode deixar os arquivos de configuração padrão para Vendas de varejo na fórmula [!DNL Data Science Workspace] Faça referência a como são.

### Importar receita baseada no Docker - [!DNL Python] {#python}

Comece navegando e selecionando **[!UICONTROL Fluxos de trabalho]** localizado no canto superior esquerdo do [!DNL Platform] IU. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

O **Configurar** para a página **Importar fórmula** workflow é exibido. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Próximo]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md) tutorial, um URL Docker foi fornecido no final da criação da receita de Vendas de varejo usando arquivos de origem Python.

Quando estiver no **Selecionar origem** cole o URL do Docker correspondente à receita empacotada criada usando [!DNL Python] os arquivos de origem no **[!UICONTROL URL de origem]** campo. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o sistema de arquivos **Navegador**. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecionar **[!UICONTROL Python]** no **Tempo de execução** e **[!UICONTROL Classificação]** no **Tipo** menu suspenso. Depois que tudo tiver sido preenchido, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> Suporte de tipo **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo na seção **Gerenciar esquemas**, eles foram criados usando o script de inicialização fornecido no [criar o esquema de vendas de varejo e o conjunto de dados](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Em **Gerenciamento de recursos** selecione na identificação do locatário no visualizador de esquema para expandir o esquema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Recurso de entrada]** ou **[!UICONTROL Recurso do Target]** à direita **[!UICONTROL Propriedades do campo]** janela. Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como  **[!UICONTROL Recurso do Target]** e tudo mais **[!UICONTROL Recurso de entrada]**. Selecionar **[!UICONTROL Próximo]** para revisar a nova receita configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Selecionar **[!UICONTROL Concluir]** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para o [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula recém-criada Vendas de varejo.

### Importar receita baseada no Docker - R {#r}

Comece navegando e selecionando **[!UICONTROL Fluxos de trabalho]** localizado no canto superior esquerdo do [!DNL Platform] IU. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

O **Configurar** para a página **Importar fórmula** workflow é exibido. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Próximo]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md) tutorial, um URL Docker foi fornecido no final da criação da receita de Vendas de varejo usando arquivos de origem R.

Quando estiver no **Selecionar origem** cole o URL do Docker correspondente à receita empacotada criada usando arquivos de origem R no **[!UICONTROL URL de origem]** campo. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o sistema de arquivos **Navegador**. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecionar **[!UICONTROL R]** no **Tempo de execução** e **[!UICONTROL Classificação]** no **Tipo** menu suspenso. Depois que tudo tiver sido preenchido, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> *Tipo* suporta **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo na seção **Gerenciar esquemas**, eles foram criados usando o script de inicialização fornecido no [criar o esquema de vendas de varejo e o conjunto de dados](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Em *Gerenciamento de recursos* selecione na identificação do locatário no visualizador de esquema para expandir o esquema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Recurso de entrada]** ou **[!UICONTROL Recurso do Target]** à direita **[!UICONTROL Propriedades do campo]** janela. Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como  **[!UICONTROL Recurso do Target]** e tudo mais **[!UICONTROL Recurso de entrada]**. Selecionar **[!UICONTROL Próximo]** para revisar sua nova receita configurada.

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Selecionar **Concluir** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para o [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula recém-criada Vendas de varejo.

### Importar receita baseada no Docker - PySpark {#pyspark}

Comece navegando e selecionando **[!UICONTROL Fluxos de trabalho]** localizado no canto superior esquerdo do [!DNL Platform] IU. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

O **Configurar** para a página **Importar fórmula** workflow é exibido. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md) tutorial, um URL Docker foi fornecido no final da criação da receita de Vendas de varejo usando arquivos de origem PySpark.

Quando estiver no **Selecionar origem** cole o URL do Docker correspondente à receita empacotada criada usando arquivos de origem PySpark no **[!UICONTROL URL de origem]** campo. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o sistema de arquivos **Navegador**. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecionar **[!UICONTROL PySpark]** no **Tempo de execução** menu suspenso. Depois que o tempo de execução de PySpark é selecionado, o artefato padrão é preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Classificação]** no **Tipo** menu suspenso. Depois que tudo tiver sido preenchido, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> *Tipo* suporta **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo usando o **Gerenciar esquemas** seletor , os esquemas foram criados usando o script bootstrap fornecido no [criar o esquema de vendas de varejo e o conjunto de dados](../models-recipes/create-retails-sales-dataset.md) tutorial.

![gerenciar schemas](../images/models-recipes/import-package-ui/manage-schemas.png)

Em **Gerenciamento de recursos** selecione na identificação do locatário no visualizador de esquema para expandir o esquema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Recurso de entrada]** ou **[!UICONTROL Recurso do Target]** à direita **[!UICONTROL Propriedades do campo]** janela. Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como  **[!UICONTROL Recurso do Target]** e tudo mais **[!UICONTROL Recurso de entrada]**. Selecionar **[!UICONTROL Próximo]** para revisar a nova receita configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Selecionar **[!UICONTROL Concluir]** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para o [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula recém-criada Vendas de varejo.

### Importar receita baseada no Docker - Scala {#scala}

Comece navegando e selecionando **[!UICONTROL Fluxos de trabalho]** localizado no canto superior esquerdo do [!DNL Platform] IU. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

O **Configurar** para a página **Importar fórmula** workflow é exibido. Insira um nome e uma descrição para a receita e selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md) tutorial, um URL Docker foi fornecido no final da criação da receita de Vendas de varejo usando Scala ([!DNL Spark]) arquivos de origem.

Quando estiver no **Selecionar origem** cole o URL do Docker correspondente à receita empacotada criada usando arquivos de origem Scala no campo Source URL . Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o navegador do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecionar **[!UICONTROL Spark]** no **Tempo de execução** menu suspenso. Uma vez [!DNL Spark] tempo de execução é selecionado, o artefato padrão é preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Regressão]** do **Tipo** menu suspenso. Depois que tudo tiver sido preenchido, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> Suporte de tipo **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo usando o **Gerenciar esquemas** seletor , os esquemas foram criados usando o script bootstrap fornecido no [criar o esquema de vendas de varejo e o conjunto de dados](../models-recipes/create-retails-sales-dataset.md) tutorial.

![gerenciar schemas](../images/models-recipes/import-package-ui/manage-schemas.png)

Em **Gerenciamento de recursos** selecione na identificação do locatário no visualizador de esquema para expandir o esquema de entrada Vendas de varejo. Selecione os recursos de entrada e saída destacando o recurso desejado e selecionando **[!UICONTROL Recurso de entrada]** ou **[!UICONTROL Recurso do Target]** à direita **[!UICONTROL Propriedades do campo]** janela. Para a finalidade deste tutorial, defina &quot;[!UICONTROL weeklySales]&quot; como a  **[!UICONTROL Recurso do Target]** e tudo mais **[!UICONTROL Recurso de entrada]**. Selecionar **[!UICONTROL Próximo]** para revisar a nova receita configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise a receita, adicione, modifique ou remova configurações conforme necessário. Selecionar **[!UICONTROL Concluir]** para criar a receita.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para o [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula recém-criada Vendas de varejo.

## Próximas etapas {#next-steps}

Este tutorial forneceu informações sobre como configurar e importar uma receita no [!DNL Data Science Workspace]. Agora você pode criar, treinar e avaliar um Modelo usando a fórmula recém-criada.

- [Treine e avalie um modelo na interface do usuário](./train-evaluate-model-ui.md)
- [Treine e avalie um modelo usando a API](./train-evaluate-model-api.md)
