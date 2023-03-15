---
title: Grupo de Campos de Esquema de Detalhes de Atualização
description: Este documento fornece uma visão geral do grupo de campos do esquema Detalhes da Atualização.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---

# [!UICONTROL Detalhes da atualização] grupo de campos de esquema

[!UICONTROL Detalhes da atualização] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para registrar informações sobre um evento de marketing de atualização, incluindo detalhes sobre a transação e as diferentes maneiras como a oferta foi exibida para um cliente.

O grupo de campos fornece um único campo do tipo objeto, `upgrades`. As propriedades contidas nesse objeto são explicadas abaixo.

![Atualizar estrutura de detalhes](../../images/field-groups/upgrade-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `upgradeImpressions` | Matriz de [Impressões](../../data-types/impressions.md) | Um storage que lista as impressões gravadas (visualizações digitais ou compromissos com a oferta de atualização) do cliente. |
| `upgradeTransaction` | [Transação](../../data-types/transaction.md) | Descreve a transação de moeda da atualização. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
