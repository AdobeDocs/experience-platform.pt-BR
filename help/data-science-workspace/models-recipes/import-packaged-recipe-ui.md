---
keywords: Experience Platform;importar receita empacotada;Data Science Workspace;tópicos populares;receitas;ui;criar mecanismo
solution: Experience Platform
title: Importar uma fórmula empacotada na interface do usuário do Data Science Workspace
type: Tutorial
description: Este tutorial fornece informações sobre como configurar e importar uma fórmula em pacote usando o exemplo fornecido de Vendas de Varejo. Ao final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 0%

---

# Importar uma fórmula em pacote na interface do usuário do Data Science Workspace

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial fornece informações sobre como configurar e importar uma fórmula em pacote usando o exemplo fornecido de Vendas de Varejo. Ao final deste tutorial, você estará pronto para criar, treinar e avaliar um Modelo no Adobe Experience Platform [!DNL Data Science Workspace].

## Pré-requisitos

Este tutorial requer uma fórmula em pacote no formato de um URL de imagem do Docker. Consulte o tutorial sobre como [Compactar arquivos de origem em uma fórmula](./package-source-files-recipe.md) para obter mais informações.

## interface fluxo de Trabalho

A importação de uma fórmula empacotada para [!DNL Data Science Workspace] configurações de fórmula específicas, compiladas em um único arquivo de Anotação de Objeto JavaScript (JSON), esta compilação de configurações fórmula é conhecida como o arquivo de configuração. Um fórmula com um conjunto específico de configurações é conhecido como um fórmula instância. Uma fórmula pode ser usada para criar muitas instâncias fórmula em [!DNL Data Science Workspace].

A fluxo de Trabalho para importação de um fórmula de pacote consiste nas seguintes etapas:
- [Configurar um fórmula](#configure)
- [Importar fórmula baseada no Docker - Python](#python)
- [Importar fórmula baseada no Docker - R](#r)
- [Importar fórmula baseada no Docker - PySpark](#pyspark)
- [Importar fórmula baseada no Docker - Scala](#scala)

### Configurar uma fórmula {#configure}

Cada instância da fórmula em [!DNL Data Science Workspace] é acompanhada por um conjunto de configurações que adaptam a instância da fórmula para atender a um caso de uso específico. Os arquivos de configuração definem as treinamento padrão e os comportamentos de pontuação de um Modelo criado usando esse fórmula instância.

>[!NOTE]
>
>Os arquivos de configuração são fórmula e específicos para maiúsculas e minúsculas.

Abaixo está um arquivo de configuração de amostra mostrando comportamentos padrão de treinamento e pontuação para o fórmula de Vendas no varejo.

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
| `learning_rate` | Número | Escala para multiplicação de gradiente. |
| `n_estimators` | Número | Número de árvores na floresta para Classificador de Floresta Aleatória. |
| `max_depth` | Número | Profundidade máxima de uma árvore no Classificador Random Forest. |
| `ACP_DSW_INPUT_FEATURES` | String | Lista de atributos de esquema de entrada separados por vírgula. |
| `ACP_DSW_TARGET_FEATURES` | String | Lista de atributos de esquema de saída separados por vírgulas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina se os recursos de entrada e saída podem ser modificados |
| `tenantId` | String | Essa ID garante que os recursos criados sejam nomes espaçados corretamente e contidos na organização. [Siga as etapas aqui](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar sua ID do inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | String | A entrada schema usada para treinamento um Modelo. Deixe isso em branco ao importar na interface do usuário, substitua por SchemaID de treinamento ao importar usando a API. |
| `evaluation.labelColumn` | String | Rótulo da coluna para visualizações de avaliação. |
| `evaluation.metrics` | String | Lista separada por vírgulas de métricas de avaliação a serem usadas para avaliar um Modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | String | O esquema de saída usado para pontuar um Modelo. Deixe isso em branco ao importar na interface do usuário, substitua por SchemaID de pontuação ao importar usando a API. |

Para o propósito deste tutorial, você pode deixar os arquivos de configuração padrão para a fórmula de Vendas de Varejo na [!DNL Data Science Workspace] Referencie como estão.

### Importar fórmula baseada no Docker - [!DNL Python] {#python}

Comece navegando e selecionando **[!UICONTROL Fluxos de trabalho]** localizados na parte superior esquerda da interface do usuário do [!DNL Platform]. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Iniciar]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A **página Configurar** para a **Importar fórmula** fluxo de Trabalho é exibida. Insira um nome e uma descrição para a fórmula, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito.

![configurar fluxo de Trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nos arquivos de origem do [Pacote em um tutorial de Receita](./package-source-files-recipe.md) , um Docker URL foi fornecido no final da construção do fórmula de Vendas de Varejo usando arquivos de origem Python.

Depois de estar na página de origem **** Select, cole o Docker URL correspondente aos fórmula criados com pacotes usando [!DNL Python] arquivos de origem **[!UICONTROL no campo de Origem URL]**. Próximo, importe o arquivo de configuração fornecido arrastando e soltando ou use o navegador **do sistema** de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Selecione **[!UICONTROL Python]** no menu suspenso **Tempo de Execução** e **[!UICONTROL Classificação]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Avançar]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> O tipo dá suporte a **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o seu modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo na seção **Gerenciar esquemas**, que foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção **Gerenciamento de recursos**, selecione em sua identificação de locatário no visualizador de esquema para expandir o esquema de entrada de Vendas de Varejo. Selecione os recursos de entrada e saída, realçando o recurso desejado e selecionando **[!UICONTROL Recurso de Entrada]** ou **[!UICONTROL Recurso de Destino]** na janela direita **[!UICONTROL Propriedades do Campo]**. Para fins deste tutorial, defina **[!UICONTROL weeklySales]** como o **[!UICONTROL Recurso do Target]** e tudo o mais como **[!UICONTROL Recurso de Entrada]**. Selecione **[!UICONTROL Avançar]** para revisar sua nova fórmula configurada.

Revise a fórmula, adicione, modifique ou remova configurações conforme necessário. Selecione **[!UICONTROL Concluir]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula de Vendas de Varejo recém-criada.

### Importar fórmula baseada no Docker - R {#r}

Comece navegando e selecionando **[!UICONTROL Fluxos de trabalho]** localizados na parte superior esquerda da interface do usuário do [!DNL Platform]. Em seguida, selecione **Importar fórmula** e selecione **[!UICONTROL Iniciar]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A **página Configurar** para a **Importar fórmula** fluxo de Trabalho é exibida. Insira um nome e uma descrição para a fórmula, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito.

![configurar fluxo de Trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nos arquivos de origem do [Pacote em um tutorial de Receita](./package-source-files-recipe.md) , um Docker URL foi fornecido no final da construção do fórmula de Vendas de Varejo usando arquivos de origem R.

Depois de estar na página de origem **** Select, cole o Docker URL correspondente aos fórmula agrupados construídos usando arquivos de origem **[!UICONTROL R no campo de Origem URL]**. Próximo, importe o arquivo de configuração fornecido arrastando e soltando ou use o navegador **do sistema** de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Selecione **[!UICONTROL R]** na **lista suspensa Tempo** de execução e **[!UICONTROL Classificação]** no **menu suspenso Tipo** . Depois que tudo estiver preenchido, selecione **[!UICONTROL Avançar]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> *Type* dá suporte a **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se o seu modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo na seção **Gerenciar esquemas**, que foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Na seção *Gerenciamento de recursos*, selecione em sua identificação de locatário no visualizador de esquema para expandir o esquema de entrada de Vendas de Varejo. Selecione os recursos de entrada e saída, realçando o recurso desejado e selecionando **[!UICONTROL Recurso de Entrada]** ou **[!UICONTROL Recurso de Destino]** na janela direita **[!UICONTROL Propriedades do Campo]**. Para fins deste tutorial, defina **[!UICONTROL weeklySales]** como o **[!UICONTROL Recurso do Target]** e tudo o mais como **[!UICONTROL Recurso de Entrada]**. Selecione **[!UICONTROL Avançar]** para revisar sua nova fórmula Configurada.

Revise as fórmula, adicione, modifique ou remova as configurações conforme necessário. Selecione **Concluir** para criar o fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continue para as [próximas etapas](#next-steps) para descobrir como criar um Modelo usando o recém-criado fórmula de Vendas no [!DNL Data Science Workspace] Varejo.

### Importar com base no Docker fórmula - PySpark {#pyspark}

Início navegando e selecionando **[!UICONTROL Workflows localizados]** no canto superior esquerdo da [!DNL Platform] interface. Próximo, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A **página Configurar** para a **Importar fórmula** fluxo de Trabalho é exibida. Insira um nome e uma descrição para a fórmula, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![configurar fluxo de Trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nos arquivos de origem do [Pacote em um tutorial de Receita](./package-source-files-recipe.md) , um Docker URL foi fornecido no final da construção do fórmula de Vendas de Varejo usando arquivos de origem do PySpark.

Uma vez que você esteja na página de origem **** Select, cole o Docker URL correspondente ao fórmula embalado construído usando arquivos de origem do PySpark no campo de **[!UICONTROL Origem URL]**. Próximo, importe o arquivo de configuração fornecido arrastando e soltando ou use o navegador **do sistema** de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Selecione **[!UICONTROL PySpark]** na **lista suspensa Tempo** de execução. Depois que o tempo de execução do PySpark é selecionado, o artefato padrão é preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Classificação]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Avançar]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> *Type* dá suporte a **[!UICONTROL Classification]** e **[!UICONTROL Regression]**. Se o seu modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

Em seguida, selecione os esquemas de entrada e saída de Vendas de Varejo usando o seletor **Gerenciar esquemas**. Os esquemas foram criados usando o script de inicialização fornecido no [tutorial criar esquema e conjunto de dados de vendas de varejo](../models-recipes/create-retails-sales-dataset.md).

![gerenciar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

**Na seção Gerenciamento** de recursos, selecione na identificação do locatário no schema visualizador para expandir as entradas de Vendas no varejo schema. Selecione os recursos de entrada e saída, destacando o recurso desejado e selecionando **[!UICONTROL O Recurso]** de entrada ou **[!UICONTROL Target Recurso]** na janela de Propriedades ]**campo direito**[!UICONTROL . Para a finalidade deste tutorial, defina **[!UICONTROL weeklySales]** como o Recurso ]**de Target e todo o**[!UICONTROL  resto como **[!UICONTROL Recurso]** de entrada. Selecione **[!UICONTROL Próximo]** para revisar sua nova fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise as fórmula, adicione, modifique ou remova as configurações conforme necessário. Selecione **[!UICONTROL Concluir]** para criar o fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continue para as [próximas etapas](#next-steps) para descobrir como criar um Modelo usando o recém-criado fórmula de Vendas no [!DNL Data Science Workspace] Varejo.

### fórmula baseado em Docker Importar - Scala {#scala}

Início navegando e selecionando **[!UICONTROL Workflows localizados]** no canto superior esquerdo da [!DNL Platform] interface. Próximo, selecione **Importar fórmula** e selecione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

A **página Configurar** para a **Importar fórmula** fluxo de Trabalho é exibida. Insira um nome e uma descrição para a fórmula, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![configurar fluxo de Trabalho](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> Nos arquivos de origem do [Pacote em um tutorial de Receita](./package-source-files-recipe.md) , um Docker URL foi fornecido no final da construção do fórmula de Vendas no Varejo usando arquivos de origem Scala ([!DNL Spark]).

Quando você estiver na página **Selecionar origem**, cole a URL do Docker correspondente à fórmula em pacote criada usando arquivos de origem Scala no campo URL do Source. Em seguida, importe o arquivo de configuração fornecido arrastando e soltando ou use o navegador do sistema de arquivos. O arquivo de configuração fornecido pode ser encontrado em `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Selecione **[!UICONTROL Spark]** no menu suspenso **Tempo de Execução**. Depois que o tempo de execução [!DNL Spark] for selecionado, o artefato padrão será preenchido automaticamente para **[!UICONTROL Docker]**. Em seguida, selecione **[!UICONTROL Regressão]** no menu suspenso **Tipo**. Depois que tudo estiver preenchido, selecione **[!UICONTROL Avançar]** no canto superior direito para prosseguir para **Gerenciar esquemas**.

>[!NOTE]
>
> O tipo dá suporte a **[!UICONTROL Classificação]** e **[!UICONTROL Regressão]**. Se o seu modelo não se enquadrar em um desses tipos, selecione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

Próximo, selecione a entrada de Vendas no varejo e os schemas de saída usando o **seletor Manage Schemas** , os esquemas foram criados usando o script de inicialização fornecido na criação do [schema de vendas no varejo e na conjunto de dados](../models-recipes/create-retails-sales-dataset.md) tutorial.

![schemas de gerenciar](../images/models-recipes/import-package-ui/manage-schemas.png)

**Na seção Gerenciamento** de recursos, selecione na identificação do locatário no schema visualizador para expandir as entradas de Vendas no varejo schema. Selecione os recursos de entrada e saída, destacando o recurso desejado e selecionando **[!UICONTROL O Recurso]** de entrada ou **[!UICONTROL Target Recurso]** na janela de Propriedades ]**campo direito**[!UICONTROL . Para esse tutorial, defina &quot;[!UICONTROL weeklySales]&quot; como o  **[!UICONTROL Recurso]** de Target e tudo mais como **[!UICONTROL Recurso]** de entrada. Selecione **[!UICONTROL Próximo]** para revisar sua nova fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise a fórmula, adicione, modifique ou remova configurações conforme necessário. Selecione **[!UICONTROL Concluir]** para criar a fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Prossiga para as [próximas etapas](#next-steps) para descobrir como criar um Modelo no [!DNL Data Science Workspace] usando a fórmula de Vendas de Varejo recém-criada.

## Próximas etapas {#next-steps}

Este tutorial forneceu informações sobre como configurar e importar uma fórmula para o [!DNL Data Science Workspace]. Agora você pode criar, treinar e avaliar um Modelo usando a fórmula recém-criada.

- [Treinar e avaliar um modelo na interface do usuário](./train-evaluate-model-ui.md)
- [Treinar e avaliar um modelo usando a API](./train-evaluate-model-api.md)
