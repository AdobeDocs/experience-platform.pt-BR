---
title: Classe de conta de negócios XDM
description: Saiba mais sobre a classe Conta comercial XDM no Experience Data Model (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# Classe [!UICONTROL Conta Comercial XDM]

>[!IMPORTANT]
>
>Esta classe deve ser usada por organizações com acesso ao [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Você deve ter acesso ao Real-Time CDP B2B Edition para que esta classe participe do [Perfil de Cliente em Tempo Real](../../../profile/home.md).

A [!UICONTROL Conta Comercial XDM] é uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma conta comercial.

![A estrutura da classe de Conta Comercial XDM como aparece na interface do usuário](../../images/classes/b2b/business-account.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Um identificador composto da entidade da conta. |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria de Sistema Source Externos]](../../data-types/external-source-system-audit-attributes.md) | Se a conta vem de um sistema de origem externa, esse objeto captura atributos de auditoria para esse sistema. |
| `_id` | String | Um identificador exclusivo do registro. Este é um valor gerado pelo sistema separado do identificador `accountKey`. |
| `isDeleted` | Booleano | Indica se esta entidade de conta foi excluída no Marketo Engage.<br><br>Ao usar o [conector de origem do Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), todos os registros excluídos no Marketo serão refletidos automaticamente no Perfil do Cliente em Tempo Real. No entanto, os registros relacionados a esses perfis ainda podem persistir no Data Lake. Ao configurar `isDeleted` como `true`, você pode usar o campo para filtrar quais registros foram excluídos de suas fontes ao consultar o Data Lake. |

{style="table-layout:auto"}

Consulte o manual sobre [relações de esquema no Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) para saber como essa classe se relaciona conceitualmente com as outras classes B2B e como você pode estabelecer essas relações na interface do usuário do Adobe Experience Platform.
