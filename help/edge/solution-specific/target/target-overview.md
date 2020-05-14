---
title: 'O SDK da Web do Público alvo Adobe e da plataforma Adobe Experience. '
seo-title: Adobe Experience Platform Web SDK e uso do Público alvo da Adobe
description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Público alvo Adobe
seo-description: Saiba como renderizar conteúdo personalizado com o Experience Platform Web SDK usando o Público alvo Adobe
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---


# Visão geral do Público alvo

O SDK da Web da plataforma Adobe Experience pode fornecer e renderizar experiências personalizadas gerenciadas no Público alvo da Adobe para o canal da Web. Você pode usar um editor WYSIWYG, chamado [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), ou uma interface não visual, o Criador [de experiências baseado em](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)formulário, para criar, ativar e fornecer suas atividades e experiências de personalização.

## Ativação do Adobe Público alvo

Para ativar o Público alvo, é necessário fazer o seguinte:

1. Ative os tokens de resposta do atividade.id e do experience.id na interface do usuário do Público alvo.

![público alvo_reponse_token](../../solution-specific/target/assets/target_response_token.png)

1. Ative o público alvo na sua configuração [de](../../fundamentals/edge-configuration.md) borda com o código de cliente apropriado.
1. Adicione a `renderDecisions` opção aos seus eventos.

Em seguida, opcionalmente, você também pode:

* Adicione `decisionScopes` aos seus eventos para recuperar atividades específicas (úteis para atividades criadas com o compositor baseado em formulário).
* Adicione o snippet de [pré-ocultação](../../solution-specific/target/flicker-management.md) para ocultar apenas algumas partes da página.

## Uso do Público alvo Adobe VEC

Com o SDK, você pode usar o VEC normalmente com uma exceção: você precisa da extensão [auxiliar VEC do](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) público alvo instalada e ativa.

## Atividades VEC de renderização automática

O SDK da Web AEP tem o poder de renderizar automaticamente suas experiências definidas por meio do VEC do Público alvo da Adobe na Web para seus usuários. Para indicar ao AEP Web SDK para renderizar automaticamente atividades VEC, envie um evento com `renderDecisions = true`:

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

O Criador de experiências baseado em forma é uma interface não visual útil para configurar testes A/B, direcionamento de experiência, personalização automatizada e atividades do Recommendations com diferentes tipos de resposta, como JSON, HTML, Imagem etc. Dependendo do tipo de resposta ou da decisão retornada pelo Público alvo da Adobe, sua lógica comercial principal pode ser executada. Para recuperar decisões para suas atividades do Compositor baseado em forma, envie um evento com todos os &quot;escopos de decisão&quot; para os quais deseja recuperar uma decisão.

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

`decisionScopes` define seções, locais ou partes de suas páginas nas quais você gostaria de renderizar uma experiência personalizada. Eles `decisionScopes` são personalizáveis e definidos pelo usuário. Para clientes atuais do Público alvo, `decisionScopes` também são conhecidos como &quot;mboxes&quot;. Na interface do Público alvo, `decisionScopes` apareça como &quot;locais&quot;.

## __Escopo da visualização__

O AEP Web SDK fornece uma funcionalidade na qual você pode recuperar ações VEC sem depender do AEP Web SDK para renderizar as ações VEC para você. Envie um evento com `__view__` definição de `decisionScopes`.

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

Ao definir Audiências para as atividades do Público alvo que serão entregues por meio do SDK da Web do AEP, o [XDM](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html) deve ser definido e usado. Depois de definir schemas XDM, classes e combinações, você pode criar uma regra de audiência de Público alvo definida pelos dados XDM para definição de metas. No Público alvo, os dados XDM são exibidos no Construtor de Audiências como um parâmetro personalizado. O XDM é serializado usando a notação de pontos (por exemplo, `web.webPageDetails.name`).

Se você tiver atividades Públicos alvos com audiências predefinidas que usam parâmetros personalizados ou um perfil de usuário, lembre-se de que elas não serão entregues corretamente pelo SDK da Web AEP. Em vez de usar parâmetros personalizados ou o perfil do usuário, você deve usar o XDM. Entretanto, há campos de direcionamento de audiência prontos para uso compatíveis com o SDK da Web do AEP que não exigem o XDM. Estes são os campos disponíveis na interface do Público alvo que não exigem o XDM:

* Biblioteca do Target
* Geografia  
* Rede
* Sistema operacional
* Páginas do site
* Navegador
* Fontes de Tráfego
* Intervalo de tempo

## Terminologia

__Decisões__ - No Público alvo, elas estão correlacionadas à experiência selecionada de uma Atividade.

__Âmbito__ - Âmbito de aplicação da decisão. Em Público alvo, esta é a mBox. A mBox global é o `__view__` escopo.

__Schema__ - O schema de uma decisão é o tipo de oferta no Público alvo.

__XDM__ - o XDM é serializado em notação de pontos e colocado em Público alvo como parâmetros mBox.
