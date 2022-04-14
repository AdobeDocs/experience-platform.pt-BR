---
description: O Experience Platform Destination SDK usa modelos Pebble, permitindo transformar os dados exportados do Experience Platform no formato exigido pelo seu destino.
title: Funções de transformação compatíveis no Destination SDK
source-git-commit: 840404741da06ba1593b227c7d6ba459b5f43110
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 3%

---

# Funções de transformação compatíveis no Destination SDK

## Visão geral {#overview}

Experience Platform Destination SDK use [[!DNL Pebble] modelos](https://pebbletemplates.io/), permitindo transformar os dados exportados do Experience Platform no formato exigido pelo destino.

O Experience Platform [!DNL Pebble] A implementação tem algumas alterações, em comparação com a versão predefinida fornecida pelo [!DNL Pebble]. Além disso, além das funções prontas para uso fornecidas pelo [!DNL Pebble], o Adobe criou algumas funções adicionais que podem ser usadas com o Destination SDK.

## Onde usar {#where-to-use}

Use as funções compatíveis listadas mais abaixo nesta página quando [criação de um template de transformação de mensagem](./create-template.md) para os dados exportados do Experience Platform para seu destino. O modelo de transformação de mensagem é usado na variável [configuração do servidor de destino](./server-and-template-configuration.md) para destinos de transmissão.

## Pré-requisitos {#prerequisites}

Para entender os conceitos e as funções nesta página de referência, leia o [formato de mensagem](/help/destinations/destination-sdk/message-format.md) documento primeiro. Você precisa entender o [estrutura de um perfil](/help/destinations/destination-sdk/message-format.md#profile-structure) no Experience Platform antes de usar [!DNL Pebble] modelos para transformar e os dados exportados.

Antes de avançar para as funções documentadas abaixo, analise os exemplos de modelos na seção [Uso de uma linguagem de modelo para as transformações de identidade, atributos e associação de segmento](/help/destinations/destination-sdk/message-format.md#using-templating). Os exemplos lá começam muito simples e aumentam a complexidade.

## Suportado [!DNL Pebble] funções {#supported-functions}

No [!DNL Pebble] seção de tags, o Destination SDK suporta apenas:
* [filtro](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [if](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Usando `for` é diferente ao iterar por *array* ou *mapa* elementos em um template. Ao iterar por meio de uma matriz, você pode obter o elemento diretamente. Ao iterar por um mapa, você obtém cada entrada de mapa, que tem um par de valor chave.
>
> * Para obter um exemplo de um elemento de matriz, pense nas identidades em um [identityMap](./message-format.md#identities) namespace, onde você pode iterar por meio de elementos como `identityMap.gaid`, `identityMap.email`ou semelhante.
> * Para obter um exemplo de um elemento de mapa, pense em [segmentMembership](./message-format.md#segment-membership).


No [!DNL Pebble] seção de filtro, o Destination SDK suporta todas as funções. Um exemplo a seguir mostra como a função `date` pode ser usada dentro do Destination SDK.

No [!DNL Pebble] seção funções, Adobe faz *not* apoiará [intervalo](https://pebbletemplates.io/wiki/function/range/) .

## Exemplo de como a função `date` é usada {#date-function}

Para exemplificar como [!DNL Pebble] são usadas no Destination SDK, veja abaixo como a função de data ([link na documentação do Pebble](https://pebbletemplates.io/wiki/filter/date/)) é usada para transformar o formato de um carimbo de data e hora.

### Caso de uso

Você deseja alterar a variável `lastQualificationTime` carimbo de data e hora do padrão [ISO 8601](https://pt.wikipedia.org/wiki/ISO_8601) que o Experience Platform exporta para outro valor preferido pelo seu destino.

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

## Funções adicionadas por Adobe {#functions-added-by-adobe}

Além das funções prontas para uso fornecidas pelo [!DNL Pebble], consulte abaixo as funções adicionais criadas pelo Adobe que você pode usar nas exportações de dados.

### `addedSegments` e `removedSegments` funções {#addedsegments-removedsegments-functions}

#### Caso de uso

Essas funções podem ser usadas para obter uma lista de segmentos que foram adicionados ou removidos de um perfil.

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

### Added and removed segments filters {#added-and-removed-segmnts-filters}

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

Agora você sabe qual [!DNL Pebble] As funções do são compatíveis com o Destination SDK, bem como como como usá-las para ajustar o formato dos dados exportados para atender às suas necessidades. Em seguida, você deve revisar as seguintes páginas:

* [Criar e testar um modelo de transformação de mensagem](/help/destinations/destination-sdk/create-template.md)
* [Renderizar operações da API do modelo](/help/destinations/destination-sdk/render-template-api.md)