---
title: Tipo de dados de atributos de auditoria do sistema de origem externa
description: Saiba mais sobre o tipo de dados Atributos de auditoria do sistema de origem externa Experience Data Model (XDM).
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 4%

---

# [!UICONTROL Atributos de auditoria do sistema de origem externa] tipo de dados

[!UICONTROL Atributos de auditoria do sistema de origem externa] é um tipo de dados padrão do Experience Data Model (XDM) que captura os detalhes de auditoria sobre um sistema de origem externa.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Origem B2B]](./b2b-source.md) | Um identificador composto para a origem usada para auditoria. |
| `createdBy` | String | O nome do usuário que criou este registro. |
| `createdDate` | DateTime | A data em que este registro foi criado. |
| `externalID` | String | Identificador exclusivo externo da origem. Esse valor é usado para ajudar a identificar e desduplicar, se necessário. |
| `lastActivityDate` | DateTime | A última data de atividade do sistema de origem. |
| `lastReferencedDate` | DateTime | A última data referenciada para o sistema de origem. |
| `lastUpdatedBy` | String | O nome da pessoa que atualizou este registro pela última vez. |
| `lastUpdatedDate` | DateTime | A data da última atualização do sistema de origem. |
| `lastViewedDate` | DateTime | A última data exibida para o sistema de origem. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
