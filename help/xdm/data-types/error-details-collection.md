---
title: Tipo de Dados de Coleta de Detalhes do Erro
description: Saiba mais sobre o tipo de dados XDM (Error Details Collection Experience Data Model).
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL Tipo de dados da coleção de Detalhes do Erro]

A Coleção [!UICONTROL Detalhes do Erro] é um tipo de dados padrão do Experience Data Model (XDM) que descreve os detalhes do erro. Use o tipo de dados Coleção [!UICONTROL Detalhes do Erro] para capturar detalhes da fonte e da identificação do erro. A ID do erro identifica o erro e a origem do erro especifica se ele é do reprodutor ou de uma origem externa.

![Um diagrama do tipo de dados Informações sobre Detalhes do Erro.](../images/data-types/error-details-collection.png)

| Nome de exibição | Propriedade | Tipo de dados | Obrigatório | Descrição |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID do erro] | `name` | sequência de caracteres | Não | A ID do erro. |
| [!UICONTROL Source com erro] | `source` | sequência de caracteres | Não | A origem do erro. Enumerado: &quot;player&quot;, &quot;external&quot; com respectivos significados. |

{style="table-layout:auto"}
