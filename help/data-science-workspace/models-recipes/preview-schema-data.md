---
keywords: Experience Platform;dados do schema da pré-visualização;Data Science Workspace;topics populares
solution: Experience Platform
title: Pré-visualização do Schema de vendas de varejo e do conjunto de dados
topic: tutorial
type: Tutorial
description: O documento a seguir descreve a visualização de schemas e conjuntos de dados no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Pré-visualização do schema de vendas de varejo e do conjunto de dados

Após a conclusão com êxito do script de inicialização do tutorial [Criar o schema de vendas de varejo e o conjunto de dados](./create-retails-sales-dataset.md). Schemas de saída e conjuntos de dados podem ser exibidos em [!DNL Experience Platform]. Para visualização dos schemas e conjuntos de dados, siga as etapas abaixo:

1. Clique no link **[!UICONTROL Schemas]** localizado na coluna de navegação esquerda e localize o schema de entrada criado pelo script de inicialização. O nome do schema corresponderá ao que foi definido em `config.yaml` na etapa anterior. Visualização os detalhes do schema e sua composição clicando nele.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Clique no link **[!UICONTROL Conjuntos de dados]** localizado na coluna de navegação esquerda e abra o conjunto de dados de entrada criado ao clicar no nome da lista. O nome do conjunto de dados corresponderá ao que foi definido em `config.yaml` na etapa anterior.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Clique em **[!UICONTROL Conjunto de dados de Pré-visualização]** localizado na pré-visualização superior direita de um subconjunto do conjunto de dados.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Próximas etapas

Agora você assimilou com êxito dados de amostra de Vendas de varejo em [!DNL Experience Platform] usando o script de inicialização fornecido.

Para continuar trabalhando com os dados ingeridos:
- [Analise seus dados usando notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Use notebooks Júpiter em [!DNL Data Science Workspace] para acessar, explorar, visualizar e entender seus dados.
- [Empacotar arquivos de origem em uma Receita](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio Modelo para [!DNL Data Science Workspace] ao empacotar arquivos de origem em um arquivo de Receita importável.