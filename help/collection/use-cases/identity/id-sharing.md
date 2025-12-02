---
title: Compartilhamento de ID de dispositivo móvel para Web e entre domínios
description: Saiba como manter IDs de visitante móveis em propriedades da Web e entre domínios
keywords: Identidade;móvel;id;compartilhamento;domínio;domínio cruzado;sdk;plataforma;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Compartilhamento de ID de dispositivo móvel para Web e entre domínios

## Visão geral

O Adobe Experience Platform Web SDK oferece suporte a recursos de compartilhamento de ID de visitante que permitem aos clientes fornecer experiências personalizadas com mais precisão, entre aplicativos móveis e conteúdo da Web móvel, e entre domínios.

## Casos de uso {#use-cases}

### Forneça personalização consistente entre aplicativos para dispositivos móveis e sites para dispositivos móveis

Uma empresa de roupas quer personalizar a experiência de seus clientes com base em seus interesses e manter a personalização precisa em um aplicativo móvel que também carrega WebViews. Com o recurso de compartilhamento de ID de dispositivo móvel para Web, eles podem garantir que as ofertas mais precisas sejam apresentadas aos clientes, usando o mesmo identificador de visitante no aplicativo e o conteúdo da Web móvel ao passar o [!DNL ECID] para a URL da Web móvel.

### Oferecer personalização consistente entre domínios

Uma retailer com várias lojas online deseja personalizar a experiência do comprador em seus domínios, com base nos interesses do cliente. Usando o recurso de compartilhamento de ID entre domínios do Web SDK, a retailer pode fornecer ofertas precisas com base nos interesses do cliente, em todos os domínios.

### Melhorar os relatórios de atividade do visitante

Uma tecnologia que a retailer deseja melhorar os relatórios de atividades do visitante com informações sobre quando seus visitantes se movem do aplicativo móvel para o site móvel ou para outros domínios. Usando o recurso de compartilhamento de ID entre domínios do Web SDK, a equipe de marketing pode rastrear com precisão os visitantes em suas propriedades da Web e gerar relatórios de atividade.

## Pré-requisitos {#prerequisites}

Para usar o compartilhamento de ID móvel para Web e entre domínios, você deve usar o [!DNL Web SDK] versão 2.11.0 ou posterior.

Para implementações do Edge Network Mobile, esse recurso é compatível com a extensão [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) a partir da versão 1.1.0 (iOS e Android).

Este recurso também é compatível com o [!DNL VisitorAPI.js] versão 1.7.0 ou posterior.

## Compartilhamento de ID de dispositivo móvel para Web {#mobile-to-web}

Use a API `getUrlVariables` da extensão [Identidade para Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) para recuperar os identificadores como parâmetros de consulta e anexá-los à sua URL ao abrir [!DNL webViews].

Nenhuma configuração adicional é necessária para que o Web SDK aceite valores `ECID` na cadeia de caracteres de consulta.

O parâmetro da cadeia de caracteres de consulta inclui:

* `MCID`: A Experience Cloud ID (`ECID`)
* `MCORGID`: O Experience Cloud `orgID` que deve corresponder ao `orgID` configurado no [!DNL Web SDK].
* `TS`: Um parâmetro de carimbo de data/hora que não pode ter mais de cinco minutos.


O compartilhamento da ID móvel para Web usa o parâmetro `adobe_mc`. Quando o parâmetro `adobe_mc` está presente e é válido, o `ECID` da cadeia de caracteres de consulta é automaticamente adicionado ao mapa de identidade na primeira solicitação feita à Edge Network. Todas as interações subsequentes do Edge Network usarão esse `ECID`.

Para obter mais informações sobre como transmitir IDs de visitante de um aplicativo móvel para um WebView, consulte a documentação sobre [manipulação de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Implementar compartilhamento de ID entre domínios {#cross-domain-sharing}

Consulte os links a seguir, dependendo de como você configurou o Web SDK:

* **biblioteca JavaScript**: comando [`appendIdentityToUrl`](../../js/commands/appendidentitytourl.md)
* **Extensão da marca**: [Redirecionar com ação de identidade](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)
