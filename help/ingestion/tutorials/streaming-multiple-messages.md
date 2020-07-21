---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Transmissão de várias mensagens em uma única solicitação HTTP
topic: tutorial
translation-type: tm+mt
source-git-commit: 80392190c7fcae9b6e73cc1e507559f834853390
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 1%

---


# Envio de várias mensagens em uma única solicitação HTTP

Ao transmitir dados para o Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados que estão sendo enviados para [!DNL Experience Platform].

Este documento fornece um tutorial para enviar várias mensagens para [!DNL Experience Platform] dentro de uma única solicitação HTTP usando a ingestão de streaming.

## Introdução

Este tutorial requer uma compreensão funcional da Adobe Experience Platform [!DNL Data Ingestion]. Antes de iniciar este tutorial, reveja a seguinte documentação:

- [Visão geral](../home.md)da ingestão de dados: Abrange os conceitos principais de [!DNL Experience Platform Data Ingestion], incluindo métodos de ingestão e conectores de dados.
- [Visão geral](../streaming-ingestion/overview.md)da assimilação de transmissão: O fluxo de trabalho e os blocos componentes da assimilação de streaming, como conexões de streaming, conjuntos de dados [!DNL XDM Individual Profile]e [!DNL XDM ExperienceEvent].

Este tutorial também exige que você tenha concluído o tutorial [Autenticação para Adobe Experience Platform](../../tutorials/authentication.md) para fazer chamadas com êxito para [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece o valor para o cabeçalho de Autorização necessário para todas as chamadas de API neste tutorial. O cabeçalho é mostrado nas chamadas de amostra da seguinte maneira:

- Autorização: Portador `{ACCESS_TOKEN}`

Todas as solicitações POST exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão de streaming

Primeiro, você deve criar uma conexão de streaming antes de poder start os dados de streaming. [!DNL Experience Platform] Leia o guia [Criar uma conexão](./create-streaming-connection.md) de streaming para saber como criar uma conexão de streaming.

Depois de registrar uma conexão de streaming, você, como produtor de dados, terá um URL exclusivo que pode ser usado para transmitir dados para a Platform.

## Fluxo para um conjunto de dados

O exemplo a seguir mostra como enviar várias mensagens para um conjunto de dados específico em uma única solicitação HTTP. Insira a ID do conjunto de dados no cabeçalho da mensagem para que a mensagem seja assimilada diretamente nela.

Você pode obter a ID de um conjunto de dados existente usando a [!DNL Platform] interface do usuário ou uma operação de listagem na API. A ID do conjunto de dados pode ser encontrada no [Experience Platform](https://platform.adobe.com) , indo até a guia **[!UICONTROL Conjuntos]** de dados, clicando no conjunto de dados para o qual deseja obter a ID e copiando a string do campo ID **[!UICONTROL do]** Conjunto de dados na guia **[!UICONTROL Informações]** . Consulte a visão geral [do serviço de](../../catalog/home.md) catálogo para obter informações sobre como recuperar conjuntos de dados usando a API.

Em vez de usar um conjunto de dados existente, você pode criar um novo conjunto de dados. Leia o tutorial para [criar um conjunto de dados usando APIs](../../catalog/api/create-dataset.md) para obter mais informações sobre como criar um conjunto de dados usando APIs.

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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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

Uma resposta bem-sucedida retorna um status HTTP 207 (Multi-status). A revisão do corpo da resposta fornece mais detalhes sobre o sucesso ou a falha de cada método executado na solicitação. Uma resposta é retornada para cada elemento da matriz de mensagens de solicitação. Abaixo está um exemplo de uma resposta bem-sucedida sem falhas de mensagem:

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

Para obter mais informações sobre códigos de status, consulte a tabela de códigos [de](#response-codes) resposta no Apêndice deste tutorial.

## Identificar mensagens com falha

Em comparação ao envio de uma solicitação com uma única mensagem, ao enviar uma solicitação HTTP com várias mensagens, há fatores adicionais a serem considerados, como: como identificar quando os dados falharam no envio, quais mensagens específicas falharam no envio e como eles podem ser recuperados, e o que acontece com os dados que têm êxito quando outras mensagens na mesma solicitação falham.

Antes de continuar com este tutorial, é recomendável primeiro revisar o guia de [recuperação de lotes](../quality/retrieve-failed-batches.md) com falha.

### Enviar carga de solicitação com mensagens válidas e inválidas

O exemplo a seguir mostra o que acontece quando o lote inclui mensagens válidas e inválidas.

A carga da solicitação é uma matriz de objetos JSON que representam o evento no schema XDM. Observe que as seguintes condições precisam ser atendidas para uma validação bem-sucedida da mensagem:
- O `imsOrgId` campo no cabeçalho da mensagem deve corresponder à definição de entrada. Se a carga da solicitação não incluir um `imsOrgId` campo, o [!DNL Data Collection Core Service] (DCCS) adicionará o campo automaticamente.
- O cabeçalho da mensagem deve fazer referência a um schema XDM existente criado na [!DNL Platform] interface do usuário.
- O `datasetId` campo precisa fazer referência a um conjunto de dados existente no [!DNL Platform]e seu schema precisa corresponder ao schema fornecido no `header` objeto dentro de cada mensagem incluída no corpo da solicitação.

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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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

A carga de resposta inclui um status para cada mensagem junto com um GUID no `xactionId` qual pode ser usado para rastreamento.

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

O exemplo de resposta acima mostra mensagens de erro para a solicitação anterior. Ao comparar essa resposta com a resposta válida anterior, você pode observar que a solicitação resultou em um sucesso parcial, com uma mensagem sendo ingerida com sucesso e três mensagens resultando em falha. Observe que ambas as respostas retornam um código de status &#39;207&#39;. Para obter mais informações sobre códigos de status, consulte a tabela de códigos [de](#response-codes) resposta no Apêndice deste tutorial.

A primeira mensagem foi enviada com êxito para [!DNL Platform] e não é afetada pelos resultados das outras mensagens. Como resultado, ao tentar reenviar as mensagens com falha, não é necessário reincluir essa mensagem.

A segunda mensagem falhou porque faltou um corpo de mensagem. A solicitação de coleção espera que os elementos de mensagem tenham seções de cabeçalho e corpo válidas. A adição do seguinte código após o cabeçalho na segunda mensagem corrigirá a solicitação, permitindo que a segunda mensagem passe na validação:

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

A terceira mensagem falhou porque uma ID de organização IMS inválida estava sendo usada no cabeçalho. A organização IMS deve corresponder à {CONNECTION_ID} para a qual você está tentando postar. Para determinar qual ID de organização IMS corresponde à conexão de streaming que você está usando, é possível executar uma `GET inlet` solicitação usando o [!DNL Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Consulte [recuperação de uma conexão](./create-streaming-connection.md#get-data-collection-url) de streaming para obter um exemplo de como recuperar conexões de streaming criadas anteriormente.

A quarta mensagem falhou porque não seguiu o schema XDM esperado. Os itens `xdmSchema` incluídos no cabeçalho e no corpo da solicitação não correspondem ao schema XDM da `{DATASET_ID}`. A correção do schema no cabeçalho e no corpo da mensagem permite que ele passe pela validação do DCCS e seja enviado com êxito para [!DNL Platform]. O corpo da mensagem também deve ser atualizado para corresponder ao schema XDM do para `{DATASET_ID}` que ele passe a validação de streaming [!DNL Platform]. Para obter mais informações sobre o que acontece com as mensagens que fluem com êxito para o Platform, consulte a seção [confirmar mensagens assimiladas](#confirm-messages-ingested) deste tutorial.

### Recuperar mensagens com falha de [!DNL Platform]

Mensagens com falha são identificadas por um código de status de erro na matriz de respostas.
As mensagens inválidas são coletadas e armazenadas em um lote de &quot;erro&quot; no conjunto de dados especificado por `{DATASET_ID}`.

Leia o guia de [recuperação de lotes](../quality/retrieve-failed-batches.md) com falha para obter mais informações sobre como recuperar mensagens em lote com falha.

## Confirmar mensagens ingeridas

As mensagens que passam na validação do DCCS são transmitidas para [!DNL Platform]. Em [!DNL Platform], as mensagens em lote são testadas pela validação de streaming antes de serem ingeridas no [!DNL Data Lake]. O status dos lotes, com ou sem êxito, é exibido no conjunto de dados especificado por `{DATASET_ID}`.

Você pode visualização o status das mensagens em lote que são enviadas com êxito para [!DNL Platform] usar a interface do usuário [do](https://platform.adobe.com) Experience Platform, indo até a guia **[!UICONTROL Conjuntos]** de dados, clicando no conjunto de dados para o qual você está fazendo streaming e verificando a guia Atividade **** do Conjunto de dados.

As mensagens em lote que passam pela validação do streaming [!DNL Platform] são ingeridas no [!DNL Data Lake]. As mensagens estão disponíveis para análise ou exportação.

## Próximas etapas

Agora que você sabe como enviar várias mensagens em uma única solicitação e verificar quando as mensagens são ingeridas com êxito no conjunto de dados do público alvo, é possível fazer o start do streaming dos seus próprios dados para [!DNL Platform]. Para obter uma visão geral de como query e recuperar dados ingeridos de [!DNL Platform], consulte o [!DNL Data Access](../../data-access/tutorials/dataset-data.md) guia.

## Apêndice

Esta seção contém informações adicionais para o tutorial.

### Códigos de resposta

A tabela a seguir mostra os códigos de status retornados por mensagens de resposta bem-sucedidas e com falha.

| Código de status | Descrição |
| :---: | --- |
| 207 | Embora &quot;207&quot; seja usado como o código de status de resposta geral, o recipient precisa consultar o conteúdo do corpo de resposta de multistatus para obter mais informações sobre o sucesso ou falha da execução do método. O código de resposta é usado em situações de sucesso, sucesso parcial e também em situações de falha. |
| 400 | Houve um problema com o pedido. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, a carga da mensagem não possuía os campos obrigatórios ou a mensagem era desconhecida no formato xdm). |
| 401 | Não autorizado: cabeçalho de autorização válido ausente na solicitação. Isso só é retornado para entradas com autenticação ativada. |
| 403 | Não autorizado:  O token de autorização fornecido é inválido ou expirou. Isso só é retornado para entradas com autenticação ativada. |
| 413 | Carga muito grande - emitida quando a solicitação de carga total é maior que 1 MB. |
| 429 | Demasiadas solicitações dentro de uma duração de tempo especificada. |
| 500 | Erro ao processar a carga. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, schema de carga de mensagem não especificado ou não corresponde à definição XDM em [!DNL Platform]). |
| 503 | O serviço não está disponível no momento. Os clientes devem tentar novamente pelo menos 3 vezes usando uma estratégia de back-off exponencial. |