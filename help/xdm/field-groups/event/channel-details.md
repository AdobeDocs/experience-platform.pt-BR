---
keywords: Experience Platform, home, tópicos populares, esquema, Esquema, XDM, ExperienceEvent, campos, esquemas, Esquemas, Design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de Campos do Esquema de Detalhes do Canal
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes do canal .
source-git-commit: b9168052174c250810e59e403cb77419d510df3b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] Detalhes do canal

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes do canal ] é um grupo de campo de esquema padrão para a  [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md), usado para descrever informações do canal, como ID, tipo de canal, tipo de mídia e tipo de local.

![](../../images/field-groups/channel-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `channel` | [Canal de experiência](../../data-types/experience-channel.md) | Um objeto que descreve retornos de produtos, registro em garantia e processos de carrinho/pedido de compras. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.schema.json)
