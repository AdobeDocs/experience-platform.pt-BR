---
keywords: Experience Platform;visualizar dados do esquema;Data Science Workspace;tópicos populares;;preview schema data;Data Science;popular topics
solution: Experience Platform
title: Visualizar o Esquema de Vendas de Varejo e o Conjunto de Dados
type: Tutorial
description: O documento a seguir descreve a visualização de esquemas e conjuntos de dados no Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# Visualizar o esquema de vendas de varejo e o conjunto de dados

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Após a conclusão bem-sucedida do script de inicialização do [esquema de vendas de varejo e tutorial de conjunto de dados](./create-retails-sales-dataset.md). Esquemas de saída e conjuntos de dados podem ser exibidos em [!DNL Experience Platform]. Para exibir os esquemas e conjuntos de dados, siga as etapas abaixo:

Selecione a guia **[!UICONTROL Schemas]**, localizada na navegação à esquerda, e localize o esquema de entrada criado pelo script de inicialização. O nome do esquema corresponderá ao que foi definido em `config.yaml` na etapa anterior. Exiba os detalhes do esquema e sua composição clicando nele.

![](../images/models-recipes/access-data/schema.PNG)

Selecione a guia **[!UICONTROL Datasets]**, localizada na navegação à esquerda, e abra o conjunto de dados de entrada criado selecionando o nome do conjunto de dados. O nome do conjunto de dados corresponde ao que foi definido em `config.yaml` na etapa anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Selecione **[!UICONTROL Preview Dataset]**, localizado no canto superior direito, para visualizar um subconjunto do conjunto de dados.

![](../images/models-recipes/access-data/preview.PNG)

## Próximas etapas

Você assimilou com êxito dados de amostra de Vendas de Varejo em [!DNL Experience Platform] usando o script de inicialização fornecido.

Para continuar trabalhando com os dados assimilados:

- [Analise dados usando o Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Use o Jupyter Notebooks no [!DNL Data Science Workspace] para acessar, explorar, visualizar e entender seus dados.
- [Compactar arquivos de origem em uma fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para saber como trazer seu próprio Modelo para o [!DNL Data Science Workspace] empacotando arquivos de origem em um arquivo de Receita importável.
