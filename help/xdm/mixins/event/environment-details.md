---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: Mistura de detalhes do ambiente ExperienceEvent
topic: overview
description: Este documento fornece uma visão geral da combinação Detalhes do Ambiente ExperienceEvent.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# [!UICONTROL Mistura de detalhes] do ambiente ExperienceEvent

[!UICONTROL Detalhes] do ambiente ExperienceEvent é uma combinação padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md) usada para capturar informações relacionadas aos detalhes do ambiente relacionados a um Evento Experience, como detalhes do dispositivo, informações do navegador, hora local e outras informações geográficas.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descreve uma instância de dispositivo, aplicativo ou navegador de dispositivo identificada que pode ser rastreada em sessões, normalmente por cookies. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descreve informações sobre o contexto de situação da observação do evento, detalhando especificamente informações transitórias, como a rede ou as versões de software. |
| `placeContext` | [Inserir contexto](../../data-types/place-context.md) | Descreve as circunstâncias transitórias relacionadas com a observação do evento. Os exemplos incluem informações específicas da localidade, como tempo, hora local, tráfego, dia da semana, dia útil vs. feriado e horário de trabalho. |

Para obter mais detalhes sobre a mistura, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
