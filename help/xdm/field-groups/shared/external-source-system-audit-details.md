---
title: Detalhes de auditoria externa do sistema Source
description: Saiba mais sobre o grupo de campos External Source System Audit Details Experience Data Model (XDM).
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 4%

---

# Grupo de campos [!UICONTROL External Source System Audit Details]

[!UICONTROL External Source System Audit Details] é um grupo de campos padrão do Experience Data Model (XDM) que estende o tipo de dados principal &quot;Atributos de Auditoria de Sistema do Source Externo&quot; referenciando suas propriedades e adicionando metadados contextuais. Isso permite o rastreamento detalhado de auditoria e a integração flexível de dados de fontes externas.

![Um diagrama de esquema do grupo de campos Detalhes de Auditoria do Sistema Source Externo.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL External Source System Audit Details] | `external-source-system-audit-details` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | O grupo de campos &#39;[!UICONTROL External Source System Audit Details]&#39; estende o tipo de dados principal &#39;Atributos de Auditoria de Sistema Source Externos&#39; referenciando suas propriedades e adicionando metadados contextuais. Isso facilita o rastreamento detalhado de auditoria e a integração flexível de dados para fontes externas, acomodando a natureza assíncrona da assimilação de perfis. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)
