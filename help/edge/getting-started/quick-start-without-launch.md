---
title: start rápido usando javascript simples
seo-title: 'start rápido do Adobe Experience Platform Web SDK '
description: Guia de start rápido para usar o Experience Platform Web SDK para coletar dados
seo-description: Guia de start rápido para usar o Experience Platform Web SDK para coletar dados
translation-type: tm+mt
source-git-commit: 8574a2d54c00f1bd3c41780fb12ff739a7d98fc3
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 5%

---


# Boas-vindas

Este guia o guia pelas diferentes maneiras de configurar o SDK da Web do Adobe Experience Platform. Para usar esse recurso, é necessário incluir uma lista de permissões. Se você quiser entrar na lista de espera, entre em contato com seu CSM.

- Ter um domínio [próprio (CNAME)](https://docs.adobe.com/content/help/pt-BR/core-services/interface/ec-cookies/cookies-first-party.html) habilitado. Se você já tiver um CNAME para Analytics, use esse. Testar no desenvolvimento funciona sem um CNAME, mas é necessário um antes de ir para a produção.
- Tenha direito ao Adobe Experience Platform.  Se você não tiver comprado a Platform, a Adobe fornecerá a Experience Platform Data Services Foundation para uso limitado com o SDK, sem custos adicionais.
- Use a versão mais recente do serviço de ID de Visitante.

## Criar uma ID de configuração

Você pode criar uma ID de configuração usando a ferramenta [de configuração de](../fundamentals/edge-configuration.md) borda no Adobe Launch, mesmo se não estiver usando os recursos de gerenciamento de tags. Isso permite que você ative o [!DNL Edge Network] para enviar dados para as várias soluções. Detalhes sobre como localizar cada opção são encontrados na Página da Ferramenta [de Configuração de](../fundamentals/edge-configuration.md) Borda.

>[!NOTE]
>
>Sua organização deve estar na lista de permissões do recurso. Entre em contato com seu CSM para colocar a lista de permissões.

## Preparar um Schema

O [!DNL Experience Platform Edge Network] assume os dados como XDM. O XDM é um formato de dados que permite definir schemas. O schema define como [!DNL Edge Network] espera que os dados sejam formatados. Para enviar dados, é necessário definir seu schema.

- [Criar um schema](../../xdm/tutorials/create-schema-ui.md)
- Adicione a combinação Adobe Experience Platform [!DNL Web SDK] ao schema criado

O vídeo a seguir tem o objetivo de oferecer suporte para a criação de um schema, conjunto de dados e conector de fonte de streaming para seus [!DNL Web SDK] dados.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Instalar o SDK

Para instalar o SDK, copie e cole o seguinte &quot;código base&quot; o mais alto possível na `<head>` tag do seu HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Para obter mais detalhes sobre diferentes opções para fazer isso, consulte [Instalação do SDK](../fundamentals/installing-the-sdk.md).

## Configurar o SDK

Em seguida, forneça sua configuração para o SDK. Isso é feito usando o `configure` comando. Esse deve ser o primeiro comando chamado em cada página.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Aqui, você fornece a ID de configuração criada acima, bem como a ID da empresa. Esses são os dois únicos campos obrigatórios. Entretanto, há muitas outras opções [](../fundamentals/configuring-the-sdk.md)de configuração.

## Enviar um evento

Depois de chamar o comando configure, você poderá acessar eventos de rastreamento de start.

```javascript
alloy("sendEvent", {});
```

Geralmente, você envia eventos com alguns dados. Você pode enviar dados XDM como este. Os dados enviados devem estar no schema criado no XDM.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

Para obter mais detalhes sobre como rastrear eventos, consulte [Rastreamento de Eventos](../fundamentals/tracking-events.md).

## Próximas etapas

Depois de ter os dados fluindo, você pode fazer o seguinte:

- [Crie seu schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html)
- [Saiba mais sobre como depurar](../fundamentals/debugging.md)
- Saiba como [personalizar a experiência](../fundamentals/rendering-personalization-content.md)
- Saiba mais sobre como enviar dados para várias soluções
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
