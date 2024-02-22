---
title: Configurar uma CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Saiba como configurar uma CSP para o SDK da Web do Experience Platform
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurando;configuração;SDK;borda;SDK da Web;configurar;contexto;web;dispositivo;ambiente;configurações do sdk da web;política de segurança de conteúdo;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 099f87acded9eca31c31555e63c0ea49ae2d1719
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configurar uma CSP

A [Política de segurança de conteúdo](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) O (CSP) é usado para restringir os recursos que um navegador pode usar. A CSP também pode limitar a funcionalidade de recursos de script e estilo. O Adobe Experience Platform Web SDK não requer um CSP, mas adicionar um pode reduzir a superfície de ataque para impedir ataques mal-intencionados.

O documento de estratégia por país deve [!DNL Platform Web SDK] é implantado e configurado. A CSP a seguir mostra quais alterações podem ser necessárias para que o SDK funcione corretamente. Configurações adicionais da CSP provavelmente serão necessárias, dependendo do seu ambiente específico.

## Exemplo de política de segurança de conteúdo

Os exemplos a seguir mostram como configurar uma CSP.

### Permitir acesso ao domínio de borda

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

No exemplo acima, `EDGE-DOMAIN` deve ser substituído pelo domínio próprio. O domínio próprio é configurado para o [edgeDomain](configuring-the-sdk.md#edge-domain) configuração. Se nenhum domínio próprio tiver sido configurado, `EDGE-DOMAIN` deve ser substituída por `*.adobedc.net`. Se a migração do visitante estiver ativada usando [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), o `connect-src` a diretiva também deve incluir `*.demdex.net`.

### Usar NONCE para permitir script incorporado e elementos de estilo

[!DNL Platform Web SDK] O pode modificar o conteúdo da página e deve ser aprovado para criar tags de script e estilo em linha. Para fazer isso, o Adobe recomenda o uso de um nonce para o [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) Diretiva CSP. Um nonce é um token aleatório criptograficamente forte gerado pelo servidor gerado uma vez para cada exibição de página exclusiva.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Além disso, o nonce CSP precisa ser adicionado como um atributo à variável [!DNL Platform Web SDK] [código base](installing-the-sdk.md#adding-the-code) tag de script. [!DNL Platform Web SDK] O usará esse nonce ao adicionar scripts incorporados ou tags de estilo à página:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Se um nonce não for usado, a outra opção será adicionar `unsafe-inline` para o `script-src` e `style-src` Diretivas da CSP:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>O Adobe faz **não** recomendar especificação `unsafe-inline` porque permite que qualquer script seja executado na página, o que limita os benefícios da CSP.

## Configurar uma CSP para mensagens no aplicativo {#in-app-messaging}

Ao configurar [Mensagens no aplicativo da Web](../personalization/web-in-app-messaging.md), você deve incluir a seguinte diretiva na CSP:

```
default-src  blob:;
```
