---
title: Interação com a Adobe Experience Platform
description: Saiba como usar a API do Edge Network Server para interagir com o Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: recolha de dados; Saída; análises; api Adobe Experience Platform Edge Network; aep
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---


# Interação com a Adobe Experience Platform

## Visão geral {#overview}

Para habilitar a coleta de dados do Experience Platform, é necessário primeiro [configurar seu conjunto de dados](../edge/fundamentals/datastreams.md) para encaminhar eventos para conjuntos de dados do Experience Platform.

Depois de configurada, a configuração do armazenamento de dados deve incluir configurações para `com_adobe_experience_platform`, conforme mostrado no exemplo abaixo:


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
