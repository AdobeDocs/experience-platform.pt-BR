---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;Design de esquema;grupo de campos;grupo de campos;iab;tcf;consentimento;
solution: Experience Platform
title: Grupo de campos de consentimento da TCF 2.0 do IAB para esquemas de perfil
description: Saiba mais sobre o grupo de campos de esquema de consentimento da TCF 2.0 do IAB para a classe Perfil individual XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!UICONTROL Grupo de campos Consentimento] do TCF do IAB 2.0 para esquemas de perfil

>[!NOTE]
>
>Este documento abrange o grupo de campos de esquema [!UICONTROL Consentimento] da TCF do IAB para a classe de Perfil Individual XDM. Para o grupo de campos destinado à classe XDM ExperienceEvent, consulte o seguinte [documento](../event/iab.md).

[!UICONTROL O Consentimento IAB TCF 2.0] é um grupo de campos de esquema padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) usada para capturar cadeias de consentimento IAB de série com carimbo de data e hora, a fim de rastrear padrões de alteração de consentimento ao longo do tempo.

![](../../images/field-groups/iab-profile.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `identityPrivacyInfo` | Mapa | Um objeto do tipo mapa que associa os valores de identidade individuais de um cliente a diferentes sequências de consentimento TCF. Um exemplo da estrutura desse objeto é fornecido abaixo. |

{style="table-layout:auto"}

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

Como mostra o exemplo, cada chave de nível raiz de `xdm:identityPrivacyInfo` corresponde a um namespace de identidade reconhecido pelo Serviço de Identidade. Por sua vez, cada propriedade de namespace deve ter pelo menos uma subpropriedade cuja chave corresponda ao valor de identidade correspondente do cliente para esse namespace. Neste exemplo, o cliente é identificado com um valor de ID de Experience Cloud (`ECID`) de `13782522493631189`.

>[!NOTE]
>
>Embora o exemplo acima use um único par de namespace/valor para representar a identidade do cliente, você pode adicionar outras chaves para outros namespaces, e cada namespace pode ter vários valores de identidade, cada um com seu próprio conjunto de preferências de consentimento de TCF.

Para cada valor de identidade, uma propriedade `identityIABConsent` deve ser fornecida, que fornece o valor de consentimento TCF para a identidade. O valor desta propriedade deve estar em conformidade com o tipo de dados [[!UICONTROL Cadeia de caracteres de consentimento]](../../data-types/consent-string.md).

Consulte o manual sobre o [Suporte ao IAB TCF 2.0 na Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter mais informações sobre o caso de uso deste grupo de campos. Para obter mais detalhes sobre o próprio grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
