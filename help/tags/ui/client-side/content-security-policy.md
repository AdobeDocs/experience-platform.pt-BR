---
title: Suporte à Política de segurança de conteúdo (CSP)
description: Saiba como lidar com restrições da Política de segurança de conteúdo (CSP) ao integrar seu site com tags no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 59%

---

# Suporte à Política de segurança de conteúdo (CSP)

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Uma Política de Segurança de Conteúdo (CSP) é um recurso de segurança que ajuda a impedir ataques de script entre sites (XSS). Isso acontece quando o navegador é enganado para executar conteúdo mal-intencionado que parece vir de uma fonte confiável, mas vem de outro lugar. As CSPs permitem que o navegador verifique (em nome do usuário) se o script realmente vem de uma fonte confiável.

As CSPs são implementadas adicionando um cabeçalho HTTP `Content-Security-Policy` às respostas do servidor ou adicionando um elemento `<meta>` configurado na seção `<head>` dos arquivos HTML.

>[!NOTE]
>
> Para obter informações mais detalhadas sobre a CSP, consulte os [documentos da Web do MDN](https://developer.mozilla.org/pt/docs/Web/HTTP/CSP).

As tags no Adobe Experience Platform são um sistema de gerenciamento de tags projetado para carregar scripts dinamicamente em seu site. Uma CSP padrão bloqueia esses scripts carregados dinamicamente devido a possíveis problemas de segurança. Este documento fornece orientação sobre como configurar a CSP para permitir scripts carregados dinamicamente de tags.

Se você quiser que as tags funcionem com sua CSP, há dois desafios principais a serem superados:

* **A origem da biblioteca de tags deve ser confiável.** Se essa condição não for atendida, a biblioteca de tags e outros arquivos JavaScript necessários serão bloqueados pelo navegador e não serão carregados na página.
* **Os scripts incorporados devem ser permitidos.** Se essa condição não for atendida, as ações de regra do Código personalizado serão bloqueadas na página e não serão executadas adequadamente.

O aumento da segurança requer um aumento da quantidade de trabalho em nome do criador de conteúdo. Se quiser usar tags e tiver uma CSP em vigor, será necessário corrigir esses problemas sem marcar outros scripts como confiáveis incorretamente. O resto deste documento fornece orientações sobre como fazer isso.

## Adicionar tags como uma fonte confiável

Ao usar uma CSP, você deve todos os domínios confiáveis dentro do valor do cabeçalho `Content-Security-Policy`. O valor que você deve fornecer para tags varia de acordo com o tipo de hospedagem que você está usando.

### Auto-hospedagem

Se sua biblioteca for de [auto-hospedagem](../publishing/hosts/self-hosting-libraries.md), a origem da build provavelmente se encontra em seu próprio domínio. Você pode especificar que o domínio host seja uma fonte segura usando a seguinte configuração:

**Cabeçalho HTTP**

```http
Content-Security-Policy: script-src 'self'
```

**Tag `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Hospedagem gerenciada pela Adobe

Se você estiver usando um [host gerenciado pela Adobe](../publishing/hosts/managed-by-adobe-host.md), sua build será mantida no `assets.adobedtm.com`. Você deve especificar `self` como um domínio seguro para não interromper nenhum script que já esteja carregando, mas também precisa que `assets.adobedtm.com` seja listado como seguro ou a biblioteca de tags não será carregada na página. Nesse caso, você deve usar a seguinte configuração:

**Cabeçalho HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**Tag `<meta>` HTML**


Há um pré-requisito muito importante: Você deve carregar a biblioteca de tags [de forma assíncrona](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/asynchronous-deployment.html?lang=pt-BR). Isso não funciona com uma carga síncrona da biblioteca de tags (o que resulta em erros e regras do console não serem executados corretamente).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

Você deve especificar o `self` como um domínio seguro para que todos os scripts que você já esteja carregando continuem funcionando, mas você também precisa que o `assets.adobedtm.com` seja listado como seguro ou a build da sua biblioteca não carregará na página.

## Scripts integrados

A CSP não permite scripts integrados por padrão e, portanto, deve ser configurada manualmente para permitir. Há duas opções para permitir scripts integrados:

* [Permitir por nonce](#nonce) (boa segurança)
* [Permitir todos os scripts integrados](#unsafe-inline) (menos seguro)

>[!NOTE]
>
>A especificação da CSP tem detalhes para uma terceira opção usando hashes, mas essa abordagem não é viável para ser usada com sistemas de gerenciamento de tags como tags. Para obter mais informações sobre as limitações do uso de hashes com tags na Platform, consulte o [guia de Integridade de sub-recursos (SRI)](./sri.md).

### Permitir por nonce {#nonce}

Esse método envolve gerar um nonce criptográfico e adicioná-lo à CSP e a cada script integrado no site. Quando o navegador recebe uma instrução para carregar um script integrado contendo um nonce, o navegador compara o valor do nonce com o que está contido no cabeçalho da CSP. Se corresponder, o script é carregado. Este nonce deve ser alterado a cada novo carregamento de página.

>[!IMPORTANT]
>
>Para usar esse método, é necessário carregar a build de forma assíncrona. Isso não funciona ao carregar a build de forma síncrona, pois resulta em erros e regras de console que não são executados corretamente. Consulte o guia sobre [implantação assíncrona](./asynchronous-deployment.md) para obter mais informações.

Os exemplos abaixo mostram como você pode adicionar o nonce à configuração da CSP para um host gerenciado pela Adobe. Se você estiver usando a hospedagem própria, é possível excluir o `assets.adobedtm.com`.

**Cabeçalho HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**Tag `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Depois de configurar o cabeçalho ou a tag HTML, é necessário indicar à tag onde localizar o nonce ao carregar um script integrado. Para que uma tag use o nonce ao carregar o script, é necessário:

1. Criar um elemento de dados que faça referência ao local em que o nonce está localizado na sua camada de dados.
1. Configure a Extensão principal e especifique o elemento de dados usado.
1. Publique seu elemento de dados e as alterações na Extensão principal.

>[!NOTE]
>
>O processo acima trata apenas do carregamento do código personalizado, não do que esse código personalizado faz. Se um script integrado tiver um código personalizado incompatível com a CSP, ela terá prioridade. Por exemplo, se você usar o código personalizado para carregar um script integrado ao anexá-lo ao DOM, a tag não poderá adicionar o nonce corretamente, de modo que determinada ação de código personalizado não funcionará conforme esperado.

### Permitir todos os scripts integrados {#unsafe-inline}

Se o uso de nonces não funcionar para você, é possível configurar a CSP para permitir todos os scripts integrados. Essa é a opção menos segura, mas também é mais fácil de implementar e manter.

Os exemplos abaixo mostram como permitir todos os scripts integrados no cabeçalho da CSP.

#### Auto-hospedagem

Use as seguintes configurações se estiver usando a hospedagem própria:

**Cabeçalho HTTP**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**Tag `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Hospedagem gerenciada pela Adobe

Use as seguintes configurações se estiver usando a hospedagem gerenciada pela Adobe:

**Cabeçalho HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**Tag `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Próximas etapas

Ao ler este documento, você deve entender como configurar o cabeçalho da CSP para aceitar o arquivo da biblioteca de tags e scripts integrados.

Como medida de segurança adicional, você também pode optar por usar a SRI (Integridade de sub-recursos) para validar builds de bibliotecas pesquisadas. No entanto, esse recurso tem algumas limitações importantes quando usado com sistemas de gerenciamento de tags, como tags. Consulte o guia sobre [compatibilidade com a SRI no Platform](./sri.md) para obter mais informações.
