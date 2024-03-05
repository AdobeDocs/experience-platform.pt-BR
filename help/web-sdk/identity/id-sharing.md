---
title: Compartilhamento de ID de dispositivo móvel para Web e entre domínios
description: Saiba como manter IDs de visitante móveis em propriedades da Web e entre domínios
keywords: Identidade;móvel;id;compartilhamento;domínio;domínio cruzado;sdk;plataforma;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Compartilhamento de ID de dispositivo móvel para Web e entre domínios

## Visão geral

O SDK da Web da Adobe Experience Platform oferece suporte a recursos de compartilhamento de ID de visitante que permitem aos clientes fornecer experiências personalizadas com mais precisão, entre aplicativos móveis e conteúdo da Web móvel, e entre domínios.

## Casos de uso {#use-cases}

### Forneça personalização consistente entre aplicativos para dispositivos móveis e sites para dispositivos móveis

Uma empresa de roupas quer personalizar a experiência de seus clientes com base em seus interesses e manter a personalização precisa em um aplicativo móvel que também carrega WebViews. Ao usar o recurso de compartilhamento de ID de dispositivo móvel para Web, eles podem garantir que as ofertas mais precisas sejam apresentadas aos clientes, usando o mesmo identificador de visitante no aplicativo e o conteúdo da Web móvel ao passar o [!DNL ECID] ao URL da internet móvel.

### Oferecer personalização consistente entre domínios

Um varejista com várias lojas online deseja personalizar a experiência do comprador em seus domínios, com base nos interesses do cliente. Usando o recurso de compartilhamento de ID entre domínios do SDK da Web, o varejista pode fornecer ofertas precisas com base nos interesses do cliente em todos os domínios.

### Melhorar os relatórios de atividade do visitante

Um varejista de tecnologia deseja melhorar o relatório de atividades do visitante com informações sobre quando seus visitantes mudam do aplicativo móvel para o site móvel ou para outros domínios. Usando o recurso de compartilhamento de ID entre domínios do SDK da Web, a equipe de marketing pode rastrear com precisão os visitantes em suas propriedades da Web e gerar relatórios de atividades.

## Pré-requisitos {#prerequisites}

Para usar o compartilhamento de ID móvel para Web e entre domínios, você deve usar [!DNL Web SDK] versão 2.11.0 ou posterior.

Para implementações móveis da Rede de borda, esse recurso é compatível com o [Identidade da rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) extensão a partir da versão 1.1.0 (iOS e Android).

Esse recurso também é compatível com o [!DNL VisitorAPI.js] versão 1.7.0 ou posterior.

## Compartilhamento de ID de dispositivo móvel para Web {#mobile-to-web}

Use o `getUrlVariables` API do [Identidade da rede de borda](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) extensão para recuperar os identificadores como parâmetros de consulta e anexá-los ao seu URL ao abrir [!DNL webViews].

Nenhuma configuração adicional é necessária para que o SDK da Web aceite `ECID` valores na sequência de consulta.

O parâmetro da cadeia de caracteres de consulta inclui:

* `MCID`: A ID do Experience Cloud (`ECID`)
* `MCORGID`: O EXPERIENCE CLOUD `orgID` que deve corresponder ao `orgID` configurado no [!DNL Web SDK].
* `TS`: um parâmetro de carimbo de data e hora que não pode ter mais de cinco minutos.


O compartilhamento do Mobile para a Web ID usa o `adobe_mc` parâmetro. Quando a variável `adobe_mc` estiver presente e for válido, a variável `ECID` da sequência de consulta é automaticamente adicionado ao mapa de identidade na primeira solicitação feita à Rede de borda. Todas as interações subsequentes da Rede de borda usarão essa `ECID`.

Para obter mais informações sobre como transmitir IDs de visitante de um aplicativo móvel para um WebView, consulte a documentação em [manipulação de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Implementar compartilhamento de ID entre domínios {#cross-domain-sharing}

Consulte a [`appendIdentityToUrl`](../commands/appendidentitytourl.md) para obter instruções de implementação usando a extensão de tag do SDK da Web e a biblioteca JavaScript do SDK da Web.
