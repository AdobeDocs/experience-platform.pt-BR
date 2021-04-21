---
keywords: Experience Platform, home, tópicos populares, PQL, pql, linguagem de consulta de perfil
solution: Experience Platform
title: Visão geral da linguagem de consulta do perfil (PQL)
topic-legacy: developer guide
description: Este guia fornece uma visão geral do PQL, abordando as diretrizes de formatação e fornecendo exemplos de expressões PQL.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 3%

---

# [!DNL Profile Query Language] Visão geral (PQL)

[!DNL Profile Query Language] O (PQL) é uma linguagem de consulta compatível com o  [!DNL Experience Data Model] (XDM), projetada para oferecer suporte à definição e execução de consultas de segmentação para  [!DNL Real-time Customer Profile] dados.

Este guia fornece uma visão geral do PQL, abordando as diretrizes de formatação e fornecendo exemplos de expressões PQL.

## Formatação de consulta PQL

As consultas PQL têm a seguinte assinatura:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

O parâmetro de entrada pode ser um primitivo simples, como um booleano ou uma string, ou um tipo mais complexo, como um objeto, matriz ou mapa.

Há três maneiras diferentes de fazer referência aos parâmetros de entrada no corpo de uma expressão PQL:

### Referência implícita ao primeiro parâmetro

No exemplo abaixo, como o primeiro parâmetro está sempre no contexto, uma referência de propriedade (`homeAddress`) pode ser feita diretamente a ela.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Referência explícita ao primeiro parâmetro

No exemplo abaixo, `$1` se refere ao primeiro parâmetro. Como resultado, `$2` se referiria ao segundo parâmetro etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Uso de variáveis nomeadas, usando a notação lambda

No exemplo abaixo, `Profile` é um nome de variável, que pode ser escolhido pelo autor da consulta.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Literais PQL

O PQL oferece suporte para os seguintes tipos literais:

| Literal | Definição | Exemplo |
| ------- | ---------- | ------- |
| String | Um tipo de dados composto por caracteres entre aspas duplas. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Um tipo de dados verdadeiro ou falso. | `true`, `false` |
| Número inteiro | Um tipo de dados que representa um número inteiro. Pode ser positivo, negativo ou zero. | `-201`,  `0`,  `412` |
| Duplo | Um tipo de dados que representa qualquer número real. Pode ser positivo, negativo ou zero. | `-51.24`,  `3.14`,  `0.6942058` |
| Data | Um tipo de dados que pode ser usado para criar datas com base em ano, mês e dia como parâmetros inteiros. É formatado como `date(year, month, day)` | `date(2020, 3, 14)` |
| Matriz | Um tipo de dados que é composto como um grupo de outros valores literais. Ele usa colchetes para agrupar e vírgulas para delimitar entre valores diferentes. <br> **Observação:** não é possível acessar diretamente as propriedades dos itens em uma matriz. Portanto, se você precisar acessar uma propriedade em uma matriz, o método suportado será `select X from array where X.item = ...`. <br> A PQL reserva a palavra  `xEvent` para se referir a uma matriz de eventos de experiência vinculados a um perfil. | `[1, 4, 7]`,  `["US", "CA"]` |
| Referências de tempo relativas | Palavras reservadas que podem ser usadas para formar referências de carimbo de data e hora e de intervalo. <ul><li>agora, hoje, ontem, amanhã</li><li>isto, último, próximo</li><li>antes, depois, de</li><li>milissegundos, segundo(s), minuto(s), hora(s), dia(s), semana(s), mês(es), ano(s), década(s), século/séculos, milênio/milênio</li></ul> | `X.timestamp occurs before today`,  `X.timestamp occurs last month`,  `X.timestamp occurs <= 3 days before now` |


## Funções PQL

A tabela a seguir descreve as diferentes categorias de funções PQL compatíveis, incluindo links para outras documentações, para obter mais informações.

| Categoria | Definição |
| -------- | ---------- |
| Booleano | Usada para implementar álgebra booleana no PQL. Mais informações sobre essas funções podem ser encontradas no [boolean functions document](./boolean-functions.md). |
| Comparação | Usado para comparar diferentes elementos de PQL. Mais informações sobre essas funções podem ser encontradas no [documento de funções de comparação](./comparison-functions.md). |
| Matriz, lista e conjunto | Usado para interagir com arrays, listas e conjuntos. Mais informações sobre essas funções podem ser encontradas no [array, list e set functions document](./array-functions.md). |
| Mapa | Usado para interagir com mapas. Mais informações sobre essas funções podem ser encontradas no [documento de funções de mapa](./map-functions.md). |
| String | Usado para interagir com strings. Mais informações sobre essas funções podem ser encontradas no [documento de funções de string](./string-functions.md). |
| Objeto | Usado para interagir com objetos. Mais informações sobre essas funções podem ser encontradas no [object functions document](./object-functions.md). |
| Aritmética | Usado para executar aritmética básica em elementos PQL. Mais informações sobre essas funções podem ser encontradas no [documento de funções aritméticas](./arithmetic-functions.md) |
| Agregação | Usado para combinar resultados de uma matriz em um resultado singular. Mais informações sobre funções de agregação podem ser encontradas no [documento de funções de agregação](./aggregation-functions.md). |
| Data e hora | Usada em conjunto com objetos date, time e datetime. Mais informações sobre essas funções podem ser encontradas no [date/time functions document](./datetime-functions.md). |
| Filtro | Usado para filtrar dados em arrays. Mais informações sobre essas funções podem ser encontradas no [filter functions document](./filter-functions.md). |
| quantificadores lógicos | Usado para asserção de condições em um storage. Mais informações podem ser encontradas no [documento dos quantificadores lógicos](./logical-quantifiers.md). |
| Diversos | As funções que não se encaixam em nenhuma das categorias acima podem ser encontradas no [documento de funções diversas](./misc-functions.md). |

## Próximas etapas

Agora que você aprendeu a usar [!DNL Profile Query Language], pode usar o PQL ao criar e modificar segmentos. Para obter mais informações sobre segmentação, leia a [visão geral da segmentação](../home.md).
