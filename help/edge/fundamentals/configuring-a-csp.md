---
title: Configuração de um CSP
seo-title: Configuração de um CSP para Adobe Experience Platform Web SDK
description: Saiba como configurar um CSP para o SDK da Web do Experience Platform
seo-description: Saiba como configurar um CSP para o SDK da Web do Experience Platform
keywords: configuração;configuração;SDK;borda;Web SDK;configurar;contexto;web;dispositivo;ambiente;configurações do Web sdk;política de segurança de conteúdo;
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# Configuração de um CSP

Uma [Política de Segurança de Conteúdo](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) é usada para restringir os recursos que um navegador está autorizado a usar. O CSP também pode limitar a funcionalidade dos recursos de script e estilo. O Adobe Experience Platform Web SDK não requer um CSP, mas adicionar um pode reduzir a superfície do ataque para evitar ataques mal-intencionados.

O CSP precisa refletir como [!DNL Platform Web SDK] é implantado e configurado. O CSP a seguir mostra quais alterações podem ser necessárias para que o SDK funcione corretamente. Outras configurações de CSP provavelmente serão necessárias, dependendo do seu ambiente específico.

## Exemplo de política de segurança de conteúdo

Os exemplos a seguir mostram como configurar um CSP.

### Permitir acesso ao domínio de borda

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

No exemplo acima, `EDGE-DOMAIN` deve ser substituído pelo domínio primário. O domínio primário está configurado para a configuração [edgeDomain](configuring-the-sdk.md#edge-domain). Se nenhum domínio primário tiver sido configurado, `EDGE-DOMAIN` deverá ser substituído por `*.adobedc.net`. Se a migração de visitantes estiver ativada usando [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), a diretiva `connect-src` também precisará incluir `*.demdex.net`.

### Usar NONCE para permitir scripts e elementos de estilo em linha

[!DNL Platform Web SDK] pode modificar o conteúdo da página e deve ser aprovado para criar scripts em linha e tags de estilo. Para fazer isso, o Adobe recomenda usar um nonce para a diretiva CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Um nonce é um token aleatório gerado pelo servidor e criptografado que é gerado uma vez por cada visualização de página exclusiva.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Além disso, o CSP nonce precisa ser adicionado como um atributo à tag de script [!DNL Platform Web SDK] [base code](installing-the-sdk.md#adding-the-code). [!DNL Platform Web SDK] usará esse nonce ao adicionar script em linha ou tags de estilo à página:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Se um nonce não for usado, a outra opção é adicionar `unsafe-inline` às diretivas CSP `script-src` e `style-src`:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>O Adobe **não** recomenda especificar `unsafe-inline` porque permite que qualquer script seja executado na página, o que limita os benefícios do CSP.
