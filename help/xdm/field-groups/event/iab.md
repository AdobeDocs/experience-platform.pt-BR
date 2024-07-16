---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;ExperienceEvent;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;iab;tcf;consentimento;
solution: Experience Platform
title: Grupo de campos de consentimento da TCF 2.0 do IAB para esquemas de evento
description: Saiba mais sobre o grupo de campos de esquema de consentimento da TCF 2.0 do IAB para a classe ExperienceEvent XDM.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL Grupo de campos Consentimento] do TCF do IAB 2.0 para esquemas de evento

>[!IMPORTANT]
>
>Este documento abrange o grupo de campos de esquema [!UICONTROL Consentimento] da TCF do IAB para a classe XDM ExperienceEvent. Este grupo de campos só deve ser usado se você pretende rastrear eventos de alteração de consentimento ao longo do tempo.
>
>Observe que os valores de consentimento registrados nos dados do evento não são honrados nos workflows de imposição automática. Para que a aplicação automática ocorra, os valores de consentimento devem ser assimilados na classe Perfil individual XDM e ativados para o Perfil do cliente em tempo real.
>
>Para o grupo de campos destinado à classe de Perfil Individual XDM, consulte o seguinte [documento](../profile/iab.md).

[!UICONTROL O Consentimento IAB TCF 2.0] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) usada para capturar cadeias de consentimento IAB de série com carimbo de data e hora, a fim de rastrear padrões de alteração de consentimento ao longo do tempo.

![](../../images/field-groups/iab-event.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `consentStrings` | Matriz de [Cadeias de Consentimento](../../data-types/consent-string.md) | Uma matriz de valores de sequência de consentimento associados ao evento. |

{style="table-layout:auto"}

Consulte o manual sobre o [Suporte ao IAB TCF 2.0 na Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações sobre o caso de uso deste grupo de campos. Para obter mais detalhes sobre o próprio grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
