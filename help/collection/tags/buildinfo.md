---
title: buildInfo
description: Obtenha informações sobre o build de tag implementado em seu site.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

O objeto `_satellite.buildInfo` contém informações sobre a compilação da propriedade de marca implementada. Esse objeto é mais útil ao depurar builds frequentes para garantir que você esteja usando a versão mais recente.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Campos disponíveis

Os seguintes campos estão disponíveis ao chamar este objeto.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Nome | Tipo | Descrição |
| --- | --- | --- |
| **`minified`** | `boolean` | Indica se a biblioteca é minificada. As compilações de produção geralmente são minificadas (`true`), enquanto as compilações de preparo e desenvolvimento normalmente não são (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | A data e a hora em que o arquivo do JavaScript foi criado e publicado. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbine](https://github.com/adobe/reactor-turbine) é o mecanismo da Adobe que processa regras de marcas e delega lógica a extensões de marcas. Esse campo contém a data e a hora do build do Turbine usado para publicar sua propriedade de tag. |
| **`turbineVersion`** | `string` | A versão do Turbine usada para criar e publicar sua propriedade de tag. |

Informações semelhantes também estão contidas em `_satellite._container.buildInfo`. Consulte [`_container`](container.md) para obter mais informações.
