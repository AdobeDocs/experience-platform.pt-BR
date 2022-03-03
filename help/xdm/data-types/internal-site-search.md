---
title: Tipo de Dados de Pesquisa de Site Interno
description: Este documento fornece uma visão geral do tipo de dados XDM de pesquisa interna do site.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!UICONTROL Pesquisa interna do site] tipo de dados

[!UICONTROL Pesquisa interna do site] é um tipo de dados XDM padrão que descreve uma pesquisa interna do site, incluindo todos os comportamentos e detalhes de pesquisa relacionados.

![](../images/data-types/internal-site-search.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Booleano] | Indica se um visitante usou um valor de pesquisa sugerido ou preenchido automaticamente para executar a pesquisa. |
| `autoCompleteTypedValue` | [!UICONTROL String] | Para cenários de preenchimento automático, os usuários às vezes abandonam a pesquisa e selecionam um termo específico na lista suspensa. Esse valor rastreia o que o usuário começou a digitar para gerar o conjunto específico de termos de pesquisa sugeridos. |
| `autoCompleteValue` | [!UICONTROL String] | Para cenários de preenchimento automático, os usuários às vezes abandonam a pesquisa e selecionam um termo específico no menu suspenso. Esse valor é usado para rastrear os termos específicos selecionados. |
| `instances` | [!UICONTROL Número inteiro] | O número de vezes que a pesquisa interna do site ocorreu. |
| `locationInPage` | [!UICONTROL String] | Quando existem várias caixas de pesquisa na página, esse valor deve ser usado para identificar o local específico que o usuário usou para pesquisar. |
| `nullInstances` | [!UICONTROL Número inteiro] | O número de vezes que ocorreu a pesquisa interna do site que forneceu resultados zero. |
| `numberOfResults` | [!UICONTROL Número inteiro] | O número total de resultados de pesquisa retornados. |
| `postalCode` | [!UICONTROL String] | O código postal utilizado para a pesquisa, se aplicável. |
| `productFindingMethods` | [!UICONTROL String] | O valor do termo de pesquisa interna do site com vínculo de comercialização. Esse valor indica qual termo foi procurado imediatamente antes de visualizar um produto. |
| `radiusDistance` | [!UICONTROL Número inteiro] | Combinado com `radiusType`, indica a distância selecionada do raio de pesquisa. |
| `radiusType` | [!UICONTROL Número inteiro] | O tipo de distância selecionado de `radiusDistance`, em milhas ou quilômetros. |
| `refinementInstances` | [!UICONTROL Número inteiro] | O número de vezes que a pesquisa interna do site foi refinada. |
| `refinementType` | Matriz de cadeias de caracteres | Lista os tipos de refinamento aplicados aos resultados da pesquisa. Os exemplos incluem departamento, marca, preço, na loja, classificação de revisão, cor, material e assim por diante. |
| `refinementValue` | [!UICONTROL String] | O valor para o qual a pesquisa foi refinada. |
| `resultsPageNumber` | [!UICONTROL Número inteiro] | Para resultados de pesquisa paginada, esse valor rastreia a página de resultados que o visitante está visualizando. |
| `resultsPerPage` | [!UICONTROL Número inteiro] | Para resultados de pesquisa paginada, esse valor rastreia o número de resultados de pesquisa exibidos por página. |
| `searchType` | [!UICONTROL String] | Captura o método de pesquisa que está sendo executado, se aplicável. Os exemplos podem incluir uma pesquisa do tipo antecipada, uma pesquisa diretamente digitada ou qualquer outro tipo de funcionalidade de pesquisa personalizada que um site possa ter. |
| `sortOrder` | [!UICONTROL String] | Combinado com `sortType`, indica a ordem de classificação dos resultados da pesquisa, crescente ou decrescente. |
| `term` | [!UICONTROL String] | O termo interno de pesquisa do site inserido pelo visitante. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
