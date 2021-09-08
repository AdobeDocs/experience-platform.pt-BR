---
description: Esta página lista e descreve todas as operações da API que podem ser realizadas usando o endpoint da API `/authoring/testing/destinationInstance/`, para testar se o destino está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.
title: Operações da API de teste de destino
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 2%

---

# Operações da API de teste de destino {#template-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade** da API:  `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Esta página lista e descreve todas as operações de API que podem ser executadas usando o endpoint da API `/authoring/testing/destinationInstance/`, para testar se o destino está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado. Para obter uma descrição da funcionalidade suportada por este ponto de extremidade, leia [Testar sua configuração de destino](./test-destination.md).

Você faz solicitações ao endpoint de teste com ou sem adicionar perfis à chamada. Se você não enviar perfis na solicitação, o Adobe gerará esses perfis internamente para você e os adicionará à solicitação.

Você pode usar a [Amostra da API de geração de perfil](./sample-profile-generation-api.md) para criar perfis para usar em solicitações para a API de teste de destino.

>[!IMPORTANT]
>
>* Para usar essa API, você deve ter uma conexão existente com seu destino na interface do usuário do Experience Platform. Leia [conectar ao destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) e [ativar perfis e segmentos para um destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) para obter mais informações. Depois de estabelecer a conexão com seu destino, obtenha a ID da instância de destino que você deve usar em chamadas de API para esse terminal a partir do URL ao [navegar em uma conexão com seu destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![Imagem da interface do usuário como obter a ID da instância de destino](./assets/get-destination-instance-id.png)


## Introdução às operações da API de teste de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com êxito, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Teste a configuração de destino sem adicionar perfis à chamada {#test-without-adding-profiles}

Você pode testar a configuração de destino fazendo uma solicitação POST para o endpoint `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornecendo a ID da instância de destino do destino que está testando.

**Formato da API**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parâmetro de consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino do destino que você está testando. |

**Solicitação**

A solicitação a seguir chama o ponto de extremidade da API REST do seu destino. A solicitação é configurada pelo parâmetro de consulta `{DESTINATION_INSTANCE_ID}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com a resposta da API do ponto de extremidade da API REST de seu destino.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `aggregationKey` | Inclui informações sobre a política de agregação configurada para o destino. Para obter mais informações, leia a seção [Aggregation policy](./destination-configuration.md#aggregation) no documento de configuração de destino. |
| `traceId` | Um identificador exclusivo para a operação. Ao encontrar erros, você pode compartilhar essa ID com a equipe do Adobe para fins de solução de problemas. |
| `results.httpCalls.request` | Inclui a solicitação que foi enviada pelo Adobe para o seu destino. |
| `results.httpCalls.response` | Inclui a resposta recebida pelo Adobe de seu destino. |
| `inputProfiles` | Inclui os perfis que foram exportados na chamada para seu destino. Os perfis correspondem ao esquema de origem. |


## Teste a configuração de destino com perfis adicionados à chamada {#test-with-added-profiles}

Você pode testar a configuração de destino fazendo uma solicitação POST para o endpoint `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornecendo a ID da instância de destino do destino que está testando.

**Formato da API**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parâmetro de consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino do destino que você está testando. |

**Solicitação**

A solicitação a seguir chama o ponto de extremidade da API REST do seu destino. A solicitação é configurada pelos parâmetros fornecidos no payload e no parâmetro de consulta `{DESTINATION_INSTANCE_ID}` .

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 juntamente com a resposta da API do ponto de extremidade da API REST de seu destino.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do SDK de destino seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) e [erros do cabeçalho da solicitação](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe como testar seu destino. Agora você pode usar o Adobe [self-service documentation process](./docs-framework/documentation-instructions.md) para criar uma página de documentação para seu destino.