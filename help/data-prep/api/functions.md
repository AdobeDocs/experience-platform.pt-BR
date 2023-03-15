---
keywords: Experience Platform;página inicial;tópicos populares;preparação de dados;guia de api;esquemas;
title: Endpoint da API de funções
description: Você pode usar o endpoint "/functions" na API de preparação de dados para validar as expressões de mapeamento e listar as funções de conjunto de mapeamento disponíveis.
exl-id: dc24bfb4-2d96-4757-a610-0c2ee960d41d
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 5%

---

# Endpoints de funções

As funções do conjunto de mapeamento permitem transformar seus dados entre esquemas de origem e de destino. Você pode usar o `/languages/el` para validar suas expressões, bem como obter uma lista de todas as funções do conjunto de mapeamento disponíveis.

## Validar expressões

Você pode validar se sua expressão atual é válida fazendo uma solicitação POST para o `/languages/el/validate` terminal.

**Formato da API**

```
POST /languages/el/validate
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com o status de validação da expressão.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Listar funções de conjunto de mapeamento

Você pode recuperar uma lista de todas as funções do conjunto de mapeamento disponíveis fazendo uma solicitação GET para o `/languages/el/functions` terminal.

**Formato da API**

```
GET /languages/el/functions
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de todas as funções do conjunto de mapeamento disponíveis.

>[!NOTE]
>
>Esta resposta foi truncada por questões de espaço.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Operadores de conjunto de mapeamento de lista

Você pode recuperar uma lista de todos os operadores de conjunto de mapeamento disponíveis fazendo uma solicitação GET para o `/languages/el/operators` terminal.

**Formato da API**

```
GET /languages/el/operators
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de todos os operadores de conjunto de mapeamento disponíveis.

>[!NOTE]
>
>Esta resposta foi truncada por questões de espaço.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
