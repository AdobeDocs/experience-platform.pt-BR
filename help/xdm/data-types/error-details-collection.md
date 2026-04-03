---
title: Tipo de Dados de Coleta de Detalhes do Erro
description: Saiba mais sobre o tipo de dados XDM (Error Details Collection Experience Data Model).
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# [!UICONTROL Error Details] Tipo de dados da coleção

A Coleção [!UICONTROL Error Details] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes do erro. Use o tipo de dados da Coleção [!UICONTROL Error Details] para capturar detalhes da fonte e da identificação do erro. A ID do erro identifica o erro e a origem do erro especifica se ele é do reprodutor ou de uma origem externa.

![Um diagrama do tipo de dados Informações sobre Detalhes do Erro.](../images/data-types/error-details-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | sequência de caracteres | Não | A ID do erro. |
| [!UICONTROL Error Source] | `source` | sequência de caracteres | Não | A origem do erro. Enumerado: &quot;player&quot;, &quot;external&quot; com respectivos significados. |

{style="table-layout:auto"}
