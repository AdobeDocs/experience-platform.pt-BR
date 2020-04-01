---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: campo de mapeamento do Gerenciador de Audiências
topic: overview
translation-type: tm+mt
source-git-commit: 985c450a174712fa4b4185d5a6527962e697b5ba

---


# campo de mapeamento do Gerenciador de Audiências

As tabelas abaixo contêm os mapeamentos entre os campos nos dados do Adobe Audiência Manager (dados em tempo real, onboard e Perfil) e seus campos XDM correspondentes.

Consulte o dicionário [de campos](../../../xdm/schema/field-dictionary.md) XDM para obter mais informações sobre cada campo XDM.

## Dados em tempo real

Tipo: Dados em tempo real

| Campo de dados em tempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Somente para namespaces presentes em endUserIds e somente para o primeiro valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Somente para namespaces presentes em endUserIds e somente para o primeiro valor.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>PrimaryHardwareType → type</li><li>fabricante → fabricante</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → cidade</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nome dos </li><li>d_os_version → os_version</li></ul> |
| `Signals` | ExperienceEvent.signal |

## Dados de entrada **(obsoleto)**

Tipo: ExperienceEvent

| Campo de entrada | Campo XDM |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] Os campos de entrada estão programados para serem descontinuados em uma versão futura.

## dados do Perfil

Tipo: Perfil XDM

| Campo Perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
