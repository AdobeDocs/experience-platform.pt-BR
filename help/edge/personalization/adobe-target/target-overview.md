---
title: 'Adobe Target e o Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK e uso do Adobe Target
description: Saiba como renderizar conteúdo personalizado com o SDK da Web Experience Platform usando o Adobe Target
seo-description: Saiba como renderizar conteúdo personalizado com o SDK da Web Experience Platform usando o Adobe Target
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: f2bd8b89207901e57272a4f56d7f561ac10eb60a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# [!DNL Target] Visão geral

A Adobe Experience Platform [!DNL Web SDK] pode fornecer e renderizar experiências personalizadas gerenciadas no Adobe Target para o canal da Web. Você pode usar um editor WYSIWYG, chamado [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou uma interface não visual, o Criador [de experiências baseado em](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)formulário, para criar, ativar e fornecer suas atividades e experiências de personalização.

## Ativação do Adobe Target

Para ativar [!DNL Target], é necessário fazer o seguinte:

1. Ative o público alvo na sua configuração [de](../../fundamentals/edge-configuration.md) borda com o código de cliente apropriado.
1. Adicione a `renderDecisions` opção aos seus eventos.

Em seguida, opcionalmente, você também pode:

* Adicione `decisionScopes` aos seus eventos para recuperar atividades específicas (úteis para atividades criadas com o compositor baseado em formulário).
* Adicione o snippet de [pré-ocultação](../manage-flicker.md) para ocultar apenas algumas partes da página.

## Uso do Adobe Target VEC

Para usar o VEC com uma implementação do SDK da Web de plataforma, é necessário instalar e ativar o [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension.

## Atividades VEC de renderização automática

O SDK da Web AEP tem o poder de renderizar automaticamente suas experiências definidas por meio do VEC da Adobe Target na Web para seus usuários. Para indicar ao AEP Web SDK para renderizar automaticamente atividades VEC, envie um evento com `renderDecisions = true`:

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

## Uso do Criador baseado em forma

O Criador de experiências baseado em forma é uma interface não visual útil para configurar Testes A/B, [!DNL Experience Targeting]Automated Personalization e Recommendations atividade com diferentes tipos de resposta, como JSON, HTML, Imagem etc. Dependendo do tipo de resposta ou da decisão retornada pela Adobe Target, sua lógica comercial central pode ser executada. Para recuperar decisões para suas atividades do Compositor baseado em forma, envie um evento com todos os &quot;escopos de decisão&quot; para os quais deseja recuperar uma decisão.

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

`decisionScopes` define seções, locais ou partes de suas páginas nas quais você gostaria de renderizar uma experiência personalizada. Eles `decisionScopes` são personalizáveis e definidos pelo usuário. Para [!DNL Target] os clientes atuais, `decisionScopes` também são conhecidos como &quot;mboxes&quot;. Na [!DNL Target] interface do usuário, `decisionScopes` apareça como &quot;locais&quot;.

## O `__view__` âmbito

O AEP [!DNL Web SDK] fornece uma funcionalidade na qual você pode recuperar ações VEC sem depender do AEP [!DNL Web SDK] para renderizar as ações do VEC para você. Envie um evento com `__view__` definição de `decisionScopes`.

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## Audiências no XDM

Ao definir Audiências para as atividades do Público alvo que serão entregues por meio do SDK da Web do AEP, o [XDM](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/home.html) deve ser definido e usado. Depois de definir schemas XDM, classes e combinações, você pode criar uma regra de audiência de Público alvo definida pelos dados XDM para definição de metas. No Público alvo, os dados XDM são exibidos no Construtor de Audiências como um parâmetro personalizado. O XDM é serializado usando a notação de pontos (por exemplo, `web.webPageDetails.name`).

Se você tiver atividades Públicos alvos com audiências predefinidas que usam parâmetros personalizados ou um perfil de usuário, lembre-se de que elas não serão entregues corretamente pelo SDK da Web AEP. Em vez de usar parâmetros personalizados ou o perfil do usuário, você deve usar o XDM. Entretanto, há campos de direcionamento de audiência prontos para uso compatíveis com o SDK da Web do AEP que não exigem o XDM. Estes são os campos disponíveis na interface do Público alvo que não exigem o XDM:

* Biblioteca do Target
* Geografia  
* Rede
* Operating System
* Páginas do site
* Browser
* Fontes de Tráfego
* Intervalo de tempo

## Terminologia

__Decisões:__ Em [!DNL Target], elas estão correlacionadas à experiência selecionada de uma Atividade.

__Schema:__ O schema de uma decisão é o tipo de oferta em [!DNL Target].

__Âmbito:__ O âmbito da decisão. Em [!DNL Target]casa, aqui está a mBox. A mBox global é o `__view__` escopo.

__XDM:__ O XDM é serializado em notação de pontos e colocado em [!DNL Target] parâmetros mBox.
