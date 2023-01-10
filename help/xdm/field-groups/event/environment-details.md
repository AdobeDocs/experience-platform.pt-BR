---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; Esquemas; Design de esquema; grupo de campos; grupo de campos; ambiente; detalhes de ambiente;
solution: Experience Platform
title: Grupo de campos do esquema Detalhes do ambiente
description: Este documento fornece uma visão geral do grupo de campos Detalhes do ambiente ExperienceEvent .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL Detalhes do ambiente] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações de nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Detalhes do ambiente] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usado para capturar informações relacionadas a detalhes do ambiente relacionados a um evento de experiência, como detalhes do dispositivo, informações do navegador, hora local e outras informações geográficas.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `device` | [Dispositivo](../../data-types/device.md) | Descreve uma instância identificada de dispositivo, aplicativo ou navegador de dispositivo que é rastreável entre sessões, normalmente por cookies. |
| `environment` | [Ambiente](../../data-types/environment.md) | Descreve informações sobre o contexto de situação da observação do evento, detalhando especificamente informações transitórias, como a rede ou as versões de software. |
| `placeContext` | [Inserir contexto](../../data-types/place-context.md) | Descreve as circunstâncias transitórias relacionadas com a observação de eventos. Os exemplos incluem informações específicas da localidade, como tempo, hora local, tráfego, dia da semana, dia útil vs. feriado e horário de trabalho. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
