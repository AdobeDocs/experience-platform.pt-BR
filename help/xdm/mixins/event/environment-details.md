---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; esquemas; design de esquema; mixin; mixin; ambiente; detalhes do ambiente;
solution: Experience Platform
title: Mistura de detalhes do ambiente
topic-legacy: overview
description: Este documento fornece uma visão geral do mixin Detalhes do ambiente ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---

# [!UICONTROL Environment Details] mistura

>[!NOTE]
>
>Os nomes de várias mixins mudaram. Consulte o documento em [mixin name updates](../name-updates.md) para obter mais informações.

[!UICONTROL Environment Details] é um mixin padrão para a classe  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) usada para capturar informações sobre detalhes do ambiente relacionados a um evento de experiência, como detalhes do dispositivo, informações do navegador, hora local e outras informações geográficas.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descreve uma instância identificada de dispositivo, aplicativo ou navegador de dispositivo que é rastreável entre sessões, normalmente por cookies. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descreve informações sobre o contexto de situação da observação do evento, detalhando especificamente informações transitórias, como a rede ou as versões de software. |
| `placeContext` | [Inserir contexto](../../data-types/place-context.md) | Descreve as circunstâncias transitórias relacionadas com a observação de eventos. Os exemplos incluem informações específicas da localidade, como tempo, hora local, tráfego, dia da semana, dia útil vs. feriado e horário de trabalho. |

Para obter mais detalhes sobre o mixin, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
