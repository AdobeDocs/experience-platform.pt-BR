---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; Esquemas; Design de esquema; grupo de campos; grupo de campos; iab; tcf; consentimento;
solution: Experience Platform
title: Grupo de campos de consentimento do IAB TCF 2.0 para esquemas de evento
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Consent schema do IAB TCF 2.0 para a classe XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 046486d5e154b45fc2c2f5408eee235dddf46a4d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# [!UICONTROL Consentimento do IAB TCF 2.0] grupo de campos para esquemas de evento

>[!IMPORTANT]
>
>Este documento aborda a [!UICONTROL Consentimento do IAB TCF 2.0] grupo de campos de esquema para a classe XDM ExperienceEvent. Esse grupo de campos só deve ser usado se você pretende rastrear eventos de alteração de consentimento ao longo do tempo.
>
>Observe que os valores de consentimento registrados nos dados do evento não são honrados nos workflows de imposição automática. Para que a imposição automática ocorra, os valores de consentimento devem ser assimilados na classe Perfil individual XDM e ativados para o Perfil do cliente em tempo real.
>
>Para o grupo de campos destinado à classe de Perfil individual XDM, consulte o seguinte [documento](../profile/iab.md) em vez disso.

[!UICONTROL Consentimento do IAB TCF 2.0] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usada para capturar sequências de consentimento IAB de séries com carimbo de data e hora, para rastrear padrões de alteração de consentimento ao longo do tempo.

![](../../images/field-groups/iab-event.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `consentStrings` | Matriz de [Cadeias de consentimento](../../data-types/consent-string.md) | Uma matriz de valores da cadeia de consentimento associados ao evento. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre [Suporte ao IAB TCF 2.0 na plataforma](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações sobre o caso de uso desse grupo de campos. Para obter mais detalhes sobre o próprio grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
