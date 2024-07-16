---
title: Tipo de dados de pesquisa interna do site
description: Saiba mais sobre o tipo de dados XDM de pesquisa interna do site.
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Tipo de dados de [!UICONTROL Pesquisa Interna de Site]

[!UICONTROL Pesquisa Interna de Site] é um tipo de dados XDM padrão que descreve uma pesquisa interna de site, incluindo todos os comportamentos e detalhes de pesquisa relacionados.

![](../images/data-types/internal-site-search.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Booleano] | Indica se um visitante usou um valor de pesquisa sugerido ou preenchido automaticamente para executar a pesquisa. |
| `autoCompleteTypedValue` | [!UICONTROL String] | Para cenários de preenchimento automático, os usuários às vezes abandonam a pesquisa e selecionam um termo específico na lista suspensa. Esse valor rastreia o que o usuário começou a digitar para gerar o conjunto específico de termos de pesquisa sugeridos. |
| `autoCompleteValue` | [!UICONTROL String] | Para cenários de preenchimento automático, os usuários às vezes abandonam a pesquisa e selecionam um termo específico no menu suspenso. Esse valor é usado para rastrear os termos específicos selecionados. |
| `instances` | [!UICONTROL Inteiro] | O número de vezes que a pesquisa interna do site ocorreu. |
| `locationInPage` | [!UICONTROL String] | Quando existem várias caixas de pesquisa na página, esse valor deve ser usado para identificar o local específico que o usuário usou para pesquisar. |
| `nullInstances` | [!UICONTROL Inteiro] | O número de vezes que ocorreu a pesquisa interna do site que não forneceu resultados. |
| `numberOfResults` | [!UICONTROL Inteiro] | O número total de resultados da pesquisa retornados. |
| `postalCode` | [!UICONTROL String] | O código postal usado para a pesquisa, se aplicável. |
| `productFindingMethods` | [!UICONTROL String] | O valor do termo de pesquisa interna do site com vinculação de merchandising. Esse valor indica qual termo foi pesquisado imediatamente antes de visualizar um produto. |
| `radiusDistance` | [!UICONTROL Inteiro] | Combinado com `radiusType`, indica a distância selecionada do raio de pesquisa. |
| `radiusType` | [!UICONTROL Inteiro] | O tipo de distância selecionado de `radiusDistance`, seja milhas ou quilômetros. |
| `refinementInstances` | [!UICONTROL Inteiro] | O número de vezes que a pesquisa interna do site foi refinada. |
| `refinementType` | Matriz de cadeias de caracteres | Lista os tipos de refinamento aplicados aos resultados da pesquisa. Os exemplos incluem departamento, marca, preço, na loja, avaliação, cor, material e assim por diante. |
| `refinementValue` | [!UICONTROL String] | O valor para o qual a pesquisa foi refinada. |
| `resultsPageNumber` | [!UICONTROL Inteiro] | Para resultados de pesquisa paginados, esse valor rastreia a página de resultados que o visitante está visualizando. |
| `resultsPerPage` | [!UICONTROL Inteiro] | Para resultados de pesquisa paginados, esse valor rastreia o número de resultados de pesquisa exibidos por página. |
| `searchType` | [!UICONTROL String] | Registra o método de pesquisa que está sendo executado, se aplicável. Os exemplos podem incluir uma pesquisa com digitação antecipada, uma pesquisa digitada diretamente ou qualquer outro tipo de funcionalidade de pesquisa personalizada que um site possa ter. |
| `sortOrder` | [!UICONTROL String] | Combinado com `sortType`, indica a ordem de classificação dos resultados da pesquisa, crescente ou decrescente. |
| `term` | [!UICONTROL String] | O termo de pesquisa interna do site inserido pelo visitante. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
