---
title: Grupo de Campos de Esquema de Detalhes de Atualização
description: Saiba mais sobre o grupo de campos de esquema Detalhes da atualização.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Detalhes da atualização] grupo de campos de esquema

[!UICONTROL Detalhes de Atualização] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usada para capturar informações sobre um evento de marketing de atualização, incluindo detalhes sobre a transação e as diferentes maneiras das quais a oferta foi exibida para um cliente.

O grupo de campos fornece um único campo de tipo de objeto, `upgrades`. As propriedades contidas nesse objeto são explicadas abaixo.

![Estrutura de Detalhes da Atualização](../../images/field-groups/upgrade-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `upgradeImpressions` | Matriz de [Impressões](../../data-types/impressions.md) | Um storage que lista as impressões gravadas (visualizações digitais ou compromissos com a oferta de atualização) do cliente. |
| `upgradeTransaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda da atualização. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
