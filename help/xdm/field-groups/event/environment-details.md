---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; Esquemas; Design de esquema; grupo de campos; grupo de campos; ambiente; detalhes de ambiente;
solution: Experience Platform
title: Grupo de campos do esquema Detalhes do ambiente
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Detalhes do ambiente ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos ] Detalhes do ambiente

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Os ] Detalhes do ambiente são um grupo de campo de esquema padrão para a classe  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) usada para capturar informações relacionadas a detalhes do ambiente relacionados a um Evento de experiência, como detalhes do dispositivo, informações do navegador, hora local e outras informações geográficas.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descreve uma instância identificada de dispositivo, aplicativo ou navegador de dispositivo que é rastreável entre sessões, normalmente por cookies. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descreve informações sobre o contexto de situação da observação do evento, detalhando especificamente informações transitórias, como a rede ou as versões de software. |
| `placeContext` | [Inserir contexto](../../data-types/place-context.md) | Descreve as circunstâncias transitórias relacionadas com a observação de eventos. Os exemplos incluem informações específicas da localidade, como tempo, hora local, tráfego, dia da semana, dia útil vs. feriado e horário de trabalho. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
