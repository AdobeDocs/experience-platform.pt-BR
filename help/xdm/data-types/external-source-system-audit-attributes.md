---
title: Tipo de Dados de Atributos de Auditoria do Sistema Source Externo
description: Saiba mais sobre o tipo de dados External Source System Audit Attributes Experience Data Model (XDM).
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# [!UICONTROL Tipo de dados de Atributos de Auditoria do Sistema Source Externo]

[!UICONTROL Atributos de Auditoria de Sistema Externos do Source] é um tipo de dados padrão do Experience Data Model (XDM) que captura detalhes de auditoria sobre um sistema de origem externo.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Source B2B]](./b2b-source.md) | Um identificador composto para a origem usada para auditoria. |
| `createdBy` | String | O nome do usuário que criou este registro. |
| `createdDate` | DateTime | A data em que este registro foi criado. |
| `externalID` | String | Identificador exclusivo externo da origem. Esse valor é usado para ajudar a identificar e desduplicar, se necessário. |
| `lastActivityDate` | DateTime | A última data de atividade do sistema de origem. |
| `lastReferencedDate` | DateTime | A última data referenciada para o sistema de origem. |
| `lastUpdatedBy` | String | O nome da pessoa que atualizou este registro pela última vez. |
| `lastUpdatedDate` | DateTime | A data da última atualização do sistema de origem. Este valor é usado pela [política de mesclagem de atributos](../../profile/api/merge-policies.md#attribute-merge) para determinar a prioridade em caso de conflitos de mesclagem. |
| `lastViewedDate` | DateTime | A última data exibida para o sistema de origem. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)
