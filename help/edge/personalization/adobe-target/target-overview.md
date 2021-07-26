---
title: Uso do Adobe Target com o SDK da Web da plataforma
description: Saiba como renderizar conteúdo personalizado com o SDK da Web do Experience Platform usando o Adobe Target
keywords: target; adobe target; activity.id; experience.id; renderDecisões; decisionScopes; pré-ocultar trecho; vec; Experience Composer baseado em formulário; xdm; públicos-alvo; decisões; escopo; esquema; diagrama do sistema; diagrama
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c99bc94226b296463e92340723d1318e0775f6a7
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 5%

---

# Usar [!DNL Adobe Target] com o [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] O pode entregar e renderizar experiências personalizadas gerenciadas no  [!DNL Adobe Target] para o canal da Web. Você pode usar um editor WYSIWYG, chamado [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou uma interface não visual, o [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), para criar, ativar e entregar suas atividades e experiências de personalização.

Os seguintes recursos foram testados e atualmente são compatíveis em [!DNL Target]:

* [Testes A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [Relatórios de impressão e conversão do A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=pt-BR)
* [Atividades do Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Atividades de Direcionamento de experiência](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Testes multivariados (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Atividades do Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Relatório de impressão e conversão do Target nativo](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [Suporte ao VEC](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] diagrama do sistema

O diagrama a seguir ajuda você a entender o fluxo de trabalho das [!DNL Target] e [!DNL Platform Web SDK] decisões de borda.

![Diagrama da decisão de borda do Adobe Target com o SDK da Web da plataforma](./assets/target-platform-web-sdk.png)

| Chame | Detalhes |
| --- | --- |
| 1 | O dispositivo carrega o [!DNL Platform Web SDK]. O [!DNL Platform Web SDK] envia uma solicitação para a rede de borda com dados XDM, a ID do ambiente de datastreams, parâmetros transmitidos e a ID do cliente (opcional). A página (ou contêineres) é pré-oculta. |
| 2 | A rede de borda envia a solicitação aos serviços de borda para enriquecê-la com a ID do visitante, o consentimento e outras informações de contexto do visitante, como localização geográfica e nomes amigáveis ao dispositivo. |
| 3 | A rede de borda envia a solicitação de personalização enriquecida para a borda [!DNL Target] com a ID do visitante e os parâmetros transmitidos. |
| 4 | Os scripts de perfil executam e, em seguida, fazem o feed no armazenamento de perfil [!DNL Target]. O armazenamento de perfil busca segmentos da [!UICONTROL Biblioteca de público-alvo] (por exemplo, segmentos compartilhados de [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | Com base nos parâmetros de solicitação de URL e dados de perfil, [!DNL Target] determina quais atividades e experiências serão exibidas para o visitante na exibição de página atual e para exibições futuras pré-buscadas. [!DNL Target] em seguida, envia isso de volta para a rede de borda. |
| 6 | a. A rede de borda envia a resposta de personalização de volta para a página, incluindo, opcionalmente, valores de perfil para personalização adicional. O conteúdo personalizado na página atual é revelado o mais rápido possível sem cintilação do conteúdo padrão.<br>b. O conteúdo personalizado para exibições que são mostradas como resultado das ações do usuário em um Aplicativo de página única (SPA) é armazenado em cache para que possa ser aplicado instantaneamente, sem uma chamada de servidor adicional, quando as exibições forem acionadas. &#x200B;<br>c. A rede de borda envia a ID do visitante e outros valores em cookies, como consentimento, ID da sessão, identidade, verificação de cookie, personalização e assim por diante. |
| 7 | A rede de borda encaminha [!UICONTROL os detalhes do Analytics for Target] (A4T) (metadados de atividade, experiência e conversão) para o &#x200B; de borda [!DNL Analytics]. |

## Ativar [!DNL Adobe Target]

Para ativar [!DNL Target], faça o seguinte:

1. Ative [!DNL Target] em seu [datastream](../../fundamentals/datastreams.md) com o código de cliente apropriado.
1. Adicione a opção `renderDecisions` aos eventos.

Em seguida, opcionalmente, também é possível adicionar as seguintes opções:

* **`decisionScopes`**: Recupere atividades específicas (úteis para atividades criadas com o compositor baseado em formulário) adicionando essa opção aos eventos.
* **[Pré-ocultar trecho](../manage-flicker.md)**: Ocultar apenas determinadas partes da página.

## Uso do VEC do Adobe Target

Para usar o VEC com uma implementação [!DNL Platform Web SDK], instale e ative a extensão de ajuda do VEC do [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) ou [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak).

Para obter mais informações, consulte [Extensão de assistente do Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) no *Guia do Adobe Target*.

## Atividades do VEC de renderização automática

O [!DNL Adobe Experience Platform Web SDK] tem o poder de renderizar automaticamente suas experiências definidas por meio do VEC do [!DNL Adobe Target] na Web para seus usuários. Para indicar [!DNL Experience Platform Web SDK] para renderizar automaticamente atividades do VEC, envie um evento com `renderDecisions = true`:

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

O [Experience Composer baseado em formulário](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) é uma interface não visual que é útil para configurar [!UICONTROL Testes A/B], [!UICONTROL Direcionamento de experiência], [!UICONTROL Automated Personalization] e [!UICONTROL Recommendations] atividades com diferentes tipos de resposta, como JSON, HTML, Imagem etc. Dependendo do tipo de resposta ou da decisão retornada por [!DNL Target], a lógica de negócios principal pode ser executada. Para recuperar as decisões das atividades do Composer baseado em formulário, envie um evento com todos os &quot;Deciscopes&quot; para os quais deseja recuperar uma decisão.

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

`decisionScopes` defina seções, locais ou partes de suas páginas em que você deseja renderizar uma experiência personalizada. Esses `decisionScopes` são personalizáveis e definidos pelo usuário. Para clientes atuais [!DNL Target], `decisionScopes` também são conhecidas como &quot;mboxes&quot;. Na interface [!DNL Target], `decisionScopes` aparece como &quot;locais&quot;.

## O `__view__` Escopo

O [!DNL Experience Platform Web SDK] fornece funcionalidade para recuperar ações do VEC sem depender do SDK para renderizar as ações do VEC para você. Envie um evento com `__view__` definido como um `decisionScopes`.

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

Ao definir públicos para suas atividades [!DNL Target] que são entregues por meio do [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR) deve ser definido e usado. Depois de definir esquemas, classes e grupos de campos de esquema XDM, você pode criar uma regra de público-alvo [!DNL Target] definida pelos dados XDM para direcionamento. Em [!DNL Target], os dados do XDM são exibidos no [!UICONTROL Audience Builder] como um parâmetro personalizado. O XDM é serializado usando notação de pontos (por exemplo, `web.webPageDetails.name`).

Se você tiver [!DNL Target] atividades com públicos-alvo predefinidos que usam parâmetros personalizados ou um perfil de usuário, elas não serão entregues corretamente por meio do SDK. Em vez de usar parâmetros personalizados ou o perfil do usuário, você deve usar o XDM. No entanto, há campos de direcionamento de público-alvo prontos para uso compatíveis por meio do [!DNL Platform Web SDK] que não exigem XDM. Esses campos estão disponíveis na interface [!DNL Target] que não requer XDM:

* Biblioteca do Target
* Geografia
* Rede
* Operating System
* Páginas do site
* Navegador
* Fontes de Tráfego
* Intervalo de tempo

Para obter mais informações, consulte [Categorias para públicos](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) no *Guia do Adobe Target*.

### Atualização de perfil único

O [!DNL Platform Web SDK] permite atualizar o perfil para o perfil [!DNL Target] e para o [!DNL Platform Web SDK] como um evento de experiência.

Para atualizar um perfil [!DNL Target], verifique se os dados do perfil foram passados com o seguinte:

* Em `“data {“`
* Em `“__adobe.target”`
* Prefixo `“profile.”`, por exemplo, como abaixo

| Chave | Tipo | Descrição |
| --- | --- | --- |
| `renderDecisions` | Booleano | Instrui o componente de personalização se ele deve interpretar ações DOM |
| `decisionScopes` | Matriz `<String>` | Uma lista de escopos para recuperar decisões de |
| `xdm` | Objeto | Dados formatados no XDM que chegam ao SDK da Web da plataforma como um evento de experiência |
| `data` | Objeto | Pares de valor/chave arbitrária enviados para soluções [!DNL Target] na classe de destino. |

O código [!DNL Platform Web SDK] típico usando esse comando é semelhante ao seguinte:

**`sendEvent`com dados de perfil**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Como enviar atributos de perfil para o Adobe Target:**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Solicitar recomendações

A tabela a seguir lista [!DNL Recommendations] atributos e se cada um é suportado por meio de [!DNL Platform Web SDK]:

| Categoria | Atributo | Status de suporte |
| --- | --- | --- |
| Recommendations - Atributos de entidade padrão | entity.id | Suportado |
|  | entity.name | Suportado |
|  | entity.categoryId | Suportado |
|  | entity.pageUrl | Suportado |
|  | entity.thumbnailUrl | Suportado |
|  | entity.message | Suportado |
|  | entity.value | Suportado |
|  | entity.inventory | Suportado |
|  | entity.brand | Suportado |
|  | entity.margin | Suportado |
|  | entity.event.detailsOnly | Suportado |
| Recommendations - Atributos de entidade personalizados | entity.yourCustomAttributeName | Suportado |
| Recommendations - Parâmetros de mbox/página reservados | excludedIds | Suportado |
|  | cartIds | Suportado |
|  | productPurchasedId | Suportado |
| Página ou categoria do item para afinidade de categorias | user.categoryId | Suportado |

**Como enviar atributos do Recommendations para o Adobe Target:**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## Depuração

mboxTrace e mboxDebug foram descontinuadas. Use [[!DNL Platform Web SDK] depurando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologia

__Decisões:__ No  [!DNL Target], as decisões estão relacionadas à experiência selecionada em uma Atividade.

__Esquema:__ O schema de uma decisão é o tipo de oferta no  [!DNL Target].

__Âmbito de aplicação:__ âmbito de aplicação da decisão. Em [!DNL Target], o escopo é a mBox. A mBox global é o escopo `__view__`.

__XDM:__ o XDM é serializado na notação de pontos e, em seguida, colocado  [!DNL Target] como parâmetros mBox.
