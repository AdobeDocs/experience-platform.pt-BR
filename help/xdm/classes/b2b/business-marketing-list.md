---
title: Classe da lista de marketing de negócios XDM
description: Saiba mais sobre a classe Lista de marketing empresarial XDM no Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Classe [!UICONTROL Lista de Marketing Comercial XDM]

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso ao [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe do [Perfil de Cliente em Tempo Real](../../../profile/home.md).

A [!UICONTROL Lista de Marketing Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma lista de marketing. As listas de marketing permitem que você priorize os clientes em potencial com maior probabilidade de comprar seu produto.

![A estrutura da classe da Lista de Marketing Comercial XDM como aparece na interface do usuário](../../images/classes/b2b/business-marketing-list.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria de Sistema Source Externos]](../../data-types/external-source-system-audit-attributes.md) | Se a lista de marketing for proveniente de um sistema de origem externa, esse objeto capturará os atributos de auditoria desse sistema. |
| `marketingListKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade da lista de marketing. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado de `marketingListID`. |
| `isDeleted` | Booleano | Indica se esta entidade de lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar o [conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo serão refletidos automaticamente no Perfil do Cliente em Tempo Real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` como `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `marketingListDescription` | String | Uma descrição para a lista de marketing. |
| `marketingListID` | String | Uma ID exclusiva para a entidade da lista de marketing. |
| `marketingListName` | String | O nome da lista de marketing. |

{style="table-layout:auto"}

Consulte o manual sobre [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer essas relações na interface do usuário do Adobe Experience Platform.
