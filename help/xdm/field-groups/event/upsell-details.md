---
title: Grupo de Campos do Esquema de Detalhes da Venda Superior
description: Este documento fornece uma visão geral do grupo de campos Detalhes da venda adicional.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL Grupo de campos ] Detalhes da venda adicional

[!UICONTROL Upsell ] Details é um grupo de campo de esquema padrão para a classe  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) usada para capturar informações sobre um evento de marketing de upsell, incluindo detalhes sobre a transação e as diferentes maneiras em que a oferta foi exibida a um cliente.

O grupo de campos fornece um único campo do tipo objeto, `upsells`. As propriedades contidas nesse objeto são explicadas abaixo.

![Estrutura de detalhes da venda adicional](../../images/field-groups/upsell-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `upsellImpressions` | Matriz de [Impressões](../../data-types/impressions.md) | Um storage que lista as impressões gravadas (visualizações digitais ou participações com a oferta de venda adicional) para o cliente. |
| `upsellTransaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda da venda adicional. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
