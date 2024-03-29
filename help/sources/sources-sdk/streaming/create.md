---
title: Crie uma nova especificação de conexão para o SDK de streaming usando a API do serviço de fluxo
description: O documento a seguir fornece etapas sobre como criar uma especificação de conexão usando a API de Serviço de Fluxo e integrar uma nova origem por meio de Origens de Autoatendimento.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# Crie uma nova especificação de conexão usando o [!DNL Flow Service] API

>[!NOTE]
>
>O SDK de transmissão de fontes de autoatendimento está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Uma especificação de conexão representa a estrutura de uma origem. Ele contém informações sobre os requisitos de autenticação de uma origem, define como os dados de origem podem ser explorados e inspecionados e fornece informações sobre os atributos de uma determinada origem. A variável `/connectionSpecs` endpoint na variável [!DNL Flow Service] A API permite gerenciar programaticamente as especificações de conexão em sua organização.

O documento a seguir fornece etapas sobre como criar uma especificação de conexão usando o [!DNL Flow Service] e integre uma nova fonte por meio de Fontes de autoatendimento (SDK de transmissão).

## Introdução

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Coletar artefatos

Para criar uma nova fonte de transmissão usando Fontes de autoatendimento, primeiro você deve coordenar com o Adobe, solicitar um repositório Git privado e alinhar com o Adobe nos detalhes sobre o rótulo, a descrição, a categoria e o ícone da fonte.

Depois de fornecido, você deve estruturar seu repositório Git privado da seguinte maneira:

* Origens
   * {your_source}
      * Artefatos
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefatos (nomes de arquivo) | Descrição | Exemplo |
| --- | --- | --- |
| {your_source} | O nome da fonte. Esta pasta deve conter todos os artefatos relacionados à sua origem, dentro do seu repositório Git privado. | `medallia` |
| {your_source}-category.txt | A categoria à qual a origem pertence, formatada como um arquivo de texto. **Nota**: Se você acredita que sua fonte não se encaixa em nenhuma das categorias acima, entre em contato com o representante da Adobe para discutir. | `medallia-category.txt` Dentro do arquivo, especifique a categoria da sua origem, como: `streaming`. |
| {your_source}-description.txt | Uma breve descrição da sua origem. | [!DNL Medallia] é uma fonte de automação de marketing que você pode usar para trazer [!DNL Medallia] dados para Experience Platform. |
| {your_source}-icon.svg | A imagem a ser usada para representar sua fonte no catálogo de fontes de Experience Platform. Esse ícone deve ser um arquivo SVG. |
| {your_source}-label.txt | O nome da fonte como deve aparecer no catálogo de fontes Experience Platform. | Medália |
| {your_source}-connectionSpec.json | Um arquivo JSON que contém a especificação de conexão da origem. Inicialmente, esse arquivo não é necessário, pois você preencherá a especificação de conexão ao concluir este guia. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Durante o período de teste de sua especificação de conexão, em vez de valores-chave, você pode usar `text` na especificação da conexão.

Depois de adicionar os arquivos necessários ao repositório Git privado, você deve criar uma solicitação de pull (PR) para o Adobe revisar. Quando sua PR for aprovada e mesclada, você receberá uma ID que poderá ser usada para a especificação da conexão para consultar o rótulo, a descrição e o ícone da fonte.

Em seguida, siga as etapas descritas abaixo para configurar sua especificação de conexão. Para obter orientação adicional sobre as diferentes funcionalidades que podem ser adicionadas à sua origem, como agendamento avançado, esquema personalizado ou diferentes tipos de paginação, revise o guia em [configurando especificações de origem](../config/sourcespec.md).

## Copiar modelo de especificação de conexão

Depois de coletar os artefatos necessários, copie e cole o modelo de especificação de conexão abaixo no editor de texto de sua escolha e atualize os atributos entre colchetes `{}` com informações relevantes para sua fonte específica.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Criar uma especificação de conexão {#create}

Depois de adquirir o modelo de especificação de conexão, você pode começar a criar uma nova especificação de conexão preenchendo os valores apropriados que correspondem à sua origem.

Uma especificação de conexão pode ser dividida em duas partes distintas: as especificações de origem e as especificações de exploração.

Consulte os seguintes documentos para obter mais informações sobre as seções de uma especificação de conexão:

* [Configurar a especificação de origem](../config/sourcespec.md)
* [Configurar a especificação de exploração](../config/explorespec.md)

Com as informações de especificação atualizadas, você pode submeter a nova especificação de conexão fazendo uma solicitação POST para o `/connectionSpecs` endpoint do [!DNL Flow Service] API.

**Formato da API**

```http
POST /connectionSpecs
```

**Solicitação**

A solicitação a seguir é um exemplo de uma especificação de conexão totalmente criada para uma fonte de transmissão:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna a especificação de conexão recém-criada, incluindo sua `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## Próximas etapas

Agora que você criou uma nova especificação de conexão, deverá adicionar seu ID de especificação de conexão correspondente a uma especificação de fluxo existente. Veja o tutorial sobre [atualização das especificações de fluxo](./update-flow-specs.md) para obter mais informações.

Para fazer modificações na especificação de conexão criada, consulte o tutorial em [atualizando especificações de conexão](./update-connection-specs.md).
