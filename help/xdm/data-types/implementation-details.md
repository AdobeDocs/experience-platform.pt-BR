---
title: Tipo de dados de detalhes da implementação
description: Este documento fornece uma visão geral dos detalhes de Implementação do tipo de dados do Experience Data Model (XDM).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# [!UICONTROL Detalhes da implementação] tipo de dados

[!UICONTROL Detalhes da implementação] é um tipo de dados padrão do Experience Data Model (XDM) que descreve uma implementação de tecnologia, como uma API ou um SDK.

![Estrutura do tipo de dados](../images/data-types/implementation-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `environment` | String | O ambiente da implementação. |
| `name` | String | O identificador do SDK ou endpoint. Todos os SDKs ou endpoints são identificados por meio de um URI, incluindo extensões. |
| `version` | String | A versão da API ou do SDK. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
