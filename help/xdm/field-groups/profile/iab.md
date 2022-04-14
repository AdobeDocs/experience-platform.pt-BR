---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, design de esquema, grupo de campos, grupo de campos, iab, tcf, consentimento;
solution: Experience Platform
title: Grupo de campos de consentimento do IAB TCF 2.0 para esquemas de perfil
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Consent schema do IAB TCF 2.0 para a classe Perfil individual XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 046486d5e154b45fc2c2f5408eee235dddf46a4d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Consentimento do IAB TCF 2.0] grupo de campos para esquemas de perfil

>[!NOTE]
>
>Este documento aborda a [!UICONTROL Consentimento do IAB TCF 2.0] grupo de campos de esquema para a classe Perfil individual XDM. Para o grupo de campos destinado à classe XDM ExperienceEvent, consulte o seguinte [documento](../event/iab.md) em vez disso.

[!UICONTROL Consentimento do IAB TCF 2.0] é um grupo de campos de esquema padrão para a variável [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) usada para capturar sequências de consentimento IAB de séries com carimbo de data e hora, para rastrear padrões de alteração de consentimento ao longo do tempo.

![](../../images/field-groups/iab-profile.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `identityPrivacyInfo` | Mapa | Um objeto do tipo mapa que associa os valores de identidade individuais de um cliente a diferentes sequências de consentimento da TCF. Um exemplo da estrutura desse objeto é fornecido abaixo. |

{style=&quot;table-layout:auto&quot;}

O JSON a seguir demonstra a estrutura do `identityPrivacyInfo` mapa.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Como mostra o exemplo, cada chave de nível raiz de `xdm:identityPrivacyInfo` corresponde a um namespace de identidade reconhecido pelo Serviço de identidade. Por sua vez, cada propriedade de namespace deve ter pelo menos uma subpropriedade cuja chave corresponda ao valor de identidade correspondente do cliente para esse namespace. Neste exemplo, o cliente é identificado com uma ID de Experience Cloud (`ECID`) valor de `13782522493631189`.

>[!NOTE]
>
>Embora o exemplo acima use um único par de namespace/valor para representar a identidade do cliente, você pode adicionar chaves adicionais para outros namespaces, e cada namespace pode ter vários valores de identidade, cada um com seu próprio conjunto de preferências de consentimento TCF.

Para cada valor de identidade, uma `identityIABConsent` deve ser fornecida, que fornece o valor de consentimento TCF para a identidade. O valor dessa propriedade deve estar em conformidade com a variável [[!UICONTROL Sequência de consentimento] tipo de dados](../../data-types/consent-string.md).

Consulte o guia sobre [Suporte ao IAB TCF 2.0 na plataforma](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações sobre o caso de uso desse grupo de campos. Para obter mais detalhes sobre o próprio grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
