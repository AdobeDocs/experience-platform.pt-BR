---
keywords: Experience Platform, visualização de dados do esquema, Data Science Workspace, tópicos populares
solution: Experience Platform
title: Visualizar o esquema de vendas de varejo e o conjunto de dados
topic-legacy: tutorial
type: Tutorial
description: O documento a seguir descreve a visualização de esquemas e conjuntos de dados no Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Visualizar o esquema de vendas de varejo e o conjunto de dados

Após a conclusão bem-sucedida do script de bootstrap do tutorial [retail sales schema e conjunto de dados](./create-retails-sales-dataset.md). Esquemas de saída e conjuntos de dados podem ser visualizados em [!DNL Experience Platform]. Para exibir os esquemas e conjuntos de dados, siga as etapas abaixo:

Selecione a guia **[!UICONTROL Schemas]** localizada na navegação à esquerda e localize o schema de entrada criado pelo script do bootstrap. O nome do schema corresponderá ao que foi definido em `config.yaml` na etapa anterior. Visualize os detalhes do esquema e sua composição clicando nele.

![](../images/models-recipes/access-data/schema.PNG)

Selecione a guia **[!UICONTROL Datasets]** localizada na navegação à esquerda e abra o conjunto de dados de entrada criado ao selecionar o nome do conjunto de dados. O nome do conjunto de dados corresponde ao que foi definido em `config.yaml` na etapa anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Selecione **[!UICONTROL Preview Dataset]** localizado no canto superior direito para visualizar um subconjunto do conjunto de dados.

![](../images/models-recipes/access-data/preview.PNG)

## Próximas etapas

Agora você assimilou com sucesso dados de amostra de Vendas de varejo em [!DNL Experience Platform] usando o script de bootstrap fornecido.

Para continuar trabalhando com os dados assimilados:
- [Analise seus dados usando notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Use notebooks Júpiter em [!DNL Data Science Workspace] para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio Modelo para [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de Receita importante.
