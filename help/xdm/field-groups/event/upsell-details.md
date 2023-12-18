---
title: Grupo de Campos de Esquema de Detalhes de Venda Adicional
description: Saiba mais sobre o grupo de campos de esquema Detalhes da venda adicional.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Detalhes de venda adicional] grupo de campos de esquema

[!UICONTROL Detalhes de venda adicional] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para registrar informações sobre um evento de marketing de venda adicional, incluindo detalhes sobre a transação e as diferentes maneiras como a oferta foi exibida para um cliente.

O grupo de campos fornece um único campo do tipo objeto, `upsells`. As propriedades contidas nesse objeto são explicadas abaixo.

![Estrutura de detalhes de venda adicional](../../images/field-groups/upsell-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `upsellImpressions` | Matriz de [Impressões](../../data-types/impressions.md) | Um storage que lista as impressões gravadas (visualizações digitais ou compromissos com a oferta de venda adicional) do cliente. |
| `upsellTransaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda para a venda adicional. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
