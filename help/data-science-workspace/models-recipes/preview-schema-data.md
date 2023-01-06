---
keywords: Experience Platform, visualização de dados do esquema, Data Science Workspace, tópicos populares
solution: Experience Platform
title: Visualizar o esquema de vendas de varejo e o conjunto de dados
type: Tutorial
description: O documento a seguir descreve a visualização de esquemas e conjuntos de dados no Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Visualizar o esquema de vendas de varejo e o conjunto de dados

Após a conclusão bem-sucedida do script de bootstrap do [esquema de vendas de varejo e conjunto de dados](./create-retails-sales-dataset.md) tutorial. Esquemas de saída e conjuntos de dados podem ser visualizados em [!DNL Experience Platform]. Para exibir os esquemas e conjuntos de dados, siga as etapas abaixo:

Selecione o **[!UICONTROL Esquemas]** localizada na navegação à esquerda e encontre o schema de entrada criado pelo script bootstrap. O nome do schema corresponderá ao que foi definido em `config.yaml` da etapa anterior. Visualize os detalhes do esquema e sua composição clicando nele.

![](../images/models-recipes/access-data/schema.PNG)

Selecione o **[!UICONTROL Conjuntos de dados]** localizada na navegação à esquerda e abra o conjunto de dados de entrada criado ao selecionar o nome do conjunto de dados. O nome do conjunto de dados corresponde ao que foi definido em `config.yaml` da etapa anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Selecionar **[!UICONTROL Visualizar conjunto de dados]** localizado na parte superior direita para visualizar um subconjunto do conjunto de dados.

![](../images/models-recipes/access-data/preview.PNG)

## Próximas etapas

Agora você assimilou com êxito os dados de amostra de Vendas de varejo no [!DNL Experience Platform] usando o script bootstrap fornecido.

Para continuar trabalhando com os dados assimilados:
- [Analise seus dados usando notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Usar notebooks jupyter em [!DNL Data Science Workspace] para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio modelo para o [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de Receita importável.
