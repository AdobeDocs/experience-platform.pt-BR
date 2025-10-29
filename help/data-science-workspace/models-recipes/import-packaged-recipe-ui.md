---
keywords: Experience Platform;importar receita empacotada;Data Science Workspace;tópicos populares;receitas;ui;criar mecanismo
solution: Experience Platform
title: Importar uma fórmula empacotada na interface do usuário do Data Science Workspace
type: Tutorial
description: Este tutorial fornece ao insight como configurar e importar uma fórmula em pacote usando o exemplo fornecido de Vendas de varejo. Ao final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 0%

---

# Importar uma fórmula em pacote na interface do usuário do Data Science Workspace

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial fornece ao insight como configurar e importar uma fórmula em pacote usando o exemplo fornecido de Vendas de varejo. Ao final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

## Pré-requisitos

Este tutorial requer uma fórmula em pacote no formato de um URL de imagem do Docker. Consulte o tutorial sobre como [Compactar arquivos de origem em uma fórmula](./package-source-files-recipe.md) para obter mais informações.

## Fluxo de trabalho da interface do usuário

A importação de uma fórmula em pacote para o [!DNL Data Science Workspace] requer configurações de fórmula específicas, compiladas em um único arquivo JSON (JavaScript Object Notation). Essa compilação de configurações de fórmula é conhecida como o arquivo de configuração. Uma fórmula em pacote com um conjunto específico de configurações é chamada de instância de fórmula. Uma fórmula pode ser usada para criar muitas instâncias de fórmula em [!DNL Data Science Workspace].

O fluxo de trabalho para importar uma fórmula de pacote consiste nas seguintes etapas:

- [Configurar uma fórmula](#configure)
- [Importar fórmula baseada no Docker - Python](#python)
- [Importar fórmula baseada no Docker - R](#r)
- [Importar fórmula baseada no Docker - PySpark](#pyspark)
- [Importar fórmula baseada no Docker - Scala](#scala)

### Configurar uma fórmula {#configure}

Cada instância da fórmula em [!DNL Data Science Workspace] é acompanhada por um conjunto de configurações que adaptam a instância da fórmula para atender a um caso de uso específico. Os arquivos de configuração definem os comportamentos padrão de treinamento e pontuação de um Modelo criado usando essa instância de fórmula.

>[!NOTE]
>
>Os arquivos de configuração são específicos de receita e caso.

Abaixo está um arquivo de configuração de exemplo que mostra os comportamentos padrão de treinamento e pontuação para a fórmula de Vendas de varejo.

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
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de esquema de saída separados por vírgulas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída são modificáveis |
| `tenantId` | String | Essa ID garante que os recursos criados tenham o namespace adequado e estejam contidos na organização. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar sua ID de locatário. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | O esquema de entrada usado para treinar um Modelo. Deixe isso em branco ao importar na interface do usuário, substitua por SchemaID de treinamento ao importar usando a API. |
| `evaluation.labelColumn` | String | Rótulo da coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O esquema de saída usado para pontuar um Modelo. Deixe isso em branco ao importar na interface do usuário, substitua por SchemaID de pontuação ao importar usando a API. |

Para o propósito deste tutorial, você pode deixar os arquivos de configuração padrão para a fórmula de Vendas de Varejo na [!DNL Data Science Workspace] Referencie como estão.

### Importar fórmula baseada no Docker - [!DNL Python] {#python}

Comece navegando e selecionando **[!UICONTROL Workflows]**, localizado no canto superior esquerdo da interface do usuário do [!DNL Experience Platform]. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página **Configurar** para o fluxo de trabalho **Importar fórmula** é exibida. Insira um nome e uma descrição para a fórmula e selecione **[!UICONTROL Next]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No tutorial [Empacotar arquivos de origem em uma Receita](./package-source-files-recipe.md), uma URL Docker foi fornecida no final da criação da fórmula de Vendas de Varejo usando arquivos de origem Python.

Quando você estiver na página **Selecionar origem**, cole a URL do Docker correspondente à fórmula em pacote criada usando os arquivos de origem [!DNL Python] no campo **[!UICONTROL Source URL]**. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **Navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecione **[!UICONTROL Python]** no menu suspenso **Tempo de Execução** e **[!UICONTROL Classification]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Next]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> O tipo suporta **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo na seção **Gerenciar esquemas**, que foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção **Gerenciamento de recursos**, selecione em sua identificação de locatário no visualizador de esquema para expandir o esquema de entrada de Vendas de Varejo. Selecione os recursos de entrada e saída, realçando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela **[!UICONTROL Field Properties]** direita. Para o propósito deste tutorial, defina **[!UICONTROL weeklySales]** como **[!UICONTROL Target Feature]** e tudo mais como **[!UICONTROL Input Feature]**. Selecione **[!UICONTROL Next]** para revisar sua nova fórmula configurada.

Revise a fórmula, adicione, modifique ou remova configurações conforme necessário. Selecione **[!UICONTROL Finish]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula de Vendas de Varejo recém-criada.

### Importar fórmula baseada no Docker - R {#r}

Comece navegando e selecionando **[!UICONTROL Workflows]**, localizado no canto superior esquerdo da interface do usuário do [!DNL Experience Platform]. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página **Configurar** para o fluxo de trabalho **Importar fórmula** é exibida. Insira um nome e uma descrição para a fórmula e selecione **[!UICONTROL Next]** no canto superior direito.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No tutorial [Empacotar arquivos de origem em uma Fórmula](./package-source-files-recipe.md), uma URL Docker foi fornecida no final da criação da fórmula de Vendas de Varejo usando arquivos de origem R.

Quando você estiver na página **Selecionar origem**, cole a URL do Docker correspondente à fórmula em pacote criada usando arquivos de origem R no campo **[!UICONTROL Source URL]**. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **Navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecione **[!UICONTROL R]** no menu suspenso **Tempo de Execução** e **[!UICONTROL Classification]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Next]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> *Type* dá suporte a **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo na seção **Gerenciar esquemas**, que foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção *Gerenciamento de recursos*, selecione em sua identificação de locatário no visualizador de esquema para expandir o esquema de entrada de Vendas de Varejo. Selecione os recursos de entrada e saída, realçando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela **[!UICONTROL Field Properties]** direita. Para o propósito deste tutorial, defina **[!UICONTROL weeklySales]** como **[!UICONTROL Target Feature]** e tudo mais como **[!UICONTROL Input Feature]**. Selecione **[!UICONTROL Next]** para revisar sua nova fórmula Configurada.

Revise a fórmula, adicione, modifique ou remova configurações conforme necessário. Selecione **Concluir** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula de Vendas de Varejo recém-criada.

### Importar fórmula baseada no Docker - PySpark {#pyspark}

Comece navegando e selecionando **[!UICONTROL Workflows]**, localizado no canto superior esquerdo da interface do usuário do [!DNL Experience Platform]. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página **Configurar** para o fluxo de trabalho **Importar fórmula** é exibida. Insira um nome e uma descrição para a fórmula e selecione **[!UICONTROL Next]** no canto superior direito para continuar.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No tutorial [Empacotar arquivos de origem em uma Receita](./package-source-files-recipe.md), uma URL Docker foi fornecida no final da criação da fórmula de Vendas de Varejo usando arquivos de origem do PySpark.

Quando você estiver na página **Selecionar origem**, cole a URL do Docker correspondente à fórmula em pacote criada usando os arquivos de origem do PySpark no campo **[!UICONTROL Source URL]**. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o **Navegador** do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecione **[!UICONTROL PySpark]** no menu suspenso **Tempo de Execução**. Depois que o tempo de execução do PySpark é selecionado, o artefato padrão é preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Classification]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Next]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> *Type* dá suporte a **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo usando o seletor **Gerenciar esquemas**. Os esquemas foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![gerenciar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

Na seção **Gerenciamento de recursos**, selecione em sua identificação de locatário no visualizador de esquema para expandir o esquema de entrada de Vendas de Varejo. Selecione os recursos de entrada e saída, realçando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela **[!UICONTROL Field Properties]** direita. Para o propósito deste tutorial, defina **[!UICONTROL weeklySales]** como **[!UICONTROL Target Feature]** e tudo mais como **[!UICONTROL Input Feature]**. Selecione **[!UICONTROL Next]** para revisar sua nova fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise a fórmula, adicione, modifique ou remova configurações conforme necessário. Selecione **[!UICONTROL Finish]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula de Vendas de Varejo recém-criada.

### Importar fórmula baseada no Docker - Scala {#scala}

Comece navegando e selecionando **[!UICONTROL Workflows]**, localizado no canto superior esquerdo da interface do usuário do [!DNL Experience Platform]. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A página **Configurar** para o fluxo de trabalho **Importar fórmula** é exibida. Insira um nome e uma descrição para a fórmula e selecione **[!UICONTROL Next]** no canto superior direito para continuar.

![configurar fluxo de trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> No tutorial [Empacotar arquivos de origem em uma Fórmula](./package-source-files-recipe.md), uma URL Docker foi fornecida no final da criação da fórmula de Vendas de Varejo usando arquivos de origem Scala ([!DNL Spark]).

Quando você estiver na página **Selecionar origem**, cole a URL do Docker correspondente à fórmula em pacote criada usando arquivos de origem Scala no campo URL do Source. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o navegador do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecione **[!UICONTROL Spark]** no menu suspenso **Tempo de Execução**. Depois que o tempo de execução [!DNL Spark] for selecionado, o artefato padrão será preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Regression]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Next]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> O tipo suporta **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se o modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo usando o seletor **Gerenciar esquemas**. Os esquemas foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![gerenciar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

Na seção **Gerenciamento de recursos**, selecione em sua identificação de locatário no visualizador de esquema para expandir o esquema de entrada de Vendas de Varejo. Selecione os recursos de entrada e saída, realçando o recurso desejado e selecionando **[!UICONTROL Input Feature]** ou **[!UICONTROL Target Feature]** na janela **[!UICONTROL Field Properties]** direita. Para o propósito deste tutorial, defina &quot;[!UICONTROL weeklySales]&quot; como **[!UICONTROL Target Feature]** e todo o resto como **[!UICONTROL Input Feature]**. Selecione **[!UICONTROL Next]** para revisar sua nova fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise a fórmula, adicione, modifique ou remova configurações conforme necessário. Selecione **[!UICONTROL Finish]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula de Vendas de Varejo recém-criada.

## Próximas etapas {#next-steps}

Este tutorial forneceu o insight sobre como configurar e importar uma fórmula para o [!DNL Data Science Workspace]. Agora você pode criar, treinar e avaliar um Modelo usando a fórmula recém-criada.

- [Treinar e avaliar um modelo na interface do usuário](./train-evaluate-model-ui.md)
- [Treinar e avaliar um modelo usando a API](./train-evaluate-model-api.md)
