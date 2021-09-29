---
title: Tipo de Dados de Origem B2B
description: Este documento fornece uma visão geral do tipo de dados do Modelo de Dados de Experiência de Origem B2B (XDM).
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 2%

---

# [!UICONTROL Tipo de ] fonte B2B (Beta)

>[!IMPORTANT]
>
>Esse tipo de dados está disponível como parte da Real-time Customer Data Platform B2B Edition, que está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!UICONTROL Fontes B2B ] é um tipo de dados padrão do Experience Data Model (XDM) que representa um identificador composto para uma entidade B2B (como uma  [conta](../classes/b2b/business-account.md), uma  [oportunidade](../classes/b2b/business-opportunity.md) ou uma  [campanha](../classes/b2b/business-campaign.md)).

Ao depender exclusivamente de identificadores baseados em sequência, pode haver sobreposições entre IDs em vários sistemas (por exemplo, uma oportunidade pode receber uma ID de sequência em um sistema de CRM, mas essa mesma ID pode se referir a uma oportunidade completamente diferente). Isso pode resultar em conflitos de dados ao mesclar dados em [Perfil do cliente em tempo real](../../profile/home.md).

O tipo de dados [!UICONTROL B2B Source] permite usar a ID da cadeia de caracteres original de uma entidade e combiná-la com informações contextuais específicas da fonte para garantir que ela permaneça totalmente exclusiva no sistema da Plataforma, independentemente da fonte da qual ela se originou.

![Estrutura de Origem B2B](../images/data-types/b2b-source.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `sourceID` | String | Uma ID exclusiva para o registro de origem. |
| `sourceInstanceID` | String | A ID da instância ou da organização dos dados de origem. |
| `sourceKey` | String | Um identificador exclusivo composto por `sourceId`, `sourceInstanceId` e `sourceType` concatenado no seguinte formato: `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Alguns conectores de origem como o Marketo concatenam esse valor automaticamente para determinados identificadores. Outros devem ser concatenados manualmente usando a função [Data Prep `concat`](../../data-prep/functions.md#string), por exemplo: `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | String | O nome da plataforma que fornece os dados de origem. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
