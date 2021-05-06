---
keywords: Experience Platform; home; mapeador; conjunto de mapeamento; mapeamento;
solution: Experience Platform
title: Visão geral dos conjuntos de mapeamento
topic: visão geral
description: Saiba como usar conjuntos de mapeamento com a Preparação de dados do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4c06f621eb6fba8daa6501d56255cddbbcfdbda2
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# Visão geral dos conjuntos de mapeamento

Um conjunto de mapeamentos é um conjunto de mapeamentos que transforma dados de um esquema para outro. Este documento fornece informações sobre como os conjuntos de mapeamento são compostos, incluindo schema de entrada, schema de saída e mapeamentos.

## Introdução

Essa visão geral requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Preparação](./home.md) de dados: A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).
- [Fluxos de dados](../dataflows/home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile] e para [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Os métodos pelos quais os dados podem ser enviados para o  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.

## Sintaxe do conjunto de mapeamento

Um conjunto de mapeamentos é composto de uma ID, nome, schema de entrada, schema de saída e uma lista de mapeamentos associados.

O JSON a seguir é um exemplo de um conjunto de mapeamento típico:

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name" : "Id",
            "description" : "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | Um identificador exclusivo para o conjunto de mapeamento. |
| `name` | O nome do conjunto de mapeamentos. |
| `inputSchema` | O esquema XDM para os dados recebidos. |
| `outputSchema` | O esquema XDM ao qual os dados de entrada serão transformados em conformidade. |
| `mappings` | Uma matriz de mapeamentos de campo para campo do schema de origem para o schema de destino. |
| `sourceType` | Para cada mapeamento listado, seu atributo `sourceType` indica o tipo de fonte que deve ser mapeada. Pode ser um de `ATTRIBUTE`, `STATIC` ou `EXPRESSION`: <ul><li> `ATTRIBUTE` é usada para qualquer valor encontrado no caminho de origem. </li><li>`STATIC` é usada para valores inseridos no caminho de destino. Esse valor permanece constante e não é afetado pelo schema de origem.</li><li> `EXPRESSION` é usada para uma expressão, que será resolvida durante o tempo de execução. Uma lista de expressões disponíveis pode ser encontrada no [guia de funções de mapeamento](./functions.md).</li> </ul> |
| `source` | Para cada mapeamento listado, o atributo `source` indica o campo que você deseja mapear. Mais informações sobre como configurar sua fonte podem ser encontradas na seção [sources](#sources). |
| `destination` | Para cada mapeamento listado, o atributo `destination` indica o campo ou o caminho para o campo, onde o valor extraído do campo `source` será colocado. Mais informações sobre como configurar seus destinos podem ser encontradas na seção [destination](#destination). |
| `mappings.name` | (*Opcional*) Um nome para o mapeamento. |
| `mappings.description` | (*Opcional*) Uma descrição do mapeamento. |

## Configuração de fontes de mapeamento

Em um mapeamento, `source` pode ser um campo, uma expressão ou um valor estático. Com base no tipo de origem fornecido, o valor pode ser extraído de várias maneiras.

### Campo em dados em coluna

Ao mapear um campo em dados em colunas, como um arquivo CSV, use o tipo de origem `ATTRIBUTE`. Se o campo contiver `.` dentro de seu nome, use `\` para escapar do valor. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo CSV de exemplo:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Exemplo de mapeamento**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo de dados aninhados

Ao mapear um campo em dados aninhados, como um arquivo JSON, use o tipo de origem `ATTRIBUTE` . Se o campo contiver `.` dentro de seu nome, use `\` para escapar do valor. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de exemplo**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo dentro de uma matriz

Ao mapear um campo em uma matriz, é possível recuperar um valor específico usando um índice. Para fazer isso, use o tipo de origem `ATTRIBUTE` e o índice do valor que deseja mapear. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de exemplo**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Matriz para matriz ou objeto para objeto

Usando o tipo de origem `ATTRIBUTE`, também é possível mapear diretamente uma matriz para uma matriz ou um objeto para um objeto. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de exemplo**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Operações iterativas em arrays

Usando o tipo de origem `ATTRIBUTE`, é possível executar loop repetidamente por matrizes e mapeá-las para um esquema de destino usando um índice curinga (`[*]`). Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de exemplo**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Valor constante

Se desejar mapear uma constante ou um valor estático, use o tipo de origem `STATIC` .  Ao usar o tipo de origem `STATIC`, o `source` representa o valor codificado que você deseja atribuir ao `destination`. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de exemplo**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Exemplo de mapeamento**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Dados transformados**

```json
{
    "userType:": "CUSTOMER"
}
```

### Expressões

Se quiser mapear uma expressão, use o tipo de origem `EXPRESSION` . Uma lista de funções aceitas pode ser encontrada no [guia de funções de mapeamento](./functions.md). Ao usar o tipo de origem `EXPRESSION`, `source` representa a função que deseja resolver. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de exemplo**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Exemplo de mapeamento**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Dados transformados**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Configuração de destinos de mapeamento

Em um mapeamento, `destination` é o local onde o valor extraído de `source` será inserido.

### Campo no nível da raiz

Quando quiser mapear o valor `source` para o nível raiz dos dados transformados, siga o exemplo abaixo:

**Arquivo JSON de exemplo**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "name": "John Smith"
}
```

### Campo aninhado

Quando desejar mapear o valor `source` para um campo aninhado em seus dados transformados, siga o exemplo abaixo:

**Arquivo JSON de exemplo**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Exemplo de mapeamento**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo em um índice de matriz específico

Quando quiser mapear o valor `source` para um índice específico em uma matriz nos dados transformados, siga o exemplo abaixo:

**Arquivo JSON de exemplo**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "piList": ["John Smith"]
}
```

### Operação de matriz iterativa

Quando quiser realizar loop iterativamente por matrizes e mapear os valores para o destino, use um índice curinga (`[*]`). Um exemplo disso pode ser visto abaixo:

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Exemplo de mapeamento**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Dados transformados**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Próximas etapas

Ao ler este documento, agora você deve entender como os conjuntos de mapeamento são construídos, incluindo como configurar mapeamentos individuais em um conjunto de mapeamento. Para obter mais informações sobre outros recursos da Preparação de dados, leia a [Visão geral da Preparação de dados](./home.md). Para saber como usar conjuntos de mapeamento na API de Preparação de dados, leia o [Guia do desenvolvedor de Preparação de dados](./api/overview.md).