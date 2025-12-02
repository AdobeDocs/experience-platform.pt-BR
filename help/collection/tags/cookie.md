---
title: cookie
description: Grave, edite ou exclua manualmente os cookies da propriedade de tag.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

O objeto `_satellite.cookie` contém métodos que permitem gravar, editar ou excluir cookies aos quais as regras de marca podem fazer referência. É uma cópia parcial de [`js-cookie`](https://github.com/js-cookie/js-cookie), contendo muitos recursos principais dessa biblioteca.

## `cookie.set()`

O método `set()` grava um cookie ao qual a propriedade da tag pode fazer referência.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

Os seguintes parâmetros de método estão disponíveis:

| Nome | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| **`name`** | `string` | Sim | O nome do cookie. |
| **`value`** | `string` | Sim | O valor do cookie |
| **`attributes`** | `object` | Não | Atributos adicionais que você deseja que o cookie tenha. |

O objeto `attributes` dá suporte às seguintes propriedades:

| Nome do atributo | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|
| **`expires`** | `number` ou [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | Não | O cookie expira ao final da sessão do navegador | O número de dias de expiração do cookie. |
| **`path`** | `string` | Não | Cookie visível em todo o site | Onde no domínio o cookie está visível. |
| **`domain`** | `string` | Não | Cookie visível para o domínio em que foi criado | Um domínio válido (com ou sem um subdomínio) em que o cookie está visível. Se um domínio for incluído sem um subdomínio, o cookie será visível para todos os subdomínios sob esse domínio. |
| **`secure`** | `boolean` | Não | Nenhum atributo definido | Determina se o cookie requer um protocolo seguro (`https://`). Se omitido, não há requisito de protocolo seguro. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | Não | Nenhum atributo definido | Permite que você defina o atributo [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) de um cookie. Se você definir `sameSite` como `None`, também deverá definir `secure` como `true`. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

Chamar esse método grava o cookie desejado e retorna a string de cookie serializada que foi gravada. Essa string é usada principalmente para fins de depuração ou registro.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>As versões anteriores do objeto de marca usaram `_satellite.setCookie()`. O método `setCookie()` foi substituído em favor de `_satellite.cookie.set()`.

## `cookie.get()`

O método `get()` retorna um valor de cookie.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Nome | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| **`name`** | `string` | Sim | O nome do cookie do qual você deseja recuperar o valor (diferencia maiúsculas de minúsculas). |

Se o nome do cookie existir, retorna o valor do cookie. Se o nome do cookie não existe, retorna `undefined`.

>[!TIP]
>
>As versões anteriores do objeto de marca usaram `_satellite.getCookie()`. O método `getCookie()` foi substituído em favor de `_satellite.cookie.get()`.

## `cookie.remove()`

O método `remove()` exclui um cookie definido.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Nome | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| **`name`** | `string` | Sim | O nome do cookie que você deseja remover. |
| **`attributes`** | `object` | Não | Os atributos associados ao cookie que você deseja remover. Se você definir um cookie usando os atributos `path` ou `domain`, inclua esses mesmos atributos ao remover o cookie. A não inclusão desses atributos não remove o cookie. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>As versões anteriores do objeto de marca usaram `_satellite.removeCookie()`. O método `removeCookie()` foi substituído em favor de `_satellite.cookie.remove()`.
