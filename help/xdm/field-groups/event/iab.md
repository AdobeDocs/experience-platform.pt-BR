---
keywords: Experience Platform; home; tópicos populares; esquema; Esquema; XDM; ExperienceEvent; campos; esquemas; Esquemas; Design de esquema; grupo de campos; grupo de campos; iab; tcf; consentimento;
solution: Experience Platform
title: Grupo de campos do esquema de consentimento do IAB TCF 2.0
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Consent schema do IAB TCF 2.0 para a classe XDM ExperienceEvent.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# [!UICONTROL Grupo de campos ] Consentschema TCF 2.0 do IAB

>[!IMPORTANT]
>
>Este documento aborda o grupo de campos [!UICONTROL Consentimento IAB TCF 2.0] para a classe XDM ExperienceEvent. Esse grupo de campos só deve ser usado se você pretende rastrear eventos de alteração de consentimento ao longo do tempo.
>
>Observe que os valores de consentimento registrados nos dados do evento não são honrados nos workflows de imposição automática. Para que a imposição automática ocorra, os valores de consentimento devem ser assimilados na classe Perfil individual XDM e ativados para o Perfil do cliente em tempo real.
>
>Para o grupo de campos destinado à classe de Perfil individual XDM, consulte o seguinte [document](../profile/iab.md).

[!UICONTROL TCF do IAB 2.0 ] Consiste em um grupo de campo de esquema padrão para as classes  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) usadas para capturar sequências com carimbo de data e hora de consentimento do IAB, para rastrear padrões de alteração de consentimento ao longo do tempo.

![](../../images/field-groups/iab-event.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `consentStrings` | Matriz de [Cadeias de consentimento](../../data-types/consent-string.md) | Uma matriz de valores da cadeia de consentimento associados ao evento. |

{style=&quot;table-layout:auto&quot;}

Consulte o guia sobre o suporte ao [IAB TCF 2.0 no Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações sobre o caso de uso desse grupo de campos. Para obter mais detalhes sobre o próprio grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
