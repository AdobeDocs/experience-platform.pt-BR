---
title: edgeBasePath
description: O caminho base do endpoint usado para interagir com os serviços da Adobe.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

A propriedade `edgeBasePath` altera o caminho de destino quando você interage com os serviços da Adobe. A Adobe pode solicitar que você altere essa variável se participar de programas alfa ou beta para coleta de dados. A maioria das organizações não precisa definir ou alterar essa propriedade.

Definir o campo de texto `edgeBasePath` ao executar o comando `configure`. Se você omitir essa propriedade, o padrão será o valor de `ee`. A Adobe recomenda omitir essa propriedade na maioria das configurações.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Caminho básico do Edge usando a extensão de tag da Web SDK

O equivalente da extensão de tag do Web SDK deste campo está em [Configurações avançadas](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md) ao configurar a extensão de tag.
