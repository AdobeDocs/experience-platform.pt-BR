---
keywords: Experience Platform;início;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;ambiente;detalhes do ambiente;
solution: Experience Platform
title: Grupo de campos de esquema de detalhes do ambiente
description: Este documento fornece uma visão geral do grupo de campos do esquema Detalhes do ambiente ExperienceEvent.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%

---


# [!UICONTROL Detalhes do ambiente] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes do ambiente] é um grupo de campos de esquema padrão para o [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para registrar informações sobre detalhes do ambiente relacionados a um Evento de experiência, como detalhes do dispositivo, informações do navegador, hora local e outras informações geográficas.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descreve um dispositivo, aplicativo ou instância de navegador de dispositivo identificado que pode ser rastreado entre as sessões, normalmente por cookies. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descreve informações sobre o contexto situacional da observação do evento, detalhando especificamente informações transitórias, como a rede ou versões de software. |
| `placeContext` | [Contexto do local](../../data-types/place-context.md) | Descreve as circunstâncias transitórias relacionadas à observação do evento. Os exemplos incluem informações específicas do local, como clima, hora local, trânsito, dia da semana, dia útil vs. feriado e horário de trabalho. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
