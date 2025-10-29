---
description: Saiba como usar a API de teste de destino para testar se o destino de transmissão está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.
title: Teste seu destino de streaming com perfis de amostra
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---


# Teste seu destino de streaming com perfis de amostra {#template-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

Esta página lista e descreve todas as operações de API que você pode executar usando o ponto de extremidade de API `/authoring/testing/destinationInstance/` para testar se o destino está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado. Para obter uma descrição da funcionalidade com suporte neste ponto de extremidade, leia [Testar a configuração de destino](streaming-destination-testing-overview.md).

Você faz solicitações ao endpoint de teste com ou sem adicionar perfis à chamada. Se você não enviar nenhum perfil na solicitação, o Adobe os gerará internamente e os adicionará à solicitação.

Você pode usar a [Amostra da API de geração de perfil](sample-profile-generation-api.md) para criar perfis a serem usados em solicitações para a API de teste de destino.

## Como obter a ID da instância de destino {#get-destination-instance-id}

>[!IMPORTANT]
>
>* Para usar essa API, é necessário ter uma conexão existente com o destino na interface do usuário do Experience Platform. Leia [conectar ao destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) e [ativar perfis e públicos a um destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) para obter mais informações.
>* Depois de estabelecer a conexão com seu destino, obtenha a ID da instância de destino que você deve usar em chamadas de API para este ponto de extremidade ao [navegar em uma conexão com seu destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>  &#x200B;>![Imagem da interface do usuário para obter a ID da instância de destino](../../assets/testing-api/get-destination-instance-id.png)

## Introdução às operações de API de teste de destino {#get-started}

Antes de continuar, consulte o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Testar a configuração de destino sem adicionar perfis à chamada {#test-without-adding-profiles}

Você pode testar a configuração de destino fazendo uma solicitação POST para o ponto de extremidade `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornecendo a ID da instância de destino do destino que você está testando.

**Formato da API**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parâmetro da consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino do destino que você está testando. |

**Solicitação**

A solicitação a seguir chama o ponto de extremidade da API REST do destino. A solicitação é configurada pelo parâmetro de consulta `{DESTINATION_INSTANCE_ID}`.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com a resposta da API do ponto de acesso da API REST do destino.

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
| `aggregationKey` | Inclui informações sobre a política de agregação configurada para o destino. Para obter mais informações, leia a documentação da [Política de agregação](../../functionality/destination-configuration/aggregation-policy.md). |
| `traceId` | Um identificador exclusivo para a operação. Ao encontrar erros, é possível compartilhar essa ID com a equipe do Adobe para fins de solução de problemas. |
| `results.httpCalls.request` | Inclui a solicitação enviada pelo Adobe para o seu destino. |
| `results.httpCalls.response` | Inclui a resposta recebida pelo Adobe do seu destino. |
| `inputProfiles` | Inclui os perfis que foram exportados na chamada para o seu destino. Os perfis correspondem ao esquema de origem. |

{style="table-layout:auto"}

## Testar a configuração de destino com perfis adicionados à chamada {#test-with-added-profiles}

Você pode testar a configuração de destino fazendo uma solicitação POST para o ponto de extremidade `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` e fornecendo a ID da instância de destino do destino que você está testando.

**Formato da API**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| Parâmetro da consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino do destino que você está testando. |

**Solicitação**

A solicitação a seguir chama o ponto de extremidade da API REST do destino. A solicitação é configurada pelos parâmetros fornecidos na carga e no parâmetro de consulta `{DESTINATION_INSTANCE_ID}`.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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

Uma resposta bem-sucedida retorna o status HTTP 200 junto com a resposta da API do ponto de acesso da API REST do destino.

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

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, você sabe como testar seu destino. Agora você pode usar o [processo de documentação de autoatendimento](../../docs-framework/documentation-instructions.md) do Adobe para criar uma página de documentação para o seu destino.
