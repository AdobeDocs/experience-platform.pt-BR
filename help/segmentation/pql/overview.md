---
keywords: Experience Platform;página inicial;tópicos populares;PQL;pql;profile query language
solution: Experience Platform
title: Visão geral do Idioma de consulta de perfil (PQL)
description: Este guia fornece uma visão geral do PQL, abordando diretrizes de formatação e fornecendo exemplos de expressões PQL.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 3%

---

# [!DNL Profile Query Language] Visão geral do (PQL)

[!DNL Profile Query Language] (PQL) é uma [!DNL Experience Data Model] Linguagem de consulta compatível com (XDM) projetada para oferecer suporte à definição e execução de consultas de segmentação para [!DNL Real-Time Customer Profile] dados.

Este guia fornece uma visão geral do PQL, abordando diretrizes de formatação e fornecendo exemplos de expressões PQL.

## Formatação de consulta PQL

As consultas PQL têm a seguinte assinatura:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

O parâmetro de entrada pode ser um primitivo simples, como um booleano ou uma string, ou um tipo mais complexo, como um objeto, matriz ou mapa.

Há três maneiras diferentes de fazer referência aos parâmetros de entrada no corpo de uma expressão PQL:

### Referência implícita ao primeiro parâmetro

No exemplo abaixo, como o primeiro parâmetro está sempre em contexto, uma referência de propriedade (`homeAddress`) pode ser feita diretamente para ele.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Referência explícita ao primeiro parâmetro

No exemplo abaixo, `$1` refere-se ao primeiro parâmetro. Como resultado, `$2` se refere ao segundo parâmetro etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Uso de variáveis nomeadas, usando a notação lambda

No exemplo abaixo, `Profile` é um nome de variável, que pode ser escolhido pelo autor da consulta.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Literais PQL

O PQL fornece suporte para os seguintes tipos literais:

| Literal | Definição | Exemplo |
| ------- | ---------- | ------- |
| String | Um tipo de dados composto de caracteres entre aspas duplas. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Um tipo de dados que é verdadeiro ou falso. | `true`, `false` |
| Número inteiro | Um tipo de dados que representa um número inteiro. Pode ser positivo, negativo ou zero. | `-201`, `0`, `412` |
| Duplo | Um tipo de dados que representa qualquer número real. Pode ser positivo, negativo ou zero. | `-51.24`, `3.14`, `0.6942058` |
| Data | Um tipo de dados que pode ser usado para criar datas com base no ano, mês e dia como parâmetros inteiros. É formatado como `date(year, month, day)` | `date(2020, 3, 14)` |
| Matriz | Um tipo de dados que é composto como um grupo de outros valores literais. Ela usa colchetes para agrupar e vírgulas para delimitar entre valores diferentes. <br> **Nota:** Não é possível acessar diretamente as propriedades dos itens em uma matriz. Portanto, se você precisar acessar uma propriedade em uma matriz, o método compatível é `select X from array where X.item = ...`. <br> A PQL reserva a palavra `xEvent` para consultar uma variedade de eventos de experiência vinculados a um perfil. | `[1, 4, 7]`, `["US", "CA"]` |
| Referências de tempo relativas | Palavras reservadas que podem ser usadas para formar referências de carimbo de data e hora e intervalo de tempo. <ul><li>hoje, ontem, amanhã</li><li>este, último, próximo</li><li>antes, depois, de</li><li>milissegundo(s), segundo(s), minuto(s), hora(s), dia(s), semana(s), mês(es), ano(s), década(s), século/séculos, milênio/milênio</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Funções PQL

A tabela a seguir descreve as diferentes categorias de funções PQL compatíveis, incluindo links para documentação adicional a fim de obter mais informações.

| Categoria | Definição |
| -------- | ---------- |
| Booleano | Usado para implementar álgebra booleana no PQL. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções booleanas](./boolean-functions.md). |
| Comparação | Usado para comparar entre diferentes elementos PQL. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções de comparação](./comparison-functions.md). |
| Matriz, lista e conjunto | Usado para interagir com matrizes, listas e conjuntos. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções de matriz, lista e definição](./array-functions.md). |
| Mapa | Usado para interagir com mapas. Mais informações sobre essas funções podem ser encontradas na seção [documento mapear funções](./map-functions.md). |
| String | Usado para interagir com strings. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções de sequência](./string-functions.md). |
| Objeto | Usado para interagir com objetos. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções de objeto](./object-functions.md). |
| Aritmética | Usado para executar aritmética básica em elementos PQL. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções aritméticas](./arithmetic-functions.md) |
| Agregação | Usado para combinar resultados de uma matriz em um resultado único. Mais informações sobre funções de agregação podem ser encontradas no [documento de funções de agregação](./aggregation-functions.md). |
| Data e hora | Usado em conjunto com objetos de data, hora e data e hora. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções de data/hora](./datetime-functions.md). |
| Filtro | Usado para filtrar dados em matrizes. Mais informações sobre essas funções podem ser encontradas na seção [documento de funções de filtro](./filter-functions.md). |
| Quantificadores lógicos | Usado para confirmar condições em uma matriz. Mais informações podem ser encontradas no [documento de quantificadores lógicos](./logical-quantifiers.md). |
| Diversos | As funções que não se encaixam em nenhuma das categorias acima podem ser encontradas na [documento de funções diversas](./misc-functions.md). |

## Próximas etapas

Agora que você aprendeu a usar [!DNL Profile Query Language], é possível usar o PQL ao criar e modificar segmentos. Para obter mais informações sobre segmentação, leia o [visão geral da segmentação](../home.md).
