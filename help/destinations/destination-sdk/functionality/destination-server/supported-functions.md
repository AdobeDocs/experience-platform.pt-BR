---
description: O Experience Platform Destination SDK usa modelos Pebble, permitindo transformar os dados exportados do Experience Platform no formato exigido pelo destino.
title: Funções de transformação compatíveis com o Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 3%

---

# Funções de transformação compatíveis com o Destination SDK

Experience Platform Destination SDK usa [[!DNL Pebble] modelos](https://pebbletemplates.io/), permitindo transformar os dados exportados do Experience Platform no formato exigido pelo destino.

O EXPERIENCE PLATFORM [!DNL Pebble] A implementação do tem algumas alterações, em comparação com a versão pronta para uso fornecida pelo [!DNL Pebble]. Além disso, além das funções prontas para uso fornecidas pelo [!DNL Pebble], o Adobe criou algumas funções adicionais que podem ser usadas com o Destination SDK.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Onde usar {#where-to-use}

Use as funções suportadas listadas mais abaixo nesta página quando [criação de um template de transformação de mensagem](../../testing-api/streaming-destinations/create-template.md) para os dados exportados do Experience Platform para o seu destino.

O template de transformação de mensagem é usado no campo [configuração do servidor de destino](templating-specs.md) para destinos de transmissão.

## Pré-requisitos {#prerequisites}

Para entender os conceitos e as funções nesta página de referência, leia a [formato da mensagem](message-format.md) documento primeiro. Você precisa entender o [estrutura de um perfil](message-format.md#profile-structure) no Experience Platform antes de poder usar [!DNL Pebble] modelos para transformar e exportar os dados.

Antes de avançar para as funções documentadas abaixo, revise os exemplos de modelo na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de público](message-format.md#using-templating). Os exemplos aqui começam de forma muito simples e aumentam em complexidade.

## Compatível [!DNL Pebble] funções {#supported-functions}

No [!DNL Pebble] seção de tags, o Destination SDK suporta apenas:

* [filtro](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [se](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Usar `for` é diferente ao iterar através *matriz* ou *mapa* elementos em um modelo. Ao iterar por meio de uma matriz, você pode obter o elemento diretamente. Ao percorrer um mapa, você obtém cada entrada de mapa, que tem um par de valores chave.
>
> * Para obter um exemplo de um elemento de matriz, pense nas identidades em um [identityMap](message-format.md#identities) namespace, em que você pode iterar por meio de elementos como `identityMap.gaid`, `identityMap.email`, ou similar.
> * Para obter um exemplo de um elemento de mapa, pense em [segmentMembership](message-format.md#segment-membership).

No [!DNL Pebble] seção de filtro, o Destination SDK suporta todas as funções. Um exemplo mais abaixo mostra como a `date` função pode ser usada dentro do Destination SDK.

No [!DNL Pebble] funções, o Adobe faz *não* apoiar a [intervalo](https://pebbletemplates.io/wiki/function/range/) função.

## Exemplo de como a variável `date` é usada {#date-function}

Para exemplificar como [!DNL Pebble] são usadas no Destination SDK, veja abaixo como a função de data ([link na documentação do Pebble](https://pebbletemplates.io/wiki/filter/date/)) é usado para transformar o formato de um carimbo de data e hora.

### Caso de uso

Você deseja alterar o `lastQualificationTime` carimbo de data e hora do padrão [ISO 8601](https://pt.wikipedia.org/wiki/ISO_8601) que o Experience Platform exporta para outro valor preferido pelo seu destino.

### Exemplo

#### Entrada

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Formato

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Saída

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Funções adicionadas pelo Adobe {#functions-added-by-adobe}

Além das funções prontas para uso fornecidas pela [!DNL Pebble], veja abaixo as funções adicionais criadas pelo Adobe que podem ser usadas nas exportações de dados.

### `addedSegments` e `removedSegments` funções {#addedsegments-removedsegments-functions}

#### Caso de uso

Essas funções podem ser usadas para obter uma lista de públicos-alvo que foram adicionados ou removidos de um perfil.

#### Exemplo

##### Entrada

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

##### Formato

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Saída

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

Agora você sabe qual [!DNL Pebble] As funções são compatíveis com o Destination SDK, bem como sobre como usá-las para ajustar o formato dos dados exportados para atender às suas necessidades. Em seguida, você deve revisar as seguintes páginas:

* [Criar e testar um modelo de transformação de mensagem](../../testing-api/streaming-destinations/create-template.md)
* [Renderizar operações de API de modelo](../../testing-api/streaming-destinations/render-template-api.md)
