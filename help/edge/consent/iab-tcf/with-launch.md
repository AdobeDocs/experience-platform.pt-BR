---
title: Integrar o suporte do IAB TCF 2.0 usando tags e a extensão do SDK da Web da plataforma
description: Saiba como configurar o consentimento do IAB TCF 2.0 com tags e a extensão do Adobe Experience Platform Web SDK.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Integre o suporte ao IAB TCF 2.0 usando tags e a extensão SDK da Web da plataforma

O SDK da Web da Adobe Experience Platform é compatível com a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (TCF do IAB 2.0). Este guia mostra como configurar uma propriedade de tag para enviar informações de consentimento do IAB TCF 2.0 para o Adobe usando a extensão de tag do Adobe Experience Platform Web SDK.

Se você não deseja usar tags, consulte o guia em [usar o IAB TCF 2.0 sem tags](./without-launch.md).

## Introdução

Para usar o TCF 2.0 do IAB com tags e a extensão SDK da Web da plataforma, é necessário ter um esquema XDM e conjunto de dados disponíveis.

Além disso, este guia requer que você tenha uma compreensão funcional do SDK da Web da Adobe Experience Platform. Para obter um atualizado rápido, leia a [Visão geral do SDK da Web da Adobe Experience Platform](../../home.md) e a documentação de [Perguntas frequentes](../../web-sdk-faq.md).

## Configuração do consentimento padrão

Na configuração da extensão, há uma configuração para consentimento padrão. Isso controla o comportamento dos clientes que não têm um cookie de consentimento. Se você quiser colocar na fila Eventos de experiência para clientes que não têm um cookie de consentimento, defina como `pending`. Se quiser descartar os Eventos de experiência para clientes que não têm um cookie de consentimento, defina como `out`. Você também pode usar um elemento de dados para definir dinamicamente o valor de consentimento padrão.

Para obter mais informações sobre como configurar o consentimento padrão, consulte a [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) no guia de configuração do SDK.

## Atualização do perfil com informações de consentimento {#consent-code-1}

Para chamar a ação `setConsent` quando as preferências de consentimento dos clientes forem alteradas, é necessário criar uma nova regra de tag. Comece adicionando um novo evento e escolha o tipo de evento &quot;Código personalizado&quot; da extensão principal.

Use a seguinte amostra de código para o novo evento:

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

Este código personalizado faz duas coisas:

* Define dois elementos de dados, um com a cadeia de consentimento e outro com o sinalizador `gdprApplies`. Isso é útil posteriormente ao preencher a ação &quot;Definir consentimento&quot;.

* Aciona a regra quando as preferências de consentimento são alteradas. A ação &quot;Definir consentimento&quot; deve ser usada sempre que as preferências de consentimento forem alteradas. Adicione uma ação &quot;Definir consentimento&quot; na extensão e preencha o formulário da seguinte maneira:

* Padrão: &quot;TCF do IAB&quot;
* Versão: &quot;2.0&quot;
* Valor: &quot;%Cadeia de consentimento da TCF do IAB%&quot;
* O GDPR se aplica: &quot;%IAB TCF Consentimento GDPR%&quot;

![Ação de consentimento do conjunto IAB](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Não é possível escolher esses elementos de dados usando o seletor de elemento de dados porque eles foram criados por meio do código personalizado. Você deve digitar o nome do elemento de dados com os sinais de porcentagem. Esse código atualiza o perfil do cliente com suas novas preferências de consentimento sempre que elas mudam. Além disso, o servidor retorna um valor de cookie, o que pode impedir que o SDK da Web da Adobe Experience Platform registre os Eventos de experiência.

## Criar um elemento de dados XDM para eventos de experiência

A cadeia de consentimento deve ser incluída no Evento de experiência XDM. Para fazer isso, use o elemento de dados Objeto XDM. Comece criando um novo elemento de dados Objeto XDM ou, alternativamente, use um que já tenha criado para enviar eventos. Se você tiver adicionado o grupo de campos Privacidade de eventos de experiência ao esquema, deverá ter uma chave `consentStrings` no objeto XDM.

1. Selecione **[!UICONTROL consentStrings]**.

1. Escolha **[!UICONTROL Fornecer itens individuais]** e selecione **[!UICONTROL Adicionar Item]**.

1. Expanda o cabeçalho **[!UICONTROL consentString]** e expanda o primeiro item, em seguida, preencha os seguintes valores:

* `consentStandard`: TCF do IAB
* `consentStandardVersion`: 2,0
* `consentStringValue`: %Cadeia de consentimento da TCF do IAB%
* `gdprApplies`: %GDPR de consentimento da TCF do IAB%

>[!IMPORTANT]
>
>Não é possível escolher esses elementos de dados usando o seletor de elemento de dados porque eles foram criados por meio do código personalizado. Você deve digitar o nome do elemento de dados com os sinais de porcentagem.

## Envio de um evento de experiência inicial com informações de consentimento do IAB TCF 2.0

Se o Evento de experiência inicial na página for acionado com um evento de carregamento de página, a cadeia de consentimento talvez ainda não tenha sido carregada. Essa regra tem como objetivo substituir o evento de carregamento de página atual. Para garantir que as informações de consentimento sejam carregadas primeiro, crie uma nova regra e adicione o seguinte código como um evento de código personalizado:

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

Esse código é idêntico ao código personalizado anterior, exceto que os eventos `useractioncomplete` e `tcloaded` são manipulados. O [código personalizado anterior](#consent-code-1) só é acionado quando o cliente escolhe suas preferências pela primeira vez. Esse código também é acionado quando o cliente já escolheu suas preferências. Por exemplo, no segundo carregamento da página.

Adicione uma ação &quot;Enviar evento&quot; da extensão SDK da Web da plataforma. No campo XDM , escolha o elemento de dados XDM criado na seção anterior.

## Envio de outros eventos com informações de consentimento do IAB TCF 2.0

Quando os eventos são acionados após o evento de experiência inicial, os dois elementos de dados ainda são definidos e podem ser usados para enviar as informações de consentimento do IAB. Use o mesmo elemento de dados XDM para enviar eventos futuros. As informações do TCF 2.0 do IAB são incluídas.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão SDK da Web da plataforma, também pode optar por integrar com outras soluções do Adobe, como a Adobe Analytics ou a Plataforma de dados do cliente em tempo real. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
