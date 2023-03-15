---
keywords: Experience Platform;home;mapeador;conjunto de mapeamento;mapeamento;
solution: Experience Platform
title: Visão geral dos conjuntos de mapeamento
description: Saiba como usar conjuntos de mapeamento com o Preparo de dados do Adobe Experience Platform.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Visão geral dos conjuntos de mapeamento

Um conjunto de mapeamento é um conjunto de mapeamentos que transforma os dados de um esquema para outro. Este documento fornece informações sobre como os conjuntos de mapeamento são compostos, incluindo o esquema de entrada, o esquema de saída e os mapeamentos.

## Introdução

Esta visão geral requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Preparação de dados](./home.md): o Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).
- [Fluxos de dados](../dataflows/home.md): os fluxos de dados são uma representação de trabalhos de dados que movem os dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados dos conectores de origem para os conjuntos de dados de destino para [!DNL Identity] e [!DNL Profile], e para [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): os métodos pelos quais os dados podem ser enviados para o [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.

## Sintaxe do conjunto de mapeamento

Um conjunto de mapeamento é composto de uma ID, nome, esquema de entrada, esquema de saída e uma lista de mapeamentos associados.

O JSON a seguir é um exemplo de um conjunto de mapeamento típico:

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
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
            "name": "Id",
            "description": "Identifier field"
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
| `id` | Um identificador exclusivo do conjunto de mapeamento. |
| `name` | O nome do conjunto de mapeamento. |
| `inputSchema` | O esquema XDM para os dados de entrada. |
| `outputSchema` | O esquema XDM ao qual os dados de entrada foram transformados para se adequar. |
| `mappings` | Uma matriz de mapeamentos de campo para campo do esquema de origem para o esquema de destino. |
| `sourceType` | Para cada mapeamento listado, seu `sourceType` attribute indica o tipo de origem a ser mapeada. Pode ser um de `ATTRIBUTE`, `STATIC`ou `EXPRESSION`: <ul><li> `ATTRIBUTE` é usado para qualquer valor encontrado no caminho de origem. </li><li>`STATIC` é usado para valores inseridos no caminho de destino. Esse valor permanece constante e não é afetado pelo esquema de origem.</li><li> `EXPRESSION` é usado para uma expressão, que será resolvida durante o tempo de execução. Uma lista de expressões disponíveis pode ser encontrada no [guia de funções de mapeamento](./functions.md).</li> </ul> |
| `source` | Para cada mapeamento listado, a variável `source` attribute indica o campo que você deseja mapear. Mais informações sobre como configurar sua origem podem ser encontradas na [seção origens](#sources). |
| `destination` | Para cada mapeamento listado, a variável `destination` atributo indica o campo, ou o caminho para o campo, onde o valor extraído do campo `source` será colocado. Mais informações sobre como configurar os destinos podem ser encontradas na [seção de destino](#destination). |
| `mappings.name` | (*Opcional*) Um nome para o mapeamento. |
| `mappings.description` | (*Opcional*) Uma descrição do mapeamento. |

## Configuração de origens de mapeamento

Em um mapeamento, a variável `source` pode ser um campo, uma expressão ou um valor estático. Com base no tipo de origem fornecido, o valor pode ser extraído de várias maneiras.

### Campo em dados de colunas

Ao mapear um campo em dados de colunas, como um arquivo CSV, use o `ATTRIBUTE` tipo de origem. Se o campo contiver `.` em seu nome, use `\` para omitir o valor. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo CSV de exemplo:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Mapeamento de amostra**

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

### Campo em dados aninhados

Ao mapear um campo em dados aninhados, como um arquivo JSON, use o `ATTRIBUTE` tipo de origem. Se o campo contiver `.` em seu nome, use `\` para omitir o valor. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de amostra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mapeamento de amostra**

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

Ao mapear um campo em uma matriz, você pode recuperar um valor específico usando um índice. Para fazer isso, use o `ATTRIBUTE` tipo de origem e o índice do valor que você deseja mapear. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de amostra**

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

**Mapeamento de amostra**

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

Usar o `ATTRIBUTE` tipo de origem, você também pode mapear diretamente uma matriz para uma matriz ou um objeto para um objeto. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de amostra**

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

**Mapeamento de amostra**

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

Usar o `ATTRIBUTE` tipo de origem, é possível executar um loop iterativo pelas matrizes e mapeá-las para um esquema de destino usando um índice curinga (`[*]`). Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de amostra**

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

**Mapeamento de amostra**

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

Se quiser mapear um valor constante ou estático, use o `STATIC` tipo de origem.  Ao usar o `STATIC` tipo de origem, a variável `source` representa o valor embutido em código que você deseja atribuir à variável `destination`. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de amostra**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Mapeamento de amostra**

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

Se quiser mapear uma expressão, use o `EXPRESSION` tipo de origem. Uma lista de funções aceitas pode ser encontrada no [guia de funções de mapeamento](./functions.md). Ao usar o `EXPRESSION` tipo de origem, a variável `source` representa a função que você deseja resolver. Um exemplo desse mapeamento pode ser encontrado abaixo:

**Arquivo JSON de amostra**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Mapeamento de amostra**

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

Em um mapeamento, a variável `destination` é o local onde o valor extraído da variável `source` será inserido.

### Campo no nível raiz

Quando quiser mapear a variável `source` para o nível raiz dos seus dados transformados, siga o exemplo abaixo:

**Arquivo JSON de amostra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mapeamento de amostra**

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

Quando quiser mapear a variável `source` para um campo aninhado em seus dados transformados, siga o exemplo abaixo:

**Arquivo JSON de amostra**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Mapeamento de amostra**

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

Quando quiser mapear a variável `source` para um índice específico em uma matriz nos dados transformados, siga o exemplo abaixo:

**Arquivo JSON de amostra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mapeamento de amostra**

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

Quando quiser executar um loop iterativo pelas matrizes e mapear os valores para o destino, você poderá usar um índice curinga (`[*]`). Um exemplo disso pode ser visto abaixo:

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

**Mapeamento de amostra**

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

Após a leitura deste documento, você deve entender como os conjuntos de mapeamento são construídos, incluindo como configurar mapeamentos individuais em um conjunto de mapeamento. Para obter mais informações sobre outros recursos do Preparo de dados, leia a [Visão geral do Preparo de dados](./home.md). Para saber como usar conjuntos de mapeamento na API de Preparo de dados, leia o [Guia do desenvolvedor de Preparo de dados](./api/overview.md).
