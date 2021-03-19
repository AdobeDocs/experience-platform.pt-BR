---
title: Uso do Adobe Target com o SDK da Web da plataforma
description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform usando o Adobe Target
keywords: target; adobe target; activity.id; experience.id; renderDecisões; decisionScopes; pré-ocultar trecho; vec; Experience Composer baseado em formulário; xdm; públicos-alvo; decisões; escopo; esquema;
translation-type: tm+mt
source-git-commit: 98db5b92ea0f51c8641651eb14e3fe6cecf7027c
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---


# Uso do Adobe Target com o SDK da Web da plataforma

O Adobe Experience Platform [!DNL Web SDK] pode entregar e renderizar experiências personalizadas gerenciadas no Adobe Target para o canal da Web. Você pode usar um editor WYSIWYG, chamado [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou uma interface não visual, o [Experience Composer baseado em formulário](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), para criar, ativar e entregar suas atividades e experiências de personalização.

Os seguintes recursos foram testados e atualmente são compatíveis com o Target:

* Testes A/B
* Relatórios de impressão e conversão do A4T
* Personalização automatizada
* Direcionamento de experiência
* Testes multivariados
* Relatórios de conversão e impressão do Target nativo
* Suporte ao VEC

## Ativação do Adobe Target

Para ativar [!DNL Target], faça o seguinte:

1. Ative o destino na sua [configuração de borda](../../fundamentals/edge-configuration.md) com o código de cliente apropriado.
1. Adicione a opção `renderDecisions` aos eventos.

Em seguida, opcionalmente, também é possível adicionar as seguintes opções:

* `decisionScopes`: Recupere atividades específicas (úteis para atividades criadas com o compositor baseado em formulário) adicionando essa opção aos eventos.
* [Pré-ocultar trecho](../manage-flicker.md): Ocultar apenas determinadas partes da página.

## Uso do VEC do Adobe Target

Para usar o VEC com uma implementação do SDK da Web da plataforma, instale e ative a [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou a [Extensão de ajuda do Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC.

## Atividades do VEC de renderização automática

O SDK da Web da Adobe Experience Platform tem o poder de renderizar automaticamente suas experiências definidas por meio do VEC da Adobe Target na Web para seus usuários. Para indicar ao Adobe Experience Platform Web SDK para renderizar automaticamente atividades do VEC, envie um evento com `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## Uso do Compositor baseado em formulário

O Experience Composer baseado em formulário é uma interface não visual útil para configurar os Testes A/B, [!DNL Experience Targeting], Automated Personalization e Recommendations com tipos de resposta diferentes, como JSON, HTML, Imagem etc. Dependendo do tipo de resposta ou da decisão retornada pela Adobe Target, a lógica de negócios principal pode ser executada. Para recuperar as decisões das atividades do Composer baseado em formulário, envie um evento com todos os &quot;Deciscopes&quot; para os quais deseja recuperar uma decisão.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Escopos de decisão

`decisionScopes` define seções, locais ou partes de suas páginas em que você deseja renderizar uma experiência personalizada. Esses `decisionScopes` são personalizáveis e definidos pelo usuário. Para clientes atuais [!DNL Target], `decisionScopes` também são conhecidas como &quot;mboxes&quot;. Na interface [!DNL Target], `decisionScopes` aparece como &quot;locais&quot;.

## O `__view__` Escopo

O Adobe Experience Platform Web SDK fornece funcionalidades onde você pode recuperar ações do VEC sem depender do SDK para renderizar as ações do VEC para você. Envie um evento com `__view__` definido como um `decisionScopes`.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Públicos-alvo no XDM

Ao definir públicos para suas atividades do Target que são entregues por meio do SDK da Web da Adobe Experience Platform, [XDM](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/home.html) deve ser definido e usado. Depois de definir esquemas, classes e combinações do XDM, você pode criar uma regra de público-alvo do Target definida pelos dados do XDM para o direcionamento. No Target, os dados do XDM são exibidos no Audience Builder como um parâmetro personalizado. O XDM é serializado usando notação de pontos (por exemplo, `web.webPageDetails.name`).

Se você tiver atividades do Target com públicos-alvo predefinidos que usam parâmetros personalizados ou um perfil de usuário, elas não serão entregues corretamente por meio do SDK. Em vez de usar parâmetros personalizados ou o perfil do usuário, você deve usar o XDM. No entanto, há campos de direcionamento de público-alvo prontos para uso compatíveis com o SDK da Web da Adobe Experience Platform que não exigem XDM. Esses campos estão disponíveis na interface do usuário do Target que não requer XDM:

* Biblioteca do Target
* Geografia  
* Rede
* Operating System
* Páginas do site
* Browser
* Fontes de Tráfego
* Intervalo de tempo

## Terminologia

__Decisões:__ No  [!DNL Target], as decisões estão relacionadas à experiência selecionada em uma Atividade.

__Esquema:__ O schema de uma decisão é o tipo de oferta no  [!DNL Target].

__Âmbito de aplicação:__ âmbito de aplicação da decisão. Em [!DNL Target], o escopo é a mBox. A mBox global é o escopo `__view__`.

__XDM:__ o XDM é serializado na notação de pontos e, em seguida, colocado  [!DNL Target] como parâmetros mBox.
