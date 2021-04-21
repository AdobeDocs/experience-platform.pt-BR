---
keywords: Experience Platform; home; tópicos populares; assimilação de streaming; ingestão; streaming de várias mensagens; várias mensagens;
solution: Experience Platform
title: Enviar várias mensagens em uma única solicitação HTTP
topic-legacy: tutorial
type: Tutorial
description: Este documento fornece um tutorial para enviar várias mensagens para o Adobe Experience Platform em uma única solicitação HTTP usando assimilação de streaming.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 1%

---

# Enviar várias mensagens em uma única solicitação HTTP

Ao transmitir dados para o Adobe Experience Platform, fazer várias chamadas HTTP pode ser caro. Por exemplo, em vez de criar 200 solicitações HTTP com cargas de 1 KB, é muito mais eficiente criar 1 solicitação HTTP com 200 mensagens de 1 KB cada, com uma única carga de 200 KB. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar os dados que estão sendo enviados para [!DNL Experience Platform].

Este documento fornece um tutorial para enviar várias mensagens para [!DNL Experience Platform] em uma única solicitação HTTP usando assimilação de streaming.

## Introdução

Este tutorial requer uma compreensão funcional do Adobe Experience Platform [!DNL Data Ingestion]. Antes de iniciar este tutorial, reveja a seguinte documentação:

- [Visão geral](../home.md) da assimilação de dados: Aborda os principais conceitos do  [!DNL Experience Platform Data Ingestion], incluindo métodos de assimilação e conectores de dados.
- [Visão geral](../streaming-ingestion/overview.md) da assimilação de streaming: O fluxo de trabalho e os blocos de construção da assimilação de streaming, como conexões de streaming, conjuntos de dados  [!DNL XDM Individual Profile]e  [!DNL XDM ExperienceEvent].

Este tutorial também requer que você tenha concluído o tutorial [Autenticação para Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs [!DNL Platform]. A conclusão do tutorial de autenticação fornece o valor para o cabeçalho de Autorização exigido por todas as chamadas de API neste tutorial. O cabeçalho é mostrado em chamadas de amostra da seguinte maneira:

- Autorização: Portador `{ACCESS_TOKEN}`

Todas as solicitações de POST exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Criar uma conexão de transmissão

Primeiro, você deve criar uma conexão de transmissão para iniciar o streaming de dados em [!DNL Experience Platform]. Leia o guia [create a streaming connection](./create-streaming-connection.md) para saber como criar uma conexão de transmissão.

Após registrar uma conexão de transmissão, você, como produtor de dados, terá um URL exclusivo que pode ser usado para transmitir dados para a Plataforma.

## Transmitir para um conjunto de dados

O exemplo a seguir mostra como enviar várias mensagens para um conjunto de dados específico em uma única solicitação HTTP. Insira a ID do conjunto de dados no cabeçalho da mensagem para que a mensagem seja assimilada diretamente nela.

Você pode obter a ID de um conjunto de dados existente usando a interface do usuário [!DNL Platform] ou usando uma operação de listagem na API. A ID do conjunto de dados pode ser encontrada em [Experience Platform](https://platform.adobe.com) acessando a guia **[!UICONTROL Datasets]**, clicando no conjunto de dados para o qual deseja a ID e copiando a cadeia de caracteres do campo de ID do conjunto de dados na guia **[!UICONTROL Info]**. Consulte a [Visão geral do Serviço de catálogo](../../catalog/home.md) para obter informações sobre como recuperar conjuntos de dados usando a API.

Em vez de usar um conjunto de dados existente, você pode criar um novo conjunto de dados. Leia o tutorial [criar um conjunto de dados usando APIs](../../catalog/api/create-dataset.md) para obter mais informações sobre como criar um conjunto de dados usando APIs.

**Formato da API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{CONNECTION_ID}` | A ID da conexão de transmissão criada. |

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

Para obter mais informações sobre códigos de status, consulte a tabela [códigos de resposta](#response-codes) no Apêndice deste tutorial.

## Identificar mensagens com falha

Em comparação ao envio de uma solicitação com uma única mensagem, ao enviar uma solicitação HTTP com várias mensagens, há fatores adicionais a serem considerados, como: como identificar quando os dados falharam no envio, quais mensagens específicas falharam no envio e como eles podem ser recuperados, e o que acontece com os dados que têm sucesso quando outras mensagens na mesma solicitação falham.

Antes de prosseguir com este tutorial, é recomendável revisar primeiro o guia [recuperar lotes com falha](../quality/retrieve-failed-batches.md).

### Enviar carga de solicitação com mensagens válidas e inválidas

O exemplo a seguir mostra o que acontece quando o lote inclui mensagens válidas e inválidas.

A carga da solicitação é uma matriz de objetos JSON que representam o evento no esquema XDM. Observe que as seguintes condições precisam ser atendidas para uma validação bem-sucedida da mensagem:
- O campo `imsOrgId` no cabeçalho da mensagem deve corresponder à definição de entrada. Se a carga da solicitação não incluir um campo `imsOrgId` , o [!DNL Data Collection Core Service] (DCCS) adicionará o campo automaticamente.
- O cabeçalho da mensagem deve referenciar um esquema XDM existente criado na interface do usuário [!DNL Platform].
- O campo `datasetId` precisa fazer referência a um conjunto de dados existente em [!DNL Platform] e seu esquema precisa corresponder ao esquema fornecido no objeto `header` dentro de cada mensagem incluída no corpo da solicitação.

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

A carga de resposta inclui um status para cada mensagem, juntamente com um GUID no `xactionId` que pode ser usado para rastreamento.

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

O exemplo de resposta acima mostra mensagens de erro para a solicitação anterior. Ao comparar essa resposta com a resposta válida anterior, você pode observar que a solicitação resultou em um sucesso parcial, com uma mensagem sendo assimilada com êxito e três mensagens resultando em falha. Observe que ambas as respostas retornam um código de status &quot;207&quot;. Para obter mais informações sobre códigos de status, consulte a tabela [códigos de resposta](#response-codes) no Apêndice deste tutorial.

A primeira mensagem foi enviada com êxito para [!DNL Platform] e não é afetada pelos resultados das outras mensagens. Como resultado, ao tentar reenviar as mensagens com falha, não é necessário reincluir essa mensagem.

A segunda mensagem falhou porque não tinha um corpo de mensagem. A solicitação de coleta espera que os elementos da mensagem tenham seções válidas de cabeçalho e corpo. Adicionar o seguinte código após o cabeçalho na segunda mensagem corrigirá a solicitação, permitindo que a segunda mensagem passe na validação:

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

A terceira mensagem falhou porque uma ID de organização IMS inválida estava sendo usada no cabeçalho. A organização IMS deve corresponder à {CONNECTION_ID} para a qual você está tentando postar. Para determinar qual IMS Organization ID corresponde à conexão de transmissão que você está usando, é possível executar uma solicitação `GET inlet` usando o [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Consulte [recuperando uma conexão de transmissão](./create-streaming-connection.md#get-data-collection-url) para obter um exemplo de como recuperar as conexões de transmissão criadas anteriormente.

A quarta mensagem falhou porque não seguiu o esquema XDM esperado. O `xdmSchema` incluído no cabeçalho e no corpo da solicitação não corresponde ao esquema XDM do `{DATASET_ID}`. A correção do esquema no cabeçalho e no corpo da mensagem permite que ele passe a validação do DCCS e seja enviado com êxito para [!DNL Platform]. O corpo da mensagem também deve ser atualizado para corresponder ao esquema XDM do `{DATASET_ID}` para que ele passe a validação de transmissão em [!DNL Platform]. Para obter mais informações sobre o que acontece com as mensagens que são transmitidas com êxito para a Plataforma, consulte a seção [confirm messages ingested](#confirm-messages-ingested) deste tutorial.

### Recuperar mensagens com falha de [!DNL Platform]

Mensagens com falha são identificadas por um código de status de erro na matriz de resposta.
As mensagens inválidas são coletadas e armazenadas em um lote de &quot;erro&quot; no conjunto de dados especificado por `{DATASET_ID}`.

Leia o guia [recuperando lotes com falha](../quality/retrieve-failed-batches.md) para obter mais informações sobre a recuperação de mensagens em lote com falha.

## Confirmar mensagens assimiladas

As mensagens que passam pela validação do DCCS são transmitidas para [!DNL Platform]. Em [!DNL Platform], as mensagens em lote são testadas por validação de streaming antes de serem assimiladas no [!DNL Data Lake]. O status dos lotes, seja bem-sucedido ou não, é exibido dentro do conjunto de dados especificado por `{DATASET_ID}`.

Você pode visualizar o status das mensagens em lote que são transmitidas com êxito para [!DNL Platform] usando a [interface do usuário do Experience Platform](https://platform.adobe.com) acessando a guia **[!UICONTROL Datasets]**, clicando no conjunto de dados para o qual você está fazendo streaming e verificando a guia **[!UICONTROL Dataset Activity]**.

As mensagens em lote que passam pela validação do streaming em [!DNL Platform] são assimiladas no [!DNL Data Lake]. As mensagens ficam disponíveis para análise ou exportação.

## Próximas etapas

Agora que você sabe como enviar várias mensagens em uma única solicitação e verificar quando as mensagens são assimiladas com êxito no conjunto de dados de destino, é possível começar a transmitir seus próprios dados para [!DNL Platform]. Para obter uma visão geral de como consultar e recuperar dados assimilados de [!DNL Platform], consulte o guia [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md).

## Apêndice

Esta seção contém informações adicionais para o tutorial.

### Códigos de resposta

A tabela a seguir mostra os códigos de status retornados por mensagens de resposta bem-sucedidas e com falha.

| Código de status | Descrição |
| :---: | --- |
| 207 | Embora &#39;207&#39; seja usado como o código de status de resposta geral, o recipient precisa consultar o conteúdo do corpo de resposta de vários status para obter mais informações sobre o sucesso ou a falha da execução do método. O código de resposta é usado em situações de sucesso, sucesso parcial e também em situações de falha. |
| 400 | Houve um problema com o pedido. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, falta de campos obrigatórios na carga da mensagem ou o formato xdm da mensagem era desconhecido). |
| 401° | Não autorizado: solicitação sem cabeçalho de autorização válido. Isso é retornado somente para entradas que têm autenticação ativada. |
| 403 | Não autorizado:  O token de autorização fornecido é inválido ou está expirado. Isso é retornado somente para entradas que têm autenticação ativada. |
| 413 | Carga muito grande - lançada quando a solicitação de carga total é maior que 1MB. |
| 429 | Demasiadas solicitações dentro de uma duração de tempo especificada. |
| 500 | Erro ao processar carga. Consulte o corpo da resposta para obter uma mensagem de erro mais específica (por exemplo, o esquema de carga da mensagem não foi especificado ou não correspondeu à definição XDM em [!DNL Platform]). |
| 503 | O serviço não está disponível no momento. Os clientes devem tentar novamente pelo menos 3 vezes usando uma estratégia de back-off exponencial. |
