---
keywords: Experience Platform;visualizar dados do esquema;Espaço de trabalho de ciência de dados;tópicos populares
solution: Experience Platform
title: Visualizar o Esquema de Vendas de Varejo e o Conjunto de Dados
type: Tutorial
description: O documento a seguir descreve a visualização de esquemas e conjuntos de dados no Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Visualizar o esquema de vendas de varejo e o conjunto de dados

Após a conclusão bem-sucedida do script de inicialização do [esquema e conjunto de dados de vendas de varejo](./create-retails-sales-dataset.md) tutorial. Esquemas de saída e conjuntos de dados podem ser exibidos em [!DNL Experience Platform]. Para exibir os esquemas e conjuntos de dados, siga as etapas abaixo:

Selecione o **[!UICONTROL Esquemas]** localizada na navegação à esquerda e localize o schema de entrada criado pelo script de inicialização. O nome do schema corresponderá ao que foi definido em `config.yaml` da etapa anterior. Exiba os detalhes do esquema e sua composição clicando nele.

![](../images/models-recipes/access-data/schema.PNG)

Selecione o **[!UICONTROL Conjuntos de dados]** localizada na navegação à esquerda e abra o conjunto de dados de entrada criado selecionando o nome do conjunto de dados. O nome do conjunto de dados corresponde ao que foi definido em `config.yaml` da etapa anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Selecionar **[!UICONTROL Visualizar conjunto de dados]** localizado no canto superior direito para visualizar um subconjunto do conjunto de dados.

![](../images/models-recipes/access-data/preview.PNG)

## Próximas etapas

Você assimilou com êxito dados de amostra de Vendas de varejo em [!DNL Experience Platform] usando o script de inicialização fornecido.

Para continuar trabalhando com os dados assimilados:
- [Analise seus dados usando o Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Usar o Jupyter Notebooks no [!DNL Data Science Workspace] para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio modelo para o [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de fórmula importável.
