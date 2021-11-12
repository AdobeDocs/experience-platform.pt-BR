---
title: Tipo de Dados de Origem B2B
description: Este documento fornece uma visão geral do tipo de dados do Modelo de Dados de Experiência de Origem B2B (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 3%

---

# [!UICONTROL Origem B2B] tipo de dados

[!UICONTROL Origem B2B] é um tipo de dados padrão do Experience Data Model (XDM) que representa um identificador composto para uma entidade B2B (como um [account](../classes/b2b/business-account.md), um [oportunidade](../classes/b2b/business-opportunity.md)ou um [campanha](../classes/b2b/business-campaign.md)).

Ao depender exclusivamente de identificadores baseados em sequência, pode haver sobreposições entre IDs em vários sistemas (por exemplo, uma oportunidade pode receber uma ID de sequência em um sistema de CRM, mas essa mesma ID pode se referir a uma oportunidade completamente diferente). Isso pode resultar em conflitos de dados ao mesclar dados em [Perfil do cliente em tempo real](../../profile/home.md).

O [!UICONTROL Origem B2B] o tipo de dados permite usar a ID da string original de uma entidade e combiná-la com informações contextuais específicas de fonte para garantir que permaneça totalmente exclusiva no sistema da plataforma, independentemente da fonte da qual ela se originou.

![Estrutura de Origem B2B](../images/data-types/b2b-source.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sourceID` | String | Uma ID exclusiva para o registro de origem. |
| `sourceInstanceID` | String | A ID da instância ou da organização dos dados de origem. |
| `sourceKey` | String | Um identificador exclusivo composto pela variável `sourceId`, `sourceInstanceId`e `sourceType` concatenadas no seguinte formato: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Alguns conectores de origem como o Marketo concatenam esse valor automaticamente para determinados identificadores. Outros devem ser concatenados manualmente usando o [Preparação de dados `concat` função](../../data-prep/functions.md#string), por exemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | O nome da plataforma que fornece os dados de origem. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
