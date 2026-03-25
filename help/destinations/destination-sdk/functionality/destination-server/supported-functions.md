---
description: O Experience Platform Destination SDK usa modelos Pebble, permitindo transformar os dados exportados do Experience Platform no formato exigido pelo destino.
title: Funções de transformação compatíveis com o Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 2%

---

# Funções de transformação compatíveis com o Destination SDK

O Experience Platform Destination SDK usa [[!DNL Pebble] modelos](https://pebbletemplates.io/), permitindo transformar os dados exportados do Experience Platform no formato exigido pelo seu destino.

A implementação do Experience Platform [!DNL Pebble] tem algumas alterações, em comparação à versão predefinida fornecida por [!DNL Pebble]. Além disso, além das funções prontas para uso fornecidas pelo [!DNL Pebble], a Adobe criou algumas funções adicionais que você pode usar com o Destination SDK.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Onde usar {#where-to-use}

Use as funções com suporte listadas mais abaixo nesta página ao [criar um modelo de transformação de mensagem](../../testing-api/streaming-destinations/create-template.md) para os dados exportados do Experience Platform para o seu destino.

O modelo de transformação de mensagem é usado na [configuração do servidor de destino](templating-specs.md) para destinos de streaming.

## Pré-requisitos {#prerequisites}

Para entender os conceitos e funções nesta página de referência, leia primeiro o documento [formato da mensagem](message-format.md). Você precisa entender a [estrutura de um perfil](message-format.md#profile-structure) no Experience Platform antes de poder usar [!DNL Pebble] modelos para transformar os dados exportados.

Antes de avançar para as funções documentadas abaixo, revise os exemplos de modelos na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de público-alvo](message-format.md#using-templating). Os exemplos aqui começam de forma muito simples e aumentam em complexidade.

## [!DNL Pebble] funções com suporte {#supported-functions}

Na seção de tags [!DNL Pebble], o Destination SDK oferece suporte apenas a:

* [filtro](https://pebbletemplates.io/wiki/tag/filter/)
* [para](https://pebbletemplates.io/wiki/tag/for/)
* [se](https://pebbletemplates.io/wiki/tag/if/)
* [conjunto](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>O uso de `for` é diferente ao iterar através de elementos *matriz* ou *mapa* em um modelo. Ao iterar por meio de uma matriz, você pode obter o elemento diretamente. Ao percorrer um mapa, você obtém cada entrada de mapa, que tem um par de valores chave.
>
> * Para obter um exemplo de um elemento de matriz, pense nas identidades em um namespace [identityMap](message-format.md#identities), em que você poderia iterar por meio de elementos como `identityMap.gaid`, `identityMap.email` ou semelhante.
> * Para obter um exemplo de um elemento de mapa, pense em [segmentMembership](message-format.md#audience-membership).

Na seção de filtro [!DNL Pebble], o Destination SDK dá suporte a todas as funções. Um exemplo mais abaixo mostra como a função `date` pode ser usada dentro do Destination SDK.

Na seção de funções [!DNL Pebble], a Adobe *não* oferece suporte à função [range](https://pebbletemplates.io/wiki/function/range/).

## Exemplo de como a função `date` é usada {#date-function}

Para exemplificar como as funções [!DNL Pebble] são usadas no Destination SDK, veja abaixo como a função de data ([link na documentação do Pebble](https://pebbletemplates.io/wiki/filter/date/)) transforma o formato de um carimbo de data/hora.

### Caso de uso {#date-use-case}

Você deseja alterar o carimbo de data/hora `lastQualificationTime` do valor padrão [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) exportado pelo Experience Platform para outro valor preferido pelo seu destino.

### Exemplo {#date-example}

#### Entrada {#date-input}

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Formato {#date-format}

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Output {#date-output}

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funções adicionadas pelo Adobe {#functions-added-by-adobe}

Além das funções prontas para uso fornecidas pelo [!DNL Pebble], veja abaixo as funções adicionais criadas pelo Adobe que você pode usar em suas exportações de dados.

### `addedSegments` e `removedSegments` funções {#addedsegments-removedsegments-functions}

#### Caso de uso {#segments-use-case}

Essas funções podem ser usadas para obter uma lista de públicos-alvo que foram adicionados ou removidos de um perfil.

#### Exemplo {#segments-example}

##### Entrada {#segments-input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Formato {#segments-format}

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Output {#segments-output}

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Próximas etapas {#next-steps}

Agora você sabe quais [!DNL Pebble] funções têm suporte no Destination SDK e como usá-las para ajustar o formato dos dados exportados de acordo com suas necessidades. Em seguida, você deve revisar as seguintes páginas:

* [Criar e testar um modelo de transformação de mensagem](../../testing-api/streaming-destinations/create-template.md)
* [Renderizar operações de API de modelo](../../testing-api/streaming-destinations/render-template-api.md)
