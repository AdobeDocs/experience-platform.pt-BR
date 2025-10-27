---
keywords: Experience Platform;página inicial;tópicos populares;assimilação por transmissão;assimilação;transmissão de várias mensagens;várias mensagens;
solution: Experience Platform
title: Enviar várias mensagens em uma única solicitação HTTP
type: Tutorial
description: Este documento fornece um tutorial para enviar várias mensagens para o Adobe Experience Platform em uma única solicitação HTTP usando a assimilação por transmissão.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 31c00e69dd92f7c3232e09f02da36c60cd8cf486
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 1%

---

# Enviar várias mensagens em uma única solicitação HTTP

Ao transmitir dados para o Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados enviados para [!DNL Experience Platform].

Este documento fornece um tutorial para enviar várias mensagens para [!DNL Experience Platform] em uma única solicitação HTTP usando a assimilação por transmissão.

## Introdução

Este tutorial requer uma compreensão funcional do Adobe Experience Platform [!DNL Data Ingestion]. Antes de iniciar este tutorial, reveja a seguinte documentação:

- [Visão geral da assimilação de dados](../home.md): abrange os conceitos principais de [!DNL Experience Platform Data Ingestion], incluindo métodos de assimilação e conectores de dados.
- [Visão geral da assimilação de streaming](../streaming-ingestion/overview.md): o fluxo de trabalho e os componentes básicos da assimilação de streaming, como conexões de streaming, conjuntos de dados, [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent].

Este tutorial também requer que você tenha concluído o tutorial [Autenticação para o Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para as APIs [!DNL Experience Platform]. A conclusão do tutorial de autenticação fornece o valor para o Cabeçalho de autorização necessário para todas as chamadas de API neste tutorial. O cabeçalho é mostrado em chamadas de exemplo da seguinte maneira:

- Autorização: Portador `{ACCESS_TOKEN}`

Todas as solicitações de POST exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão de streaming

Você deve primeiro criar uma conexão de streaming antes de iniciar a transmissão de dados para [!DNL Experience Platform]. Leia o guia [criar uma conexão de streaming](./create-streaming-connection.md) para saber como criar uma conexão de streaming.

Depois de registrar uma conexão de transmissão, você, como produtor de dados, terá um URL exclusivo que pode ser usado para transmitir dados para o Experience Platform.

## Transmitir para um conjunto de dados

O exemplo a seguir mostra como enviar várias mensagens para um conjunto de dados específico em uma única solicitação HTTP. Insira a ID do conjunto de dados no cabeçalho da mensagem para que a mensagem seja assimilada diretamente nela.

Você pode obter a ID de um conjunto de dados existente usando a interface do usuário [!DNL Experience Platform] ou usando uma operação de listagem na API. A ID do conjunto de dados pode ser encontrada no [Experience Platform](https://platform.adobe.com) acessando a guia **[!UICONTROL Datasets]**, clicando no conjunto de dados para o qual você deseja a ID e copiando a cadeia de caracteres do campo de ID do conjunto de dados na guia **[!UICONTROL Info]**. Consulte a [Visão geral do Serviço de catálogo](../../catalog/home.md) para obter informações sobre como recuperar conjuntos de dados usando a API.

Em vez de usar um conjunto de dados existente, você pode criar um novo. Leia o tutorial [criar um conjunto de dados usando APIs](../../catalog/api/create-dataset.md) para obter mais informações sobre como criar um conjunto de dados usando APIs.

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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

Para obter mais informações sobre códigos de status, consulte a tabela [códigos de resposta](#response-codes) no Apêndice deste tutorial.

## Identificar mensagens com falha

Comparado ao envio de uma solicitação com uma única mensagem, ao enviar uma solicitação HTTP com várias mensagens, há fatores adicionais a serem considerados, como: como identificar quando os dados falharam ao enviar, quais mensagens específicas falharam ao enviar e como elas podem ser recuperadas, e o que acontece com os dados que são bem-sucedidos quando outras mensagens na mesma solicitação falham.

Antes de prosseguir com este tutorial, é recomendável primeiro revisar o guia [recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### Enviar carga de solicitação com mensagens válidas e inválidas

O exemplo a seguir mostra o que acontece quando o lote inclui mensagens válidas e inválidas.

A carga da solicitação é uma matriz de objetos JSON que representam o evento no esquema XDM. Observe que as seguintes condições precisam ser atendidas para que a mensagem seja validada com êxito:
- O campo `imsOrgId` no cabeçalho da mensagem deve corresponder à definição de entrada. Se a carga da solicitação não incluir um campo `imsOrgId`, o [!DNL Data Collection Core Service] (DCCS) adicionará o campo automaticamente.
- O cabeçalho da mensagem deve fazer referência a um esquema XDM existente criado na interface do usuário do [!DNL Experience Platform].
- O campo `datasetId` precisa fazer referência a um conjunto de dados existente em [!DNL Experience Platform], e seu esquema precisa corresponder ao esquema fornecido no objeto `header` em cada mensagem incluída no corpo da solicitação.

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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

O exemplo de resposta acima mostra mensagens de erro para a solicitação anterior. Ao comparar essa resposta com a resposta válida anterior, você pode observar que a solicitação resultou em sucesso parcial, com uma mensagem sendo assimilada com êxito e três mensagens resultando em falha. Observe que ambas as respostas retornam um código de status &quot;207&quot;. Para obter mais informações sobre códigos de status, consulte a tabela [códigos de resposta](#response-codes) no Apêndice deste tutorial.

A primeira mensagem foi enviada com êxito para [!DNL Experience Platform] e não é afetada pelos resultados das outras mensagens. Como resultado, ao tentar reenviar as mensagens com falha, não é necessário incluir novamente essa mensagem.

A segunda mensagem falhou porque não tinha um corpo de mensagem. A solicitação de coleção espera que os elementos de mensagem tenham seções válidas de cabeçalho e corpo. Adicionar o seguinte código após o cabeçalho na segunda mensagem corrigirá a solicitação, permitindo que a segunda mensagem passe na validação:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

A terceira mensagem falhou devido a uma ID de organização inválida sendo usada no cabeçalho. A organização deve corresponder ao {CONNECTION_ID} para o qual você está tentando postar. Para determinar qual ID de organização corresponde à conexão de streaming que você está usando, é possível executar uma solicitação `GET inlet` usando o [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Consulte [recuperando uma conexão de streaming](./create-streaming-connection.md#get-data-collection-url) para obter um exemplo de como recuperar conexões de streaming criadas anteriormente.

A quarta mensagem falhou porque não seguiu o esquema XDM esperado. O `xdmSchema` incluído no cabeçalho e no corpo da solicitação não corresponde ao esquema XDM do `{DATASET_ID}`. A correção do esquema no cabeçalho e no corpo da mensagem permite que ele passe na validação do DCCS e seja enviado com êxito para [!DNL Experience Platform]. O corpo da mensagem também deve ser atualizado para corresponder ao esquema XDM do `{DATASET_ID}` para passar na validação de streaming em [!DNL Experience Platform]. Para obter mais informações sobre o que acontece com mensagens transmitidas com êxito para o Experience Platform, consulte a seção [confirmar mensagens assimiladas](#confirm-messages-ingested) deste tutorial.

### Recuperar mensagens com falha de [!DNL Experience Platform]

As mensagens com falha são identificadas por um código de status de erro na matriz de resposta.
As mensagens inválidas são coletadas e armazenadas em um lote de &quot;erros&quot; no conjunto de dados especificado por `{DATASET_ID}`.

Leia o guia [recuperação de lotes com falha](../quality/retrieve-failed-batches.md) para obter mais informações sobre como recuperar mensagens em lote com falha.

## Confirmar mensagens assimiladas

Mensagens que passaram na validação DCCS são transmitidas para [!DNL Experience Platform]. Em [!DNL Experience Platform], as mensagens em lote são testadas pela validação de streaming antes de serem assimiladas no [!DNL Data Lake]. O status dos lotes, sejam bem-sucedidos ou não, aparecem no conjunto de dados especificado por `{DATASET_ID}`.

Você pode visualizar o status de mensagens em lote que foram transmitidas com êxito para [!DNL Experience Platform] usando a [Interface do usuário do Experience Platform](https://platform.adobe.com) acessando a guia **[!UICONTROL Datasets]**, clicando no conjunto de dados para o qual você está transmitindo e verificando a guia **[!UICONTROL Dataset Activity]**.

Mensagens em lote que passam na validação de streaming em [!DNL Experience Platform] são assimiladas no [!DNL Data Lake]. As mensagens ficam disponíveis para análise ou exportação.

## Próximas etapas

Agora que você sabe como enviar várias mensagens em uma única solicitação e verificar quando as mensagens são assimiladas com êxito no conjunto de dados de destino, você pode começar a transmitir seus próprios dados para [!DNL Experience Platform]. Para obter uma visão geral de como consultar e recuperar dados assimilados de [!DNL Experience Platform], consulte o guia [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md).

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
| 500 | Erro ao processar a carga. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, esquema de carga da mensagem não especificado ou que não corresponde à definição XDM em [!DNL Experience Platform]). |
| 503 | Serviço não disponível no momento. Os clientes devem tentar novamente pelo menos 3 vezes usando uma estratégia de retirada exponencial. |
