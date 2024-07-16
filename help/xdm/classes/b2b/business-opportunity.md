---
title: Classe de oportunidade de negócios XDM
description: Saiba mais sobre a classe de Oportunidade comercial XDM no Experience Data Model (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# Classe [!UICONTROL Oportunidade de negócios XDM]

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso ao [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe do [Perfil de Cliente em Tempo Real](../../../profile/home.md).

A [!UICONTROL Oportunidade Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma oportunidade comercial.

![A estrutura da classe de Oportunidade Comercial XDM como aparece na interface do usuário](../../images/classes/b2b/business-opportunity.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto da conta à qual esta oportunidade está associada. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria de Sistema Source Externos]](../../data-types/external-source-system-audit-attributes.md) | Se a oportunidade vier de um sistema de origem externa, esse objeto capturará atributos de auditoria para esse sistema. |
| `opportunityKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto da entidade de oportunidade. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado de `opportunityID`. |
| `accountID` | String | Um identificador exclusivo para a conta à qual esta oportunidade está associada. |
| `isDeleted` | Booleano | Indica se esta entidade de lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar o [conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo serão refletidos automaticamente no Perfil do Cliente em Tempo Real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` como `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `opportunityDescription` | String | Uma descrição para a oportunidade. |
| `opportunityID` | String | Um identificador exclusivo para a entidade de oportunidade. |
| `opportunityName` | String | O nome da oportunidade. |
| `opportunityStage` | String | O estágio de vendas da oportunidade. |
| `opportunityType` | String | O tipo de oportunidade. |

{style="table-layout:auto"}

Consulte o manual sobre [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer essas relações na interface do usuário do Adobe Experience Platform.
