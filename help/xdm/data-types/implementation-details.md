---
title: Tipo de dados de detalhes da implementação
description: Saiba mais sobre os detalhes da implementação do tipo de dados do Experience Data Model (XDM).
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
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

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
