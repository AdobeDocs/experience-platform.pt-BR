---
title: Tipo de Dados de Informações de Detalhes do Erro
description: Saiba mais sobre o tipo de dados do Modelo de dados de experiência (XDM) de detalhes de erros.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 5%

---

# [!UICONTROL Informações de Detalhes do Erro] tipo de dados

[!UICONTROL Informações de Detalhes do Erro] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes do erro. Use o [!UICONTROL Informações de Detalhes do Erro] tipo de dados para capturar detalhes da fonte de erro e identificação. A ID do erro identifica o erro e a origem do erro especifica se ele é do reprodutor ou de uma origem externa.

![Um diagrama do tipo de dados Informações sobre Detalhes do Erro.](../images/data-types/error-details-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL ID do erro] | `name` | string | A ID do erro. |
| [!UICONTROL Origem do erro] | `source` | string | A origem do erro. Enumerado: &quot;player&quot;, &quot;external&quot; com respectivos significados. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
