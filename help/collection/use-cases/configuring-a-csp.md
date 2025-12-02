---
title: Configurar uma CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Saiba como configurar uma CSP para o Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configurando;configuração;SDK;borda;Web SDK;configurar;contexto;web;dispositivo;ambiente;configurações do sdk da web;política de segurança de conteúdo;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configurar uma CSP

Uma [Política de Segurança de Conteúdo](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) é usada para restringir os recursos que um navegador pode usar. A CSP também pode limitar a funcionalidade de recursos de script e estilo. O Adobe Experience Platform Web SDK não requer um CSP, mas adicionar um pode reduzir a superfície de ataque para impedir ataques mal-intencionados.

A CSP precisa refletir como [!DNL Experience Platform Web SDK] é implantado e configurado. A CSP a seguir mostra quais alterações podem ser necessárias para que o SDK funcione corretamente. Configurações adicionais da CSP provavelmente serão necessárias, dependendo do seu ambiente específico.

## Exemplo de política de segurança de conteúdo

Os exemplos a seguir mostram como configurar uma CSP.

### Permitir acesso ao domínio de borda

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

No exemplo acima, `EDGE-DOMAIN` deve ser substituído pelo domínio próprio. O domínio próprio está configurado para a configuração [edgeDomain](../js/commands/configure/edgedomain.md). Se nenhum domínio próprio foi configurado, `EDGE-DOMAIN` deve ser substituído por `*.adobedc.net`. Se a migração do visitante estiver ativada usando [idMigrationEnabled](../js/commands/configure/idmigrationenabled.md), a diretiva `connect-src` também precisará incluir `*.demdex.net`.

### Usar NONCE para permitir script incorporado e elementos de estilo

[!DNL Experience Platform Web SDK] pode modificar o conteúdo da página e deve ser aprovado para criar marcas de script e estilo embutidas. Para fazer isso, a Adobe recomenda o uso de um nonce para a diretiva CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Um nonce é um token aleatório criptograficamente forte gerado pelo servidor gerado uma vez para cada exibição de página exclusiva.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Além disso, o nonce CSP precisa ser adicionado como um atributo à marca de script [!DNL Experience Platform Web SDK] [código base](../js/install/library.md). [!DNL Experience Platform Web SDK] usará esse nonce ao adicionar marcas de estilo ou script embutido à página:

```html
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Se um nonce não for usado, a outra opção será adicionar `unsafe-inline` às diretivas CSP `script-src` e `style-src`:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>A Adobe **não** recomenda especificar `unsafe-inline` porque ele permite que qualquer script seja executado na página, o que limita os benefícios da CSP.

## Configurar uma CSP para mensagens no aplicativo {#in-app-messaging}

Ao configurar mensagens no aplicativo da Web, você deve incluir a seguinte diretiva na CSP:

```
default-src  blob:;
```
