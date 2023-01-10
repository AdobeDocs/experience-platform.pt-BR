---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Configurar especificações de exploração para fontes de autoatendimento (SDK em lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Fontes de autoatendimento (SDK em lote).
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# Configurar especificações de exploração para fontes de autoatendimento (SDK em lote)

Explorar especificações define os parâmetros necessários para explorar e inspecionar objetos contidos em sua origem. As especificações Explore também definem o formato de resposta retornado quando os objetos são explorados e inspecionados.

>[!TIP]
>
>As especificações de exploração são codificadas permanentemente e você pode simplesmente copiar e colar a carga abaixo de acordo com as especificações de conexão.

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| Explorar as especificações | Descrição | Exemplo |
| --- | --- | --- |
| `name` | Define o nome ou identificador da especificação de exploração. | `Resource` |
| `type` | Define o tipo da especificação de exploração. | `Resource` |
| `requestSpec` | Contém os parâmetros necessários para explorar objetos na conexão. |
| `requestSpec.type` | Define o tipo de dados da especificação da solicitação. | `object` |
| `responseSpec` | Contém os parâmetros que definem o formato da mensagem de resposta retornada em relação a uma chamada de exploração. |
| `responseSpec.type` | Define o tipo de dados da especificação de resposta. | `object` |
| `responseSpec.properties` | Contém informações sobre como a mensagem de resposta é formatada. |
| `responseSpec.properties.format` | Define a formatação do schema de resposta. | `object` |
| `responseSpec.properties.format.type` | Define o tipo de dados das propriedades. | `string` |
| `responseSpec.schema` | Contém informações relacionadas a como o schema de resposta é formatado. |
| `responseSpec.schema.type` | Define o tipo de dados do esquema. | `object` |
| `responseSpec.schema.properties` | Contém informações sobre colunas, tipos e itens mantidos em um esquema. |
| `responseSpec.schema.properties.columns.items.properties.name` | Exibe o nome do arquivo. |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Define o tipo de dados do nome do arquivo. | `string` |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Com suas especificações de exploração preenchidas, você pode continuar a criar uma especificação de conexão completa usando o [!DNL Flow Service] API. Consulte a [Guia da API de Fontes de autoatendimento (SDK em lote)](../api/api-overview.md) para obter mais informações.
