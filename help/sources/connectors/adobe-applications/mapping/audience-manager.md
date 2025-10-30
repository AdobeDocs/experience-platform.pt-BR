---
keywords: Experience Platform;página inicial;tópicos populares;mapeamento do Audience Manager;mapeamento do audience manager
solution: Experience Platform
title: Mapeamento de campos para o Adobe Audience Manager Source Connector
description: Saiba como mapear dados do Adobe Audience Manager (dados em tempo real, integrados e de perfil) para campos correspondentes do Experience Data Model (XDM) do conector de origem do Audience Manager.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Mapeamentos de campo do Audience Manager

As tabelas abaixo contêm os mapeamentos entre os campos nos dados do Adobe Audience Manager (dados em tempo real, integrados e de perfil) e seus campos XDM correspondentes.

Consulte o [dicionário de campo XDM](../../../../xdm/schema/field-dictionary.md) para obter mais informações sobre cada campo XDM.

## Dados em tempo real

Tipo: dados em tempo real

| Campo de dados em tempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Somente para namespaces presentes em endUserIds e somente o primeiro valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Somente para namespaces presentes em endUserIds e somente o primeiro valor.* |
| `trait[]` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → tipo</li><li>fabricante → fabricante</li><li>marketingName → modelo</li><li>modelNumber → modelo</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → cidade</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nome do sistema operacional </li><li>d_os_version → os_version</li></ul> |

{style="table-layout:auto"}

## Dados do perfil

Tipo: Perfil XDM

| Campo de perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style="table-layout:auto"}
