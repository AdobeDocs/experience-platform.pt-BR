---
title: edgeDomain
description: Determine o domínio para o qual deseja enviar dados.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 3%

---

# `edgeDomain`

A propriedade `edgeDomain` permite alterar o domínio para o qual o Web SDK envia dados. O uso de um domínio personalizado pode ajudar a reduzir o impacto dos bloqueadores de anúncios.

>[!NOTE]
>
>Essa propriedade não é alterada no local em que os cookies são definidos. O Web SDK sempre define [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR), independentemente de onde ele envia dados.

O valor usado para `edgeDomain` depende da sua participação no [programa de certificados gerenciados pela Adobe](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/adobe-managed-cert):

**Se sua organização participar do programa de certificados gerenciados pela Adobe**, defina o valor para o domínio próprio que foi selecionado ao configurar o certificado. Normalmente, esse valor é um subdomínio de propriedade de sua organização. Por exemplo, `data.example.com`. Os registros CNAME na organização encaminham esses dados para a Adobe.

**Se sua organização não participar do programa de certificados**, defina o valor como um subdomínio de `data.adobedc.net`. A Adobe recomenda usar a ID de empresa IMS atribuída pela Adobe de sua organização para fins de consistência. Por exemplo, `example.data.adobedc.net`. Use as seguintes etapas para determinar a ID da empresa de IMS:

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Em qualquer lugar na interface do Experience Cloud, pressione `[Cmd]` + `[I]` (macOS) ou `[Ctrl]` + `[I]` (Windows).
1. Um **[!UICONTROL User data debugger]** é exibido. Selecione a guia **[!UICONTROL Assigned orgs]**.
1. Expanda a organização IMS desejada.
1. Localize o campo **[!UICONTROL Tenant]**. Este valor é o subdomínio recomendado de `data.adobedc.net` para ser usado.

Defina a cadeia de caracteres `edgeDomain` ao executar o comando `configure`. Se você omitir essa propriedade ao configurar o SDK, o padrão será `edge.adobedc.net`. Embora o valor padrão seja aceitável, a Adobe considera uma prática recomendada definir um valor específico da organização.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Domínio do Edge usando a extensão de tag da Web SDK

A extensão de tag equivalente a esta propriedade é o campo **[!UICONTROL Edge domain]** em [configurações da instância do SDK](/help/tags/extensions/client/web-sdk/configure/general.md) ao configurar a extensão.
