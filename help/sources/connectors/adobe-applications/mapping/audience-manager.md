---
keywords: 'Experience Platform;home;popular topics;mapeamento de Audience Manager;mapeamento do gerenciador de audiências;home;popular topics;mapeamento;mapeamento do gerenciador de '
solution: Experience Platform
title: Mapeamento de campos para o Adobe Audience Manager Source Connector
topic: overview
description: Saiba como mapear dados da Adobe Audience Manager (dados em tempo real, onboard e Perfil) para os campos correspondentes do Modelo de dados da experiência (XDM) para o conector de fonte de Audience Manager.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Mapeamentos de campos Audience Manager

As tabelas abaixo contêm os mapeamentos entre os campos nos dados do Adobe Audience Manager (Dados em tempo real, Onboard e Perfil) e seus campos XDM correspondentes.

Consulte o [dicionário de campos XDM](../../../../xdm/schema/field-dictionary.md) para obter mais informações sobre cada campo XDM.

## Dados em tempo real

Tipo: Dados em tempo real

| Campo de dados em tempo real | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -  *Somente para namespaces presentes em endUserIds e somente para o primeiro valor.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Somente para namespaces presentes em endUserIds e somente o primeiro valor.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>PrimaryHardwareType → type</li><li>fabricante → fabricante</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → cidade</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nome dos </li><li>d_os_version → os_version</li></ul> |

## dados do perfil

Tipo: Perfil XDM

| Campo perfil | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
