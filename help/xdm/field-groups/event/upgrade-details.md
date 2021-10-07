---
title: Atualizar Detalhes do Grupo de Campos do Esquema
description: Este documento fornece uma visão geral do grupo de campos Detalhes da atualização.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---

# [!UICONTROL Grupo de campos Atualizar ] detalhes

[!UICONTROL Atualizar ] Detalhes é um grupo de campo de esquema padrão para a classe  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) usada para capturar informações relacionadas a um evento de marketing de atualização, incluindo detalhes sobre a transação e as diferentes maneiras em que a oferta foi exibida a um cliente.

O grupo de campos fornece um único campo do tipo objeto, `upgrades`. As propriedades contidas nesse objeto são explicadas abaixo.

![Estrutura de detalhes da atualização](../../images/field-groups/upgrade-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `upgradeImpressions` | Matriz de [Impressões](../../data-types/impressions.md) | Um storage que lista as impressões gravadas (exibições digitais ou participações com a oferta de atualização) para o cliente. |
| `upgradeTransaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda para a atualização. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
