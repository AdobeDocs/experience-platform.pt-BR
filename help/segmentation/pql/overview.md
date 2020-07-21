---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral do Linguagem do Query do Perfil (PQL)
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 2%

---


# [!DNL Profile Query Language] (PQL) visão geral

[!DNL Profile Query Language] (PQL) é uma linguagem de query compatível com [!DNL Experience Data Model] (XDM), projetada para suportar a definição e execução de query de segmentação para [!DNL Real-time Customer Profile] dados.

Este guia fornece uma visão geral do PQL, abrangendo diretrizes de formatação e fornecendo expressões de exemplo do PQL.

## Formatação de query PQL

Os query PQL têm a seguinte assinatura:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

O parâmetro de entrada pode ser um primitivo simples, como um booleano ou uma string, ou um tipo mais complexo, como um objeto, uma matriz ou um mapa.

Existem **três** maneiras diferentes de se referir aos parâmetros de entrada no corpo de uma expressão PQL:

### Referência implícita ao primeiro parâmetro

No exemplo abaixo, como o primeiro parâmetro está sempre no contexto, uma referência de propriedade (`homeAddress`) pode ser feita diretamente a ela.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Referência explícita ao primeiro parâmetro

No exemplo abaixo, `$1` se refere ao primeiro parâmetro. Como resultado, `$2` faria referência ao segundo parâmetro etc.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Uso de variáveis nomeadas, usando a notação lambda

No exemplo abaixo, `Profile` há um nome de variável, que pode ser escolhido pelo autor do query.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## Literais PQL

O PQL oferece suporte para os seguintes tipos literais:

| Literal | Definição | Exemplo |
| ------- | ---------- | ------- |
| String | Um tipo de dados composto por caracteres entre aspas de duplo. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Booleano | Um tipo de dados verdadeiro ou falso. | `true`, `false` |
| Número inteiro | Um tipo de dados que representa um número inteiro. Pode ser positivo, negativo ou zero. | `-201`, `0`, `412` |
| Duplo | Um tipo de dados que representa qualquer número real. Pode ser positivo, negativo ou zero. | `-51.24`, `3.14`, `0.6942058` |
| Data | Um tipo de dados que pode ser usado para criar datas com base em ano, mês e dia como parâmetros inteiros. Está formatado como `date(year, month, day)` | `date(2020, 3, 14)` |
| Matriz | Um tipo de dados que é composto como um grupo de outros valores literais. Ele usa colchetes para agrupar e vírgulas para delimitar entre valores diferentes. <br> **Observação:** Não é possível acessar diretamente as propriedades de itens em uma matriz. Portanto, se você precisar acessar uma propriedade em um storage, o método suportado será `select X from array where X.item = ...`. <br> O PQL reserva a palavra `xEvent` para fazer referência a uma matriz de eventos de experiência vinculados a um perfil. | `[1, 4, 7]`, `["US", "CA"]` |
| Referências de tempo relativas | Palavras reservadas que podem ser usadas para formar referências de carimbo de data e hora. <ul><li>agora, hoje, ontem, amanhã</li><li>this, last, next</li><li>before, after, from</li><li>milissegundo(s), segundo(s), minuto(s), hora(s), dia(s), semana(s), mês(es), ano(s), década(s), século/séculos, milênio/milênio</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## Funções PQL

A tabela a seguir descreve as diferentes categorias das funções PQL suportadas, incluindo links para documentação adicional para obter mais informações.

| Categoria | Definição |
| -------- | ---------- |
| Booleano | Usada para implementar álgebra booleana no PQL. Mais informações sobre essas funções podem ser encontradas no documento [de funções](./boolean-functions.md)booleanas. |
| Comparação | Usado para comparar entre elementos PQL diferentes. Mais informações sobre essas funções podem ser encontradas no documento [de funções de](./comparison-functions.md)comparação. |
| Matriz, lista e definido | Usado para interagir com arrays, listas e conjuntos. Mais informações sobre essas funções podem ser encontradas no documento [de funções](./array-functions.md)array, lista e set. |
| Mapa | Costumava interagir com mapas. Mais informações sobre essas funções podem ser encontradas no documento [de funções do](./map-functions.md)mapa. |
| String | Costumava interagir com cordas. Mais informações sobre essas funções podem ser encontradas no documento [de funções de](./string-functions.md)string. |
| Aritmética | Usado para executar aritmética básica em elementos PQL. Mais informações sobre essas funções podem ser encontradas no documento de funções [aritméticas](./arithmetic-functions.md) |
| Agregação | Usado para combinar os resultados de uma matriz em um resultado singular. Mais informações sobre as funções de agregação podem ser encontradas no documento [das funções de](./aggregation-functions.md)agregação. |
| Data e hora | Usado em conjunto com objetos date, time e datetime. Mais informações sobre essas funções podem ser encontradas no documento [de funções de](./datetime-functions.md)data/hora. |
| Filtro | Usado para filtrar dados em arrays. Mais informações sobre essas funções podem ser encontradas no documento [de funções de](./filter-functions.md)filtro. |
| Quantificadores lógicos | Usado para afirmar as condições em um storage. Mais informações podem ser encontradas no documento [de quantificadores](./logical-quantifiers.md)lógicos. |
| Diversos | As funções que não se encaixam em nenhuma das categorias acima podem ser encontradas no documento [de funções](./misc-functions.md)diversas. |

## Próximas etapas

Agora que você aprendeu a usar [!DNL Profile Query Language], é possível usar o PQL ao criar e modificar segmentos. Para obter mais informações sobre segmentação, leia a visão geral [da](../home.md)segmentação.