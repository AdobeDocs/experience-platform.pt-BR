---
title: Gerenciamento de estado do cliente
description: Saiba como o Adobe Experience Platform Edge Network gerencia o estado do cliente
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: cliente;estado;gerenciamento;borda;rede;gateway;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# Gerenciamento de estado do cliente

O Edge Network em si não tem estado (ele não mantém sua própria sessão). No entanto, há determinados casos de uso que exigem persistência de estado do lado do cliente, como:

* Identificação de dispositivo consistente
* Coletar e aplicar o consentimento do usuário
* Manter a ID da sessão de personalização

A Edge Network usa um protocolo de gerenciamento de estado, delegando o aspecto de armazenamento ao seu cliente/SDK e inclui entradas de estado em suas respostas. Para navegadores, as entradas são armazenadas como cookies.

A responsabilidade do cliente é armazená-los e incluí-los em todas as solicitações subsequentes. O cliente também deve cuidar da expiração adequada das entradas, conforme instruído pelo gateway. Quando as entradas foram armazenadas como cookies, o navegador faz tudo isso automaticamente.

Embora as entradas de estado sempre tenham um valor `String` simples (visível para o chamador/SDK), você não deve consumir ou alterar os valores de forma alguma. A estrutura/formato do valor ou até mesmo o próprio nome podem mudar a qualquer momento, o que pode levar a um comportamento inesperado dos clientes que usam o estado internamente. O estado deve ser sempre consumido pelo próprio gateway ou outros serviços de borda.

## Persistência do estado do cliente como metadados

O estado retornado por [!DNL Edge Network] no corpo da resposta é um objeto `Handle` com o tipo `state:store`.

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
| `attrs` | `Map<String, String>` | *Opcional*. Uma lista opcional de atributos de entrada. Para todas as conexões seguras com um cabeçalho HTTP de referenciador seguro, o atributo `SameSite` está definido como `None`. |


Para oferecer suporte à multimarcação (ou seja, várias instâncias do SDK na mesma propriedade, que possivelmente fazem referência a organizações diferentes), todas as entradas de estado recebem automaticamente o prefixo `kndctr_` e a ID da organização segura para URL.

Quando o SDK cliente recebe um identificador `state:store` na resposta, ele deve fazer o seguinte:

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

Ao trabalhar com clientes do navegador, o Edge Network pode manter as entradas automaticamente como cookies do navegador. Isso permite o suporte ao armazenamento de estado transparente, já que os navegadores respeitam o protocolo de gerenciamento de estado por padrão.

Quase todas as entradas são materializadas como cookies próprios quando habilitadas e com suporte (consulte a observação abaixo), mas o gateway também pode armazenar alguns cookies de terceiros quando o domínio `adobedc.demdex.net` de terceiros é usado.

Como as entradas estão sempre vinculadas a um escopo específico (dispositivo/aplicativo) por sua definição, somente o subconjunto compatível com o contexto de solicitação atual será gravado pelo Edge Network. As entradas não gravadas são
retornado em um identificador `state:store`.

Como regra geral, as entradas com escopo de aplicativo são sempre gravadas como cookies primários, enquanto as entradas com escopo de dispositivo são gravadas como cookies de terceiros. A decisão é completamente transparente para o chamador, o gateway decide quais entradas podem ser gravadas, dependendo do contexto da chamada.

O chamador deve habilitar explicitamente o suporte para armazenar o estado do cliente como cookies, por meio do sinalizador `meta.state.cookiesEnabled`:

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
| `domain` | String | Necessário quando `cookiesEnabled: true`. O domínio de nível superior no qual os cookies devem ser gravados. O Edge Network usará esse valor para decidir se o estado pode ser mantido como cookies. |

Mesmo que o suporte a cookies seja habilitado por meio do sinalizador `cookiesEnabled`, o Adobe Experience Platform Edge Network somente gravará as entradas de estado se o domínio de nível superior da solicitação corresponder ao `domain` especificado pelo chamador. Quando há uma incompatibilidade, as entradas são retornadas em um identificador `state:store`.

Os cookies primários não podem ser gravados (mesmo se o suporte estiver habilitado) nos seguintes casos:

* A solicitação está vindo do domínio `adobedc.demdex.net` de terceiros.
* A solicitação está vindo em um domínio `CNAME` próprio, diferente daquele especificado pelo chamador em `meta.state.domain`.

## Segurança de cookies

Todos os cookies têm o [sinalizador seguro](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) habilitado sempre que possível.

Todos os cookies seguros têm o [atributo SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) definido como `None`, o que significa que os cookies são enviados em todos os contextos, de origem própria ou cruzada.

* Para os cookies próprios (`kndcrt_*`), o sinalizador `Secure` só é definido quando o contexto da solicitação é seguro (HTTPS) e quando o referenciador ([Cabeçalho HTTP do Referenciador](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers/Referer)) também é HTTPS. Se o referenciador não for seguro (HTTP), o sinalizador `Secure` será omitido para permitir que o Web SDK os leia. Um cookie seguro não pode ser lido de um contexto não seguro.
* Para o cookie de terceiros (demdex), o sinalizador `Secure` é sempre definido, já que todas as solicitações são HTTPS, portanto o contexto da solicitação é seguro e esse cookie nunca é lido do JavaScript.

O sinalizador `Secure` não está presente na representação de metadados dos cookies. Somente o atributo `SameSite` está incluído. Nesse caso, é responsabilidade do cliente definir corretamente o sinalizador `Secure` sempre que o atributo `SameSite` estiver presente. Os cookies com `SameSite=None` também devem especificar o atributo `Secure`, pois exigem um contexto seguro (HTTPS).
