---
keywords: Experience Platform, home, tópicos populares, esquema, esquema, XDM, perfil individual, campos, esquemas, esquemas, design de esquema, grupo de campos, grupo de campos, iab, tcf, consentimento;
solution: Experience Platform
title: Grupo de campos do esquema de consentimento do IAB TCF 2.0
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Consent schema do IAB TCF 2.0 para a classe Perfil individual XDM.
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---


# [!UICONTROL Grupo de campos ] Consentschema TCF 2.0 do IAB

>[!NOTE]
>
>Este documento aborda o grupo de campos [!UICONTROL Consentimento IAB TCF 2.0] para a classe Perfil individual XDM. Para o grupo de campos destinado à classe XDM ExperienceEvent, consulte o seguinte [document](../event/iab.md).

[!UICONTROL TCF do IAB 2.0 ] Consiste em um grupo de campo de esquema padrão para as classes  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) usadas para capturar sequências com carimbo de data e hora de consentimento do IAB, para rastrear padrões de alteração de consentimento ao longo do tempo.

![](../../images/field-groups/iab-profile.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `identityPrivacyInfo` | Mapa | Um objeto do tipo mapa que associa os valores de identidade individuais de um cliente a diferentes sequências de consentimento da TCF. Um exemplo da estrutura desse objeto é fornecido abaixo. |

{style=&quot;table-layout:auto&quot;}

O JSON a seguir demonstra a estrutura do mapa `identityPrivacyInfo`.

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

Como mostra o exemplo, cada chave de nível raiz de `xdm:identityPrivacyInfo` corresponde a um namespace de identidade reconhecido pelo Serviço de identidade. Por sua vez, cada propriedade de namespace deve ter pelo menos uma subpropriedade cuja chave corresponda ao valor de identidade correspondente do cliente para esse namespace. Neste exemplo, o cliente é identificado com um valor de Experience Cloud (`ECID`) de `13782522493631189`.

>[!NOTE]
>
>Embora o exemplo acima use um único par de namespace/valor para representar a identidade do cliente, você pode adicionar chaves adicionais para outros namespaces, e cada namespace pode ter vários valores de identidade, cada um com seu próprio conjunto de preferências de consentimento TCF.

Para cada valor de identidade, uma propriedade `identityIABConsent` deve ser fornecida, que fornece o valor de consentimento TCF para a identidade. O valor dessa propriedade deve estar em conformidade com o tipo de dados [[!UICONTROL Consent String]](../../data-types/consent-string.md).

Consulte o guia sobre o suporte ao [IAB TCF 2.0 no Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações sobre o caso de uso desse grupo de campos. Para obter mais detalhes sobre o próprio grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
