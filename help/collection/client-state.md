---
title: Gerenciamento de estado do cliente
description: Saiba como a Rede de borda da Adobe Experience Platform gerencia o estado do cliente
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: cliente;estado;gerenciamento;borda;rede;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# Gerenciamento de estado do cliente

A Rede de borda em si não tem estado (ela não mantém sua própria sessão). No entanto, há determinados casos de uso que exigem persistência de estado do lado do cliente, como:

* Identificação de dispositivo consistente (consulte [identificação do visitante](visitor-identification.md))
* Coletar e aplicar o consentimento do usuário
* Manter a ID da sessão de personalização

A Rede de borda usa um protocolo de gerenciamento de estado, delegando o aspecto de armazenamento ao cliente/SDK e inclui entradas de estado em suas respostas. Para navegadores, as entradas são armazenadas como cookies.

A responsabilidade do cliente é armazená-los e incluí-los em todas as solicitações subsequentes. O cliente também deve cuidar da expiração adequada das entradas, conforme instruído pelo gateway. Quando as entradas foram armazenadas como cookies, o navegador faz tudo isso automaticamente.

Embora as entradas de estado sempre tenham uma `String` (visível para o chamador/SDK), você não deve consumir nem alterar os valores de forma alguma. A estrutura/formato do valor ou até mesmo o próprio nome podem mudar a qualquer momento, o que pode levar a um comportamento inesperado dos clientes que usam o estado internamente. O estado deve ser sempre consumido pelo próprio gateway ou outros serviços de borda.

## Persistência do estado do cliente como metadados

O estado retornado pelo [!DNL Edge Network] no corpo da resposta é um `Handle` objeto com o tipo `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Atributo | Tipo | Descrição |
| --- | --- | --- |
| `key` | String | **Obrigatório**. O nome da entrada. |
| `value` | String | *Opcional*. O valor de entrada. |
| `maxAge` | Número inteiro | *Opcional* O tempo (em segundos) até a entrada expirar. Quando ausentes, as entradas devem ser armazenadas somente para a sessão atual. |
| `attrs` | `Map<String, String>` | *Opcional*. Uma lista opcional de atributos de entrada. Para todas as conexões seguras com um cabeçalho HTTP de referência segura, o `SameSite` atributo está definido como `None`. |


Para oferecer suporte à multimarcação (ou seja, várias instâncias do SDK na mesma propriedade, que possivelmente fazem referência a organizações diferentes), todas as entradas de estado recebem o prefixo automaticamente com `kndctr_` e a ID de organização segura para URL.

Quando o SDK do cliente recebe uma `state:store` na resposta, ela deve fazer o seguinte:

* Armazene entradas no lado do cliente, respeitando o tempo de expiração fornecido pelo gateway.
* Carregue-os do armazenamento do cliente e inclua todas as entradas não expiradas nas solicitações subsequentes.

Este é um exemplo de uma solicitação que passa no estado armazenado do lado do cliente:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## Persistência do estado do cliente em cookies do navegador

Ao trabalhar com clientes do navegador, a Rede de borda pode manter automaticamente as entradas como cookies do navegador. Isso permite o suporte ao armazenamento de estado transparente, já que os navegadores respeitam o protocolo de gerenciamento de estado por padrão.

Quase todas as entradas são materializadas como cookies próprios quando ativados e suportados (consulte a observação abaixo), mas o gateway também pode armazenar alguns cookies de terceiros quando o terceiro `adobedc.demdex.net` domínio é usado.

Como as entradas estão sempre vinculadas a um escopo específico (dispositivo/aplicativo) por sua definição, somente o subconjunto compatível com o contexto de solicitação atual será gravado pela Rede de borda. As entradas não gravadas são retornadas em um `state:store` identificador.

Como regra geral, as entradas com escopo de aplicativo são sempre gravadas como cookies primários, enquanto as entradas com escopo de dispositivo são gravadas como cookies de terceiros. A decisão é completamente transparente para o chamador, o gateway decide quais entradas podem ser gravadas, dependendo do contexto da chamada.

O chamador deve habilitar explicitamente o suporte para armazenar o estado do cliente como cookies, por meio do `meta.state.cookiesEnabled` sinalizador:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Atributo | Tipo | Descrição |
| --- | --- | --- |
| `cookiesEnabled` | Booleano | Quando definido, ativa o suporte para cookies. O valor padrão é `false`. |
| `domain` | String | Obrigatório ao `cookiesEnabled: true`. O domínio de nível superior no qual os cookies devem ser gravados. A Rede de borda usará esse valor para decidir se o estado pode ser mantido como cookies. |

Mesmo que o suporte a cookies seja ativado por meio da variável `cookiesEnabled` , a Rede de borda da Adobe Experience Platform só gravará as entradas de estado se o domínio de nível superior da solicitação corresponder ao `domain` especificado pelo chamador. Quando há uma incompatibilidade, as entradas são retornadas em um `state:store` identificador.

Os cookies primários não podem ser gravados (mesmo se o suporte estiver habilitado) nos seguintes casos:

* A solicitação está chegando no terceiro `adobedc.demdex.net` domínio.
* A solicitação está chegando em um dispositivo próprio `CNAME` domínio, diferente do especificado pelo chamador em `meta.state.domain`.

## Segurança de cookies

Todos os cookies têm o [Sinalizador seguro](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) sempre que possível.

Todos os cookies seguros têm o [Atributo SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) definir como `None`, o que significa que os cookies são enviados em todos os contextos, de origem própria e entre origens.

* Para cookies próprios (`kndcrt_*`), o `Secure` O sinalizador é definido somente quando o contexto da solicitação é seguro (HTTPS) e quando o referenciador ([Cabeçalho HTTP de referência](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers/Referer)) também é HTTPS. Se o referenciador não for seguro (HTTP), a variável `Secure` é omitido para permitir que o SDK da Web os leia. Um cookie seguro não pode ser lido de um contexto não seguro.
* Para o cookie de terceiros (demdex), a variável `Secure` O sinalizador é sempre definido, já que todas as solicitações são HTTPS, portanto o contexto da solicitação é seguro e esse cookie nunca é lido do JavaScript.

A variável `Secure` o sinalizador não está presente no [representação de metadados de cookies](#state-as-metadata). Somente o `SameSite` atributo está incluído. Nesse caso, é responsabilidade do cliente definir corretamente a `Secure` sinalizar sempre que a variável `SameSite` o atributo está presente. Cookies com `SameSite=None` também deve especificar o `Secure` atributo, pois exigem um contexto seguro (HTTPS).
