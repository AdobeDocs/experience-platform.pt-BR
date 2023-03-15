---
title: Integrar o suporte ao IAB TCF 2.0 usando tags e a extensão SDK da Web da plataforma
description: Saiba como configurar o consentimento da TCF 2.0 do IAB com tags e a extensão SDK da Web da Adobe Experience Platform.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Integrar o suporte ao IAB TCF 2.0 usando tags e a extensão SDK da Web da plataforma

O SDK da Web da Adobe Experience Platform é compatível com a Estrutura de transparência e consentimento interativa do Advertising Bureau, versão 2.0 (IAB TCF 2.0). Este guia mostra como configurar uma propriedade de tag para enviar informações de consentimento da TCF do IAB 2.0 para o Adobe usando a extensão de tag do SDK da Web da Adobe Experience Platform.

Se não quiser usar tags, consulte o manual no [uso do IAB TCF 2.0 sem tags](./without-launch.md).

## Introdução

Para usar o IAB TCF 2.0 com tags e a extensão SDK da Web da plataforma, é necessário ter um esquema XDM e um conjunto de dados disponíveis.

Além disso, este guia requer que você tenha uma compreensão funcional do SDK da Web da Adobe Experience Platform. Para uma atualização rápida, leia o [Visão geral do SDK da Web do Adobe Experience Platform](../../home.md) e a variável [Perguntas frequentes](../../web-sdk-faq.md) documentação.

## Definição do consentimento padrão

Na configuração da extensão, há uma configuração para consentimento padrão. Isso controla o comportamento dos clientes que não têm um cookie de consentimento. Se quiser enfileirar Eventos de experiência para clientes que não têm um cookie de consentimento, defina como `pending`. Se quiser descartar Eventos de experiência para clientes que não têm um cookie de consentimento, defina como `out`. Você também pode usar um elemento de dados para definir dinamicamente o valor de consentimento padrão.

Para obter mais informações sobre como configurar o consentimento padrão, consulte o [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) no guia de configuração do SDK.

## Atualização do perfil com informações de consentimento {#consent-code-1}

Para chamar o `setConsent` ação quando as preferências de consentimento dos clientes forem alteradas, será necessário criar uma nova regra de tag. Comece adicionando um novo evento e escolha o tipo de evento &quot;Código personalizado&quot; da extensão principal.

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

* Define dois elementos de dados, um com a cadeia de consentimento e outro com a variável `gdprApplies` sinalizador. Isso é útil posteriormente ao preencher a ação &quot;Definir consentimento&quot;.

* Aciona a regra quando as preferências de consentimento foram alteradas. A ação &quot;Definir consentimento&quot; deve ser usada sempre que as preferências de consentimento forem alteradas. Adicione uma ação &quot;Definir consentimento&quot; na extensão e preencha o formulário da seguinte maneira:

* Padrão: &quot;IAB TCF&quot;
* Versão: &quot;2.0&quot;
* Valor: &quot;%IAB Cadeia de Consentimento TCF%&quot;
* O GDPR se aplica: &quot;%IAB TCF Consent GDPR%&quot;

![Ação Definir consentimento IAB](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Não é possível escolher esses elementos de dados usando o seletor de elementos de dados porque eles foram criados por meio de código personalizado. Você deve digitar o nome do elemento de dados com os sinais de porcentagem. Esse código atualiza o perfil do cliente com as novas preferências de consentimento sempre que ele mudar. Além disso, o servidor retorna um valor de cookie, o que pode impedir que o SDK da Web da Adobe Experience Platform grave Eventos de experiência.

## Criação de um elemento de dados XDM para eventos de experiência

A cadeia de consentimento deve ser incluída no Evento de experiência XDM. Para fazer isso, use o elemento de dados Objeto XDM. Comece criando um novo elemento de dados Objeto XDM ou, como alternativa, use um que você já criou para enviar eventos. Se você tiver adicionado o grupo de campos de esquema Privacidade de evento de experiência ao esquema, deverá ter um `consentStrings` no objeto XDM.

1. Selecionar **[!UICONTROL consentStrings]**.

1. Escolher **[!UICONTROL Fornecer itens individuais]** e selecione **[!UICONTROL Adicionar item]**.

1. Expanda a **[!UICONTROL consentString]** e expanda o primeiro item e, em seguida, preencha os seguintes valores:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %Cadeia de caracteres de consentimento da TCF do IAB%
* `gdprApplies`: %IAB TCF Consentimento GDPR%

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

Este código é idêntico ao código personalizado anterior, exceto que ambos `useractioncomplete` e `tcloaded` eventos são manipulados. A variável [código personalizado anterior](#consent-code-1) O só será acionado quando o cliente escolher suas preferências pela primeira vez. Esse código também será acionado quando o cliente já tiver escolhido suas preferências. Por exemplo, no segundo carregamento de página.

Adicione a ação &quot;Enviar evento&quot; da extensão SDK da Web da plataforma. No campo XDM, escolha o elemento de dados XDM criado na seção anterior.

## Envio de outros eventos com informações de consentimento da TCF 2.0 do IAB

Quando os eventos são acionados após o Evento de experiência inicial, os dois elementos de dados ainda são definidos e podem ser usados para enviar as informações de consentimento do IAB. Use o mesmo elemento de dados XDM para enviar eventos futuros. As informações da TCF 2.0 do IAB estão incluídas.

## Próximas etapas

Agora que você aprendeu a usar o IAB TCF 2.0 com a extensão SDK da Web da plataforma, também é possível optar por integrar com outras soluções de Adobe, como Adobe Analytics ou Adobe Real-time Customer Data Platform. Consulte a [Visão geral da Estrutura de transparência e consentimento 2.0 do IAB](./overview.md) para obter mais informações.
