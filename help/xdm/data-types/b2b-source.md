---
title: Tipo de dados do Source B2B
description: Saiba mais sobre o tipo de dados B2B Source Experience Data Model (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# Tipo de dados [!UICONTROL B2B Source]

[!UICONTROL Source B2B] é um tipo de dados padrão do Experience Data Model (XDM) que representa um identificador composto para uma entidade B2B (como uma [conta](../classes/b2b/business-account.md), uma [oportunidade](../classes/b2b/business-opportunity.md) ou uma [campanha](../classes/b2b/business-campaign.md)).

Ao depender apenas de identificadores baseados em sequência, pode haver sobreposições entre IDs em vários sistemas (por exemplo, uma oportunidade pode receber uma ID de sequência em um sistema de CRM, mas essa mesma ID pode se referir a uma oportunidade completamente diferente). Isso pode resultar em conflitos de dados ao mesclar dados no [Perfil de Cliente em Tempo Real](../../profile/home.md).

O tipo de dados [!UICONTROL B2B Source] permite usar a ID de cadeia de caracteres original de uma entidade e combiná-la com informações contextuais específicas da origem para garantir que ela permaneça totalmente exclusiva no sistema Experience Platform, independentemente da origem de onde ela foi originada.

![Estrutura B2B do Source](../images/data-types/b2b-source.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sourceID` | String | Uma ID exclusiva para o registro de origem. |
| `sourceInstanceID` | String | A ID da instância ou organização dos dados de origem. |
| `sourceKey` | String | Um identificador exclusivo composto por `sourceId`, `sourceInstanceId` e `sourceType` concatenados juntos no seguinte formato: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Alguns conectores de origem, como o Marketo, concatenam esse valor automaticamente para determinados identificadores. Outros devem ser concatenados manualmente usando a [função de Preparo de Dados `concat`](../../data-prep/functions.md#string), por exemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | O nome da plataforma que fornece os dados de origem. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
