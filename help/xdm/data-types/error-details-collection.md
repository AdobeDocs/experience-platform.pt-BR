---
title: Tipo de Dados de Coleta de Detalhes do Erro
description: Saiba mais sobre o tipo de dados XDM (Error Details Collection Experience Data Model).
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Detalhes do erro] Tipo de dados de coleção

[!UICONTROL Detalhes do erro] A coleção é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes do erro. Use o [!UICONTROL Detalhes do erro] Tipo de dados de coleção para capturar detalhes da fonte de erro e identificação. A ID do erro identifica o erro e a origem do erro especifica se ele é do reprodutor ou de uma origem externa.

![Um diagrama do tipo de dados Informações sobre Detalhes do Erro.](../images/data-types/error-details-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID do erro] | `name` | string | Não | A ID do erro. |
| [!UICONTROL Origem do erro] | `source` | string | Não | A origem do erro. Enumerado: &quot;player&quot;, &quot;external&quot; com respectivos significados. |

{style="table-layout:auto"}
