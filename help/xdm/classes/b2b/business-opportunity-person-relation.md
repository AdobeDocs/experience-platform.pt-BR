---
title: Classe de relação pessoal de oportunidade de negócios XDM
description: Saiba mais sobre a classe de relação pessoal de oportunidade de negócios XDM no Experience Data Model (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 3%

---

# [!UICONTROL Relação pessoal de oportunidade de negócios XDM] classe

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Relação pessoal de oportunidade de negócios XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma pessoa associada a uma oportunidade de negócios.

![A estrutura da classe de pessoa de oportunidade de negócios XDM como aparece na interface do usuário](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de auditoria do sistema de origem externa]](../../data-types/external-source-system-audit-attributes.md) | Se a relação comercial vem de um sistema de origem externa, esse objeto captura atributos de auditoria para esse sistema. |
| `opportunityKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da oportunidade no relacionamento oportunidade-pessoa. |
| `opportunityPersonKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade de relação oportunidade-pessoa. |
| `personKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto da pessoa no relacionamento oportunidade-pessoa. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado dos outros campos de ID capturados pela classe. |
| `isDeleted` | Booleano | Indica se esta entidade de lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar o [Conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `isPrimary` | Booleano | Indica se a pessoa é o contato principal desta oportunidade. |
| `opportunityID` | String | Um identificador exclusivo da oportunidade no relacionamento oportunidade-pessoa. |
| `opportunityPersonID` | String | Um identificador exclusivo da entidade de relação oportunidade-pessoa |
| `personID` | String | Um identificador exclusivo da pessoa no relacionamento oportunidade-pessoa. |
| `personRole` | String | A função da pessoa no relacionamento oportunidade-pessoa. |

{style="table-layout:auto"}

Consulte o guia sobre [relacionamentos de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
