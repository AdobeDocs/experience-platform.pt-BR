---
title: Tipo de dados de origem B2B
description: Saiba mais sobre o tipo de dados Modelo de dados de experiência de origem B2B (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# [!UICONTROL Origem B2B] tipo de dados

[!UICONTROL Origem B2B] é um tipo de dados padrão do Experience Data Model (XDM) que representa um identificador composto de uma entidade B2B (como uma [account](../classes/b2b/business-account.md), um [oportunidade](../classes/b2b/business-opportunity.md), ou um [campaign](../classes/b2b/business-campaign.md)).

Ao depender apenas de identificadores baseados em sequência, pode haver sobreposições entre IDs em vários sistemas (por exemplo, uma oportunidade pode receber uma ID de sequência em um sistema de CRM, mas essa mesma ID pode se referir a uma oportunidade completamente diferente). Isso pode resultar em conflitos de dados ao mesclar dados no [Perfil do cliente em tempo real](../../profile/home.md).

A variável [!UICONTROL Origem B2B] O tipo de dados permite usar a ID de sequência original de uma entidade e combiná-la com informações contextuais específicas da origem para garantir que ela permaneça totalmente exclusiva no sistema da Platform, independentemente da origem de onde foi originada.

![Estrutura de origem B2B](../images/data-types/b2b-source.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sourceID` | String | Uma ID exclusiva para o registro de origem. |
| `sourceInstanceID` | String | A ID da instância ou organização dos dados de origem. |
| `sourceKey` | String | Um identificador exclusivo composto por `sourceId`, `sourceInstanceId`, e `sourceType` concatenados no seguinte formato: `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Alguns conectores de origem, como o Marketo, concatenam esse valor automaticamente para determinados identificadores. Outros devem ser concatenados manualmente usando o [Preparação de dados `concat` função](../../data-prep/functions.md#string), por exemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | O nome da plataforma que fornece os dados de origem. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
