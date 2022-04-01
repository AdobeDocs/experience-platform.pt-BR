---
title: Gerenciamento do estado do cliente
description: Saiba como a Rede de borda da Adobe Experience Platform gerencia o estado do cliente
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: cliente; estado; gerenciamento; borda; rede; gateway; api
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# Gerenciamento do estado do cliente

A Rede de Borda em si é sem estado (não mantém sua própria sessão). No entanto, há determinados casos de uso que exigem persistência de estado do lado do cliente, como:

* Identificação consistente do dispositivo (consulte [identificação do visitante](visitor-identification.md))
* Coletar e aplicar o consentimento do usuário
* Manter a ID da sessão de personalização

A Edge Network usa um protocolo de gerenciamento de estado, delegando o aspecto de armazenamento ao seu cliente/SDK, e inclui entradas de estado em suas respostas. Para navegadores, as entradas são armazenadas como cookies.

A responsabilidade do cliente é armazenar e incluí-los em todas as solicitações subsequentes. O cliente também deve cuidar da expiração correta para as entradas, conforme instruído pelo gateway. Quando as entradas eram armazenadas como cookies, o navegador faz tudo isso automaticamente.

Embora as entradas de estado sempre tenham um valor simples `String` (visível para o chamador/SDK), você não deve consumir ou alterar os valores de nenhuma maneira. A estrutura/formato do valor ou mesmo o próprio nome podem mudar em qualquer ponto, o que pode levar a um comportamento inesperado para clientes que usam o estado internamente. O estado deve ser sempre consumido pelo próprio gateway ou por outros serviços de borda.

## Estado persistente do cliente como metadados

O estado retornado pelo [!DNL Edge Network] no corpo da resposta é uma `Handle` objeto com o tipo `state:store`.

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
| `maxAge` | Número inteiro | *Opcional* A entrada do TTL (time-to-live), em segundos. Quando estiver ausente, as entradas devem ser armazenadas apenas para a sessão atual. |
| `attrs` | `Map<String, String>` | *Opcional*. Uma lista opcional de atributos de entrada. Para todas as conexões seguras com um cabeçalho HTTP referenciador seguro, a variável `SameSite` está definido como `None`. |


Para suportar marcação múltipla (ou seja, várias instâncias do SDK na mesma propriedade, que potencialmente fazem referência a organizações diferentes), todas as entradas de estado recebem o prefixo automaticamente `kndctr_` e a ID da organização segura para URL.

Quando o SDK do cliente recebe uma `state:store` manipulada na resposta, ela deve fazer o seguinte:

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

## Estado persistente do cliente em cookies do navegador

Ao trabalhar com clientes do navegador, a Edge Network pode manter as entradas automaticamente como cookies do navegador. Isso permite um suporte transparente de armazenamento de estado, já que os navegadores respeitam o protocolo de gerenciamento de estado por padrão.

Quase todas as entradas são materializadas como cookies primários quando ativadas e suportadas (consulte a nota abaixo), mas o gateway também pode armazenar alguns cookies de terceiros quando o cookie de terceiros `adobedc.demdex.net` é usado.

Como as entradas são sempre vinculadas a um escopo específico (dispositivo/aplicativo) por sua definição, somente o subconjunto compatível com o contexto de solicitação atual será gravado pela Rede de borda. Entradas não escritas são retornadas dentro de um `state:store` manípulo.

Como regra geral, as entradas com escopo de aplicativo são sempre gravadas como cookies primários, enquanto as entradas com escopo de dispositivo são gravadas como cookies de terceiros. A decisão é totalmente transparente para o chamador, o gateway decide quais entradas podem ser gravadas, dependendo do contexto da chamada.

O chamador deve ativar explicitamente o suporte para armazenar o estado do cliente como cookies, por meio do `meta.state.cookiesEnabled` sinalizador:

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
| `cookiesEnabled` | Booleano | Quando definido, ativa o suporte a cookies. O valor padrão é `false`. |
| `domain` | String | Obrigatório quando `cookiesEnabled: true`. O domínio de nível superior no qual os cookies devem ser gravados. A Edge Network usará esse valor para decidir se o estado pode ser mantido como cookies. |

Mesmo se o suporte a cookies estiver ativado por meio do `cookiesEnabled` sinalizador, a Rede de borda do Adobe Experience Platform só gravará as entradas de estado se o domínio de nível superior da solicitação corresponder ao `domain` especificado pelo chamador. Quando há uma incompatibilidade, as entradas são retornadas em um `state:store` manípulo.

Os cookies próprios não podem ser gravados (mesmo se o suporte estiver ativado) nos seguintes casos:

* A solicitação está chegando em `adobedc.demdex.net` domínio.
* A solicitação está chegando em um `CNAME` , diferente do especificado pelo chamador em `meta.state.domain`.

## Segurança de cookie

Todos os cookies têm a variável [Sinalizador seguro](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) habilitado sempre que possível.

Todos os cookies seguros têm a variável [Atributo SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) defina como `None`, o que significa que os cookies são enviados em todos os contextos, seja de origem própria ou cruzada.

* Para cookies próprios (`kndcrt_*`), `Secure` O sinalizador é definido somente quando o contexto da solicitação é seguro (HTTPS) e quando o referenciador ([Cabeçalho HTTP do referenciador](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) também é HTTPS. Se o referenciador não for seguro (HTTP), a variável `Secure` O sinalizador é omitido para permitir que o SDK da Web os leia. Um cookie seguro não pode ser lido de um contexto inseguro.
* Para o cookie de terceiros (demdex), a variável `Secure` O sinalizador é sempre definido, já que todas as solicitações são HTTPS, portanto, o contexto da solicitação é seguro e esse cookie nunca é lido do JavaScript.

O `Secure` O sinalizador não está presente no [representação de metadados de cookies](#state-as-metadata). Somente a variável `SameSite` está incluído. Nesse caso, é responsabilidade do cliente definir corretamente a variável `Secure` sinalizador sempre que a variável `SameSite` está presente. Cookies com `SameSite=None` deve especificar também `Secure` , já que exigem um contexto seguro (HTTPS).
