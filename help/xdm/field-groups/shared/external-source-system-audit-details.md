---
title: Detalhes de auditoria sobre sistema de origem externo
description: Saiba mais sobre o grupo de campos External Source System Audit Details Experience Data Model (XDM).
source-git-commit: 656070cf69e3713c7889f53d51937e0e70085d96
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# [!UICONTROL Detalhes de auditoria externa do sistema Source] grupo de campos

[!UICONTROL Detalhes de auditoria do sistema Source externo] é um grupo de campos padrão do Experience Data Model (XDM) que estende o tipo de dados principal &#39;Atributos de auditoria do sistema Source externo&#39; referenciando suas propriedades e adicionando metadados contextuais. Isso permite o rastreamento detalhado de auditoria e a integração flexível de dados de fontes externas.

![Um diagrama de esquema do grupo de campos Detalhes de Auditoria do Sistema Source Externo.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL Detalhes de auditoria externa do sistema Source] | `external-source-system-audit-details` | [[!UICONTROL Atributos de Auditoria de Sistema Source Externos]](../../data-types/external-source-system-audit-attributes.md) | O grupo de campos &#39;[!UICONTROL Detalhes de Auditoria Externa do Source System]&#39; estende o tipo de dados principal &#39;Atributos de Auditoria Externa do Source System&#39; referenciando suas propriedades e adicionando metadados contextuais. Isso facilita o rastreamento detalhado de auditoria e a integração flexível de dados para fontes externas, acomodando a natureza assíncrona da assimilação de perfis. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)