---
title: Classe da Lista de Marketing Comercial XDM
description: Este documento fornece uma visão geral da classe de Lista de Marketing de Negócios XDM no Experience Data Model (XDM).
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 3%

---

# [!UICONTROL Lista de marketing comercial XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso à CDP B2B Edition em tempo real para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Lista de marketing comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma lista de marketing. As listas de marketing permitem priorizar clientes potenciais com maior probabilidade de comprar seu produto.

![A estrutura da classe de lista de negócios XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-marketing-list.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a lista de marketing for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `marketingListKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade da lista de marketing. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `marketingListID`. |
| `isDeleted` | Booleano | Indica se esta entidade da lista de marketing foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |
| `marketingListDescription` | String | Uma descrição para a lista de marketing. |
| `marketingListID` | String | Uma ID exclusiva para a entidade da lista de marketing. |
| `marketingListName` | String | O nome da lista de marketing. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema na Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
