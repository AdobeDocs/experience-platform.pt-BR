---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de Campos de Esquema de Detalhes do Canal
description: Este documento fornece uma visão geral do grupo de campos de esquema Detalhes do canal.
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%

---

# [!UICONTROL Detalhes do canal] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes do canal] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever informações de canal, como ID, tipo de canal, tipo de mídia e tipo de local.

![](../../images/field-groups/channel-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `channel` | [Canal de experiência](../../data-types/experience-channel.md) | Um objeto que descreve devoluções de produtos, registro de garantia e carrinho de compras/processos de pedido. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
