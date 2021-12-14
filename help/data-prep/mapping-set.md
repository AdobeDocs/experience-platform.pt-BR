---
keywords: Experience Platform; home; mapeador; conjunto de mapeamento; mapeamento;
solution: Experience Platform
title: Visão geral dos conjuntos de mapeamento
topic-legacy: overview
description: Saiba como usar conjuntos de mapeamento com a Preparação de dados do Adobe Experience Platform.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Visão geral dos conjuntos de mapeamento

Um conjunto de mapeamentos é um conjunto de mapeamentos que transforma dados de um esquema para outro. Este documento fornece informações sobre como os conjuntos de mapeamento são compostos, incluindo schema de entrada, schema de saída e mapeamentos.

## Introdução

Essa visão geral requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Preparação de dados](./home.md): A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).
- [Fluxos de dados](../dataflows/home.md): Os fluxos de dados são uma representação de trabalhos de dados que movem dados pela Plataforma. Os fluxos de dados são configurados em diferentes serviços, ajudando a mover dados de conectores de origem para conjuntos de dados de destino, para [!DNL Identity] e [!DNL Profile]e para [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Os métodos pelos quais os dados podem ser enviados para [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.

## Sintaxe do conjunto de mapeamento

Um conjunto de mapeamentos é composto de uma ID, nome, schema de entrada, schema de saída e uma lista de mapeamentos associados.

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
| `id` | Um identificador exclusivo para o conjunto de mapeamento. |
| `name` | O nome do conjunto de mapeamentos. |
| `inputSchema` | O esquema XDM para os dados recebidos. |
| `outputSchema` | O esquema XDM ao qual os dados de entrada serão transformados em conformidade. |
| `mappings` | Uma matriz de mapeamentos de campo para campo do schema de origem para o schema de destino. |
| `sourceType` | Para cada mapeamento listado, sua `sourceType` indica o tipo de fonte que deve ser mapeada. Pode ser um dos `ATTRIBUTE`, `STATIC`ou `EXPRESSION`: <ul><li> `ATTRIBUTE` é usada para qualquer valor encontrado no caminho de origem. </li><li>`STATIC` é usada para valores inseridos no caminho de destino. Esse valor permanece constante e não é afetado pelo schema de origem.</li><li> `EXPRESSION` é usada para uma expressão, que será resolvida durante o tempo de execução. Uma lista de expressões disponíveis pode ser encontrada no [guia de funções de mapeamento](./functions.md).</li> </ul> |
| `source` | Para cada mapeamento listado, a variável `source` indica o campo que você deseja mapear. Encontre mais informações sobre como configurar sua fonte no [seção fontes](#sources). |
| `destination` | Para cada mapeamento listado, a variável `destination` indica o campo, ou o caminho para o campo, onde o valor extraído do `source` será colocado. Mais informações sobre como configurar seus destinos podem ser encontradas no [seção destino](#destination). |
| `mappings.name` | (*Opcional*) Um nome para o mapeamento. |
| `mappings.description` | (*Opcional*) Uma descrição do mapeamento. |

## Configuração de fontes de mapeamento

Em um mapeamento, a variável `source` pode ser um campo, uma expressão ou um valor estático. Com base no tipo de origem fornecido, o valor pode ser extraído de várias maneiras.

### Campo em dados em coluna

Ao mapear um campo em dados em colunas, como um arquivo CSV, use a `ATTRIBUTE` tipo de origem. Se o campo contiver `.` em seu nome, use `\` para escapar do valor. Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Ao mapear um campo em dados aninhados, como um arquivo JSON, use a variável `ATTRIBUTE` tipo de origem. Se o campo contiver `.` em seu nome, use `\` para escapar do valor. Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Ao mapear um campo em uma matriz, é possível recuperar um valor específico usando um índice. Para fazer isso, use o `ATTRIBUTE` tipo de origem e o índice do valor que você deseja mapear. Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Usar o `ATTRIBUTE` tipo de origem, também é possível mapear diretamente uma matriz para uma matriz ou um objeto para um objeto. Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Usar o `ATTRIBUTE` tipo de origem, é possível executar loop repetidamente por arrays e mapeá-los para um schema de destino usando um índice curinga (`[*]`). Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Se quiser mapear uma constante ou um valor estático, use a variável `STATIC` tipo de origem.  Ao usar a variável `STATIC` tipo de origem, a variável `source` representa o valor codificado que deseja atribuir ao `destination`. Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Se quiser mapear uma expressão, use a variável `EXPRESSION` tipo de origem. Uma lista de funções aceitas pode ser encontrada no [guia de funções de mapeamento](./functions.md). Ao usar a variável `EXPRESSION` tipo de origem, a variável `source` representa a função que deseja resolver. Um exemplo desse mapeamento pode ser encontrado abaixo:

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

Em um mapeamento, a variável `destination` é o local onde o valor extraído do `source` será inserido.

### Campo no nível da raiz

Quando quiser mapear a variável `source` para o nível raiz dos dados transformados, siga o exemplo abaixo:

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

Quando quiser mapear a variável `source` para um campo aninhado nos dados transformados, siga o exemplo abaixo:

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

Quando quiser mapear a variável `source` para um índice específico em uma matriz nos dados transformados, siga o exemplo abaixo:

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

Quando você quiser realizar repetições em arrays e mapear os valores para o destino, poderá usar um índice curinga (`[*]`). Um exemplo disso pode ser visto abaixo:

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

Ao ler este documento, agora você deve entender como os conjuntos de mapeamento são construídos, incluindo como configurar mapeamentos individuais em um conjunto de mapeamento. Para obter mais informações sobre outros recursos de Preparação de dados, leia a [Visão geral da preparação de dados](./home.md). Para saber como usar conjuntos de mapeamento na API de preparação de dados, leia o [Guia do desenvolvedor de Preparação de dados](./api/overview.md).
