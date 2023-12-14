---
title: Tipo de Dados de Informações de Detalhes de Metadados Personalizados
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência (XDM) de informações de detalhes de metadados personalizados.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# [!UICONTROL Informações sobre detalhes de metadados personalizados] tipo de dados

[!UICONTROL Informações sobre detalhes de metadados personalizados] é um tipo de dados padrão do Experience Data Model (XDM) que define uma estrutura para armazenar metadados personalizados. Use o [!UICONTROL Informações sobre detalhes de metadados personalizados] tipo de dados para capturar detalhes como o nome e o valor dos metadados personalizados associados ao conteúdo ou às interações.

![Um diagrama do tipo de dados Informações de detalhes de metadados personalizados.](../images/data-types/custom-metadata-details-information.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nome do campo de metadados personalizado] | `name` | string | O nome do campo personalizado. |
| [!UICONTROL Valor do campo de metadados personalizado] | `value` | string | O valor do campo personalizado. |

{style="table-layout:auto"}

Para obter mais informações sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
