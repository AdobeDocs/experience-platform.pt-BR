---
title: Classe de Conta Comercial XDM
description: Este documento fornece uma visão geral da classe de conta comercial XDM no Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---

# [!UICONTROL Conta Comercial XDM] classe

>[!IMPORTANT]
>
>Esta classe destina-se a ser utilizada por organizações com acesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que essa classe participe do [Perfil do cliente em tempo real](../../../profile/home.md).

[!UICONTROL Conta Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma conta comercial.

![A estrutura da classe de conta comercial XDM como ela aparece na interface do usuário](../../images/classes/b2b/business-account.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade da conta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a conta for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo para o registro. Esse é um valor gerado pelo sistema separado da variável `accountKey` identificador. |
| `isDeleted` | Booleano | Indica se esta entidade de conta foi excluída no Marketo Engage.<br><br>Ao usar a variável [Conector de origem Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo são refletidos automaticamente no Perfil do cliente em tempo real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` para `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer esses relacionamentos na interface do usuário do Adobe Experience Platform.
