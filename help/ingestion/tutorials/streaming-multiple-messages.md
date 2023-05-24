---
keywords: Experience Platform;página inicial;tópicos populares;assimilação por transmissão;assimilação;transmissão de várias mensagens;várias mensagens;
solution: Experience Platform
title: Enviar várias mensagens em uma única solicitação HTTP
type: Tutorial
description: Este documento fornece um tutorial para enviar várias mensagens para o Adobe Experience Platform em uma única solicitação HTTP usando a assimilação por transmissão.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---

# Enviar várias mensagens em uma única solicitação HTTP

Ao transmitir dados para o Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados que estão sendo enviados para o [!DNL Experience Platform].

Este documento fornece um tutorial para o envio de várias mensagens para [!DNL Experience Platform] em uma única solicitação HTTP usando a assimilação por transmissão.

## Introdução

Este tutorial requer entendimento prático do Adobe Experience Platform [!DNL Data Ingestion]. Antes de iniciar este tutorial, reveja a seguinte documentação:

- [Visão geral da assimilação de dados](../home.md): abrange os conceitos principais do [!DNL Experience Platform Data Ingestion], incluindo métodos de assimilação e conectores de dados.
- [Visão geral da assimilação de streaming](../streaming-ingestion/overview.md): o fluxo de trabalho e os componentes da assimilação de streaming, como conexões de streaming, conjuntos de dados, [!DNL XDM Individual Profile], e [!DNL XDM ExperienceEvent].

Este tutorial também requer que você tenha concluído a [Autenticação para o Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) tutorial para fazer chamadas com êxito para o [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece o valor para o Cabeçalho de autorização necessário para todas as chamadas de API neste tutorial. O cabeçalho é mostrado em chamadas de exemplo da seguinte maneira:

- Autorização: Portador `{ACCESS_TOKEN}`

Todas as solicitações de POST exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão de streaming

Primeiro, você deve criar uma conexão de transmissão antes de iniciar a transmissão de dados para [!DNL Experience Platform]. Leia o [criar uma conexão de streaming](./create-streaming-connection.md) guia para saber como criar uma conexão de transmissão.

Depois de registrar uma conexão de transmissão, você, como produtor de dados, terá um URL exclusivo que pode ser usado para transmitir dados para a Platform.

## Transmitir para um conjunto de dados

O exemplo a seguir mostra como enviar várias mensagens para um conjunto de dados específico em uma única solicitação HTTP. Insira a ID do conjunto de dados no cabeçalho da mensagem para que a mensagem seja assimilada diretamente nela.

É possível obter a ID de um conjunto de dados existente usando o [!DNL Platform] ou usando uma operação de listagem na API. A ID do conjunto de dados pode ser encontrada em [Experience Platform](https://platform.adobe.com) acessando o **[!UICONTROL Conjuntos de dados]** , clicando no conjunto de dados para o qual deseja a ID e copiando a cadeia de caracteres do campo ID do conjunto de dados na **[!UICONTROL Informações]** guia. Consulte a [Visão geral do Serviço de catálogo](../../catalog/home.md) para obter informações sobre como recuperar conjuntos de dados usando a API.

Em vez de usar um conjunto de dados existente, você pode criar um novo. Leia as [criar um conjunto de dados usando APIs](../../catalog/api/create-dataset.md) tutorial para obter mais informações sobre como criar um conjunto de dados usando APIs.

**Formato da API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{CONNECTION_ID}` | A ID da conexão de streaming criada. |

**Solicitação**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Resposta**

Uma resposta bem-sucedida retorna um status HTTP 207 (Vários status). A revisão do corpo da resposta fornece mais detalhes sobre o sucesso ou a falha de cada método executado na solicitação. Uma resposta é retornada para cada elemento da matriz de mensagens de solicitação. Veja abaixo um exemplo de resposta bem-sucedida sem falhas de mensagem:

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Para obter mais informações sobre códigos de status, consulte a [códigos de resposta](#response-codes) no Apêndice deste tutorial.

## Identificar mensagens com falha

Comparado ao envio de uma solicitação com uma única mensagem, ao enviar uma solicitação HTTP com várias mensagens, há fatores adicionais a serem considerados, como: como identificar quando os dados falharam ao enviar, quais mensagens específicas falharam ao enviar e como elas podem ser recuperadas, e o que acontece com os dados que são bem-sucedidos quando outras mensagens na mesma solicitação falham.

Antes de prosseguir com este tutorial, é recomendável revisar primeiro a [recuperação de lotes com falha](../quality/retrieve-failed-batches.md) guia.

### Enviar carga de solicitação com mensagens válidas e inválidas

O exemplo a seguir mostra o que acontece quando o lote inclui mensagens válidas e inválidas.

A carga da solicitação é uma matriz de objetos JSON que representam o evento no esquema XDM. Observe que as seguintes condições precisam ser atendidas para que a mensagem seja validada com êxito:
- A variável `imsOrgId` no cabeçalho da mensagem deve corresponder à definição de entrada. Se a carga da solicitação não incluir um `imsOrgId` , a variável [!DNL Data Collection Core Service] O (DCCS) adicionará o campo automaticamente.
- O cabeçalho da mensagem deve fazer referência a um esquema XDM existente criado no [!DNL Platform] IU.
- A variável `datasetId` O campo precisa fazer referência a um conjunto de dados existente no [!DNL Platform], e seu schema precisa corresponder ao schema fornecido no `header` em cada mensagem incluída no corpo da solicitação.

**Formato da API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{CONNECTION_ID}` | A ID da entrada de dados criada. |

**Solicitação**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Resposta**

A carga de resposta inclui um status para cada mensagem junto com um GUID no `xactionId` que pode ser usado para rastreamento.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

O exemplo de resposta acima mostra mensagens de erro para a solicitação anterior. Ao comparar essa resposta com a resposta válida anterior, você pode observar que a solicitação resultou em sucesso parcial, com uma mensagem sendo assimilada com êxito e três mensagens resultando em falha. Observe que ambas as respostas retornam um código de status &quot;207&quot;. Para obter mais informações sobre códigos de status, consulte a [códigos de resposta](#response-codes) no Apêndice deste tutorial.

A primeira mensagem foi enviada com sucesso para [!DNL Platform] e não é afetado pelos resultados das outras mensagens. Como resultado, ao tentar reenviar as mensagens com falha, não é necessário incluir novamente essa mensagem.

A segunda mensagem falhou porque não tinha um corpo de mensagem. A solicitação de coleção espera que os elementos de mensagem tenham seções válidas de cabeçalho e corpo. Adicionar o seguinte código após o cabeçalho na segunda mensagem corrigirá a solicitação, permitindo que a segunda mensagem passe na validação:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

A terceira mensagem falhou devido a uma ID de organização inválida sendo usada no cabeçalho. A organização deve corresponder ao {CONNECTION_ID} no qual você está tentando publicar. Para determinar qual ID de organização corresponde à conexão de streaming que você está usando, é possível executar uma `GET inlet` solicite usando o [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Consulte [recuperação de uma conexão de streaming](./create-streaming-connection.md#get-data-collection-url) para obter um exemplo de como recuperar conexões de streaming criadas anteriormente.

A quarta mensagem falhou porque não seguiu o esquema XDM esperado. A variável `xdmSchema` incluídos no cabeçalho e no corpo da solicitação não correspondem ao esquema XDM da `{DATASET_ID}`. A correção do schema no cabeçalho e no corpo da mensagem permite que ele passe na validação do DCCS e seja enviado com êxito para o [!DNL Platform]. O corpo da mensagem também deve ser atualizado para corresponder ao esquema XDM do `{DATASET_ID}` para que passe na validação de transmissão [!DNL Platform]. Para obter mais informações sobre o que acontece com mensagens que são transmitidas com êxito para a Platform, consulte o [confirmar mensagens assimiladas](#confirm-messages-ingested) deste tutorial.

### Recuperar mensagens com falha de [!DNL Platform]

As mensagens com falha são identificadas por um código de status de erro na matriz de resposta.
As mensagens inválidas são coletadas e armazenadas em um lote de &quot;erros&quot; no conjunto de dados especificado pelo `{DATASET_ID}`.

Leia o [recuperação de lotes com falha](../quality/retrieve-failed-batches.md) guia para obter mais informações sobre como recuperar mensagens em lote com falha.

## Confirmar mensagens assimiladas

As mensagens que passam na validação do DCCS são transmitidas para [!DNL Platform]. Ligado [!DNL Platform], as mensagens em lote são testadas por validação de transmissão antes de serem assimiladas na [!DNL Data Lake]. O status dos lotes, sejam bem-sucedidos ou não, aparecem no conjunto de dados especificado por `{DATASET_ID}`.

Você pode visualizar o status das mensagens em lote que foram transmitidas com êxito para o [!DNL Platform] usando o [IU DO EXPERIENCE PLATFORM](https://platform.adobe.com) acessando o **[!UICONTROL Conjuntos de dados]** clique no conjunto de dados para o qual você está transmitindo e verifique a **[!UICONTROL Atividade do conjunto de dados]** guia.

Mensagens em lote que passam na validação de streaming [!DNL Platform] são assimilados na [!DNL Data Lake]. As mensagens ficam disponíveis para análise ou exportação.

## Próximas etapas

Agora que você sabe como enviar várias mensagens em uma única solicitação e verificar quando as mensagens são assimiladas com êxito no conjunto de dados de destino, você pode começar a transmitir seus próprios dados para o [!DNL Platform]. Para obter uma visão geral de como consultar e recuperar dados assimilados do [!DNL Platform], consulte o [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) guia.

## Apêndice

Esta seção contém informações complementares para o tutorial do.

### Códigos de resposta

A tabela a seguir mostra os códigos de status retornados por mensagens de resposta com êxito e com falha.

| Código de status | Descrição |
| :---: | --- |
| 207 | Embora &#39;207&#39; seja usado como o código de status de resposta geral, o recipient precisa consultar o conteúdo do corpo de resposta de vários status para obter mais informações sobre o sucesso ou a falha da execução do método. O código de resposta é usado em caso de sucesso, sucesso parcial e também em situações de falha. |
| 400 | Houve um problema com a solicitação. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, a carga da mensagem não tinha os campos obrigatórios ou a mensagem tinha um formato xdm desconhecido). |
| 401 | Não autorizado: a solicitação não tem um cabeçalho de autorização válido. Isso só é retornado para entradas que têm autenticação habilitada. |
| 403 | Não autorizado: o token de autorização fornecido é inválido ou expirou. Isso só é retornado para entradas que têm autenticação habilitada. |
| 413 | Carga muito grande - lançado quando a solicitação de carga total é maior que 1 MB. |
| 429 | Muitas solicitações dentro da duração de tempo especificada. |
| 500 | Erro ao processar a carga. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, Esquema de carga da mensagem não especificado ou não correspondeu à definição do XDM no [!DNL Platform]). |
| 503 | Serviço não disponível no momento. Os clientes devem tentar novamente pelo menos 3 vezes usando uma estratégia de retirada exponencial. |
