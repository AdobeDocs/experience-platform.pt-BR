---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Configurar especificações de exploração para Origens de Autoatendimento (SDK em Lote)
description: Este documento fornece uma visão geral das configurações que você precisa preparar para usar as Origens de Autoatendimento (SDK em Lote).
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# Configurar especificações de exploração para Origens de Autoatendimento (SDK em Lote)

Explorar especificações define os parâmetros necessários para explorar e inspecionar objetos contidos na sua origem. Explorar especificações também define o formato de resposta retornado quando os objetos são explorados e inspecionados.

>[!TIP]
>
>As especificações do Explore são codificadas e você pode simplesmente copiar e colar o conteúdo abaixo na especificação da sua conexão.

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

| Explorar especificações | Descrição | Exemplo |
| --- | --- | --- |
| `name` | Define o nome ou identificador da especificação de exploração. | `Resource` |
| `type` | Define o tipo da especificação de exploração. | `Resource` |
| `requestSpec` | Contém os parâmetros necessários para explorar objetos na conexão. |  |
| `requestSpec.type` | Define o tipo de dados da especificação da solicitação. | `object` |
| `responseSpec` | Contém os parâmetros que definem o formato da mensagem de resposta retornada em relação a uma chamada de exploração. |  |
| `responseSpec.type` | Define o tipo de dados da especificação da resposta. | `object` |
| `responseSpec.properties` | Contém informações relacionadas a como a mensagem de resposta está formatada. |  |
| `responseSpec.properties.format` | Define a formatação do schema de resposta. | `object` |
| `responseSpec.properties.format.type` | Define o tipo de dados das propriedades. | `string` |
| `responseSpec.schema` | Contém informações relacionadas a como o esquema de resposta é formatado. |  |
| `responseSpec.schema.type` | Define o tipo de dados do esquema. | `object` |
| `responseSpec.schema.properties` | Contém informações sobre as colunas, o tipo e os itens mantidos em um esquema. |  |
| `responseSpec.schema.properties.columns.items.properties.name` | Exibe o nome do arquivo. |  |
| `responseSpec.schema.properties.columns.items.properties.name.type` | Define o tipo de dados do nome do arquivo. | `string` |

{style="table-layout:auto"}

## Próximas etapas

Com suas especificações de exploração preenchidas, você pode prosseguir para criar uma especificação de conexão completa usando a API [!DNL Flow Service]. Consulte o [Guia da API de Fontes de Autoatendimento (SDK em Lote)](../api/api-overview.md) para obter mais informações.
