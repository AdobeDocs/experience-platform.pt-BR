---
title: Integrar o suporte ao IAB TCF 2.0 usando tags e a extensão Experience Platform Web SDK
description: Saiba como configurar o consentimento da TCF 2.0 do IAB com tags e a extensão Adobe Experience Platform Web SDK.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Integre o suporte ao IAB TCF 2.0 usando tags e a extensão Experience Platform Web SDK

O Adobe Experience Platform Web SDK é compatível com a Estrutura de transparência e consentimento interativa do Advertising Bureau, versão 2.0 (IAB TCF 2.0). Este guia mostra como configurar uma propriedade de tag para enviar informações de consentimento da TCF 2.0 do IAB para a Adobe usando a extensão de tag do Adobe Experience Platform Web SDK.

Se você não quiser usar marcas, consulte o manual sobre [uso do IAB TCF 2.0 sem marcas](./without-tags.md).

## Introdução

Para usar o IAB TCF 2.0 com tags e a extensão Experience Platform Web SDK, é necessário ter um esquema XDM e um conjunto de dados disponíveis.

Além disso, este guia requer que você tenha uma compreensão funcional do Adobe Experience Platform Web SDK. Para obter uma atualização rápida, leia a [visão geral do Adobe Experience Platform Web SDK](../../home.md) e a documentação de [Perguntas frequentes](../../faq.md).

## Definição do consentimento padrão

Na configuração da extensão, há uma configuração para consentimento padrão. Isso controla o comportamento dos clientes que não têm um cookie de consentimento. Se quiser enfileirar Eventos de Experiência para clientes que não têm um cookie de consentimento, defina como `pending`. Se quiser descartar os Eventos de Experiência para clientes que não têm um cookie de consentimento, defina como `out`. Você também pode usar um elemento de dados para definir dinamicamente o valor de consentimento padrão. Consulte [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) para obter mais informações.

## Atualização do perfil com informações de consentimento {#consent-code-1}

Para chamar a ação [`setConsent`](/help/web-sdk/commands/setconsent.md) quando as preferências de consentimento dos clientes forem alteradas, crie uma regra de marca. Comece adicionando um novo evento e escolha o tipo de evento &quot;Código personalizado&quot; da extensão principal.

Use a seguinte amostra de código para o seu novo evento:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Esse código personalizado faz duas coisas:

* Define dois elementos de dados, um com a cadeia de consentimento e outro com o sinalizador `gdprApplies`. Isso é útil posteriormente ao preencher a ação &quot;Definir consentimento&quot;.

* Aciona a regra quando as preferências de consentimento foram alteradas. A ação &quot;Definir consentimento&quot; deve ser usada sempre que as preferências de consentimento forem alteradas. Adicione uma ação &quot;Definir consentimento&quot; na extensão e preencha o formulário da seguinte maneira:

* Padrão: &quot;IAB TCF&quot;
* Versão: &quot;2.0&quot;
* Valor: &quot;%IAB Cadeia de Consentimento TCF%&quot;
* O GDPR se aplica: &quot;%IAB TCF Consent GDPR%&quot;

![Ação de consentimento de definição de IAB](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Não é possível escolher esses elementos de dados usando o seletor de elementos de dados porque eles foram criados por meio de código personalizado. Você deve digitar o nome do elemento de dados com os sinais de porcentagem. Esse código atualiza o perfil do cliente com as novas preferências de consentimento sempre que ele mudar. Além disso, o servidor retorna um valor de cookie, o que pode impedir que o Adobe Experience Platform Web SDK grave Eventos de experiência.

## Criação de um elemento de dados XDM para eventos de experiência

A cadeia de consentimento deve ser incluída no Evento de experiência XDM. Para fazer isso, use o elemento de dados Objeto XDM. Comece criando um novo elemento de dados Objeto XDM ou, como alternativa, use um que você já criou para enviar eventos. Se você tiver adicionado o grupo de campos do esquema Privacidade do evento de experiência ao esquema, deverá ter uma chave `consentStrings` no objeto XDM.

1. Selecione **[!UICONTROL consentStrings]**.

1. Escolha **[!UICONTROL Fornecer itens individuais]** e selecione **[!UICONTROL Adicionar Item]**.

1. Expanda o cabeçalho **[!UICONTROL consentString]**, expanda o primeiro item e preencha os seguintes valores:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %cadeia de caracteres de consentimento da TCF do IAB%
* `gdprApplies`: %GDPR% de Consentimento da TCF do IAB

>[!IMPORTANT]
>
>Não é possível escolher esses elementos de dados usando o seletor de elementos de dados porque eles foram criados por meio de código personalizado. Você deve digitar o nome do elemento de dados com os sinais de porcentagem.

## Envio de um evento de experiência inicial com informações de consentimento da TCF 2.0 do IAB

Se o Evento de experiência inicial na página for acionado com um evento de carregamento de página, a cadeia de consentimento pode ainda não ter sido carregada. Essa regra destina-se a substituir o evento de carregamento de página atual. Para garantir que as informações de consentimento sejam carregadas primeiro, crie uma nova regra e adicione o seguinte código como um evento de código personalizado:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Este código é idêntico ao código personalizado anterior, exceto que os eventos `useractioncomplete` e `tcloaded` são manipulados. O [código personalizado anterior](#consent-code-1) só é acionado quando o cliente escolhe suas preferências pela primeira vez. Esse código também será acionado quando o cliente já tiver escolhido suas preferências. Por exemplo, no segundo carregamento de página.

Adicione a ação &quot;Enviar evento&quot; da extensão do Experience Platform Web SDK. No campo XDM, escolha o elemento de dados XDM criado na seção anterior.

## Envio de outros eventos com informações de consentimento da TCF 2.0 do IAB

Quando os eventos são acionados após o Evento de experiência inicial, os dois elementos de dados ainda são definidos e podem ser usados para enviar as informações de consentimento do IAB. Use o mesmo elemento de dados XDM para enviar eventos futuros. As informações da TCF 2.0 do IAB estão incluídas.

## Próximas etapas

Agora que você aprendeu a usar a TCF do IAB 2.0 com a extensão do Experience Platform Web SDK, também é possível optar por integrar a outras soluções da Adobe, como o Adobe Analytics ou o Adobe Real-Time Customer Data Platform. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
