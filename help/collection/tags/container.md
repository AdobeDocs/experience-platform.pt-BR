---
title: _container
description: Visualizar todo o contêiner de tags em um único objeto.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

O objeto `_satellite._container` contém a configuração completa e o contexto de tempo de execução da propriedade de marca carregada na página. Todas as informações, como regras, elementos de dados, extensões e ambientes estão disponíveis nesse objeto. Seu uso principal é auxiliar na depuração da implementação para que você possa ver exatamente qual lógica é exposta ou publicada.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Este objeto é somente para fins de depuração. Não vincule a lógica de produção a esse objeto, não faça referência a esse objeto na implementação nem edite valores nesse objeto. A disponibilidade de propriedades ou nomes nesse objeto pode ser alterada pela Adobe a qualquer momento.

## Campos disponíveis

Os seguintes objetos estão disponíveis para referência:

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

O objeto `_satellite._container.buildInfo` contém uma cópia de [`_satellite.buildInfo`](buildinfo.md).

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

O objeto `_satellite._container.company` contém uma cópia de [`_satellite.company`](company.md).

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

O objeto `_satellite._container.dataElements` fornece uma referência de todos os elementos de dados na propriedade de marca.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Cada elemento de dados inclui as seguintes propriedades:

| Nome | Tipo | Descrição |
|---|---|---|
| **`modulePath`** | `string` | O caminho do arquivo JavaScript que determina a lógica desse tipo de elemento de dados. |
| **`settings`** | `Settings` | As configurações do elemento de dados. As propriedades nesse objeto dependem do tipo de elemento de dados. |

## `environment`

O objeto `_satellite._container.environment` contém uma cópia de [`_satellite.environment`](environment.md).

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

O objeto `_satellite._container.extensions` lista todas as extensões publicadas na propriedade de marca.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Cada extensão inclui as seguintes propriedades:

| Nome | Tipo | Descrição |
|---|---|---|
| **`displayName`** | `string` | O nome amigável da extensão. |
| **`hostedLibFilesUrl`** | `string` | O local na CDN onde a extensão reside. |
| **`modules`** | `Modules` | A lógica do JavaScript para todos os eventos, ações, condições e elementos de dados que a extensão usa. O conteúdo desse objeto é diferente para cada extensão. |

## `property`

O objeto `_satellite._container.property` fornece informações sobre a própria propriedade da marca.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Nome | Tipo | Descrição |
|---|---|---|
| **`id`** | `string` | O identificador exclusivo da propriedade da tag. |
| **`name`** | `string` | O nome amigável da propriedade de tag. |
| **`settings`** | `PropertySettings` | Configurações para esta propriedade. Consulte a tabela abaixo. |

| Nome da configuração | Tipo | Descrição |
|---|---|---|
| **`domains`** | `string[]` | Os domínios configurados para a propriedade, como definido ao [configurar uma propriedade de marca](/help/tags/ui/administration/companies-and-properties.md). |
| **`ruleComponentSequencingEnabled`** | `boolean` | Determina se a caixa de seleção **[!UICONTROL Run rule components in sequence]** está habilitada ao configurar a propriedade de marca. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Determina se a caixa de seleção **[!UICONTROL Return an empty string for undefined data elements]** está habilitada ao configurar a propriedade de marca. |

## `_container.rules`

A matriz de objetos `rules` fornece uma referência de todas as regras na propriedade de marca.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Cada regra contém os seguintes campos:

| Nome | Tipo | Descrição |
|---|---|---|
| **`id`** | `string` | O identificador exclusivo da regra. |
| **`name`** | `string` | O nome amigável da regra. |
| **`events`** | `Event[]` | Uma matriz de eventos configurada para acionar a regra. |
| **`conditions`** | `Condition[]` | Uma matriz de condições configuradas para acionar a regra. |
| **`actions`** | `Action[]` | Uma matriz de ações configuradas para serem executadas quando a regra for acionada. |
