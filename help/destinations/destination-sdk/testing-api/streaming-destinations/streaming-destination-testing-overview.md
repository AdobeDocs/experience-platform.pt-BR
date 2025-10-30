---
description: Saiba como usar a API de teste de destino para testar a configuração de destino de transmissão antes de publicá-la.
title: Visão geral da API de teste de destino de streaming
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Visão geral da API de teste de destino de streaming

Como parte do Destination SDK, a Adobe fornece ferramentas de desenvolvedor para ajudá-lo a configurar e testar seu destino. Esta página descreve como testar a configuração de destino. Para obter informações sobre como criar um modelo de transformação de mensagem, leia [Criar e testar um modelo de transformação de mensagem](../../testing-api/streaming-destinations/create-template.md).

Para **testar se o destino está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado**, use a *Ferramenta de teste de destino*. Com essa ferramenta, você pode testar a configuração de destino enviando mensagens para o endpoint da API REST.

Veja abaixo como testar seu destino se encaixa no [fluxo de trabalho de configuração de destino](../../guides/configure-destination-instructions.md) no Destination SDK:

![Gráfico de onde a etapa de teste de destino se encaixa no fluxo de trabalho de configuração de destino](../../assets/testing-api/test-destination-step.png)

## Ferramenta de teste de destino - finalidade e pré-requisitos {#destination-testing-tool}

Use a ferramenta de teste de destino para testar a configuração de destino enviando mensagens para o ponto de extremidade do parceiro fornecido na [configuração do servidor](../../authoring-api/destination-server/create-destination-server.md).

Antes de usar a ferramenta, verifique se você:

* Configure seu destino seguindo as etapas descritas em [workflow de configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) e
* Estabeleça uma conexão com seu destino, conforme detalhado em [Como obter a ID da instância de destino](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

Com essa ferramenta, após configurar seu destino, é possível:

* Testar se o destino está configurado corretamente;
* Verifique a integridade dos fluxos de dados para o destino configurado.

### Como usar {#how-to-use}

>[!NOTE]
>
>Para obter a documentação de referência completa da API, leia [Operações da API de testes de destino](../../testing-api/streaming-destinations/destination-testing-api.md).

Você pode fazer chamadas para o endpoint da API de teste de destino com ou sem adicionar perfis na solicitação.

Se você não adicionar perfis na solicitação, o Adobe os gerará internamente e os adicionará à solicitação. Para gerar perfis a serem usados nesta solicitação, consulte a [Referência da API de geração de perfil de amostra](../../testing-api/streaming-destinations/sample-profile-generation-api.md). Você precisa gerar perfis com base no esquema XDM de origem, conforme mostrado na [referência de API](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). Observe que o esquema de origem é o [esquema de união](../../../../profile/ui/union-schema.md) da sandbox que você está usando.

A resposta contém o resultado do processamento da solicitação de destino. A solicitação inclui três seções principais:

* A solicitação gerada pelo Adobe para o destino.
* A resposta recebida do seu destino.
* A lista de perfis enviada na solicitação, quer os perfis tenham sido [adicionados por você na solicitação](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles), ou gerados pelo Adobe se [o corpo da solicitação de teste de destino estiver vazio](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>O Adobe pode gerar vários pares de solicitação e resposta. Por exemplo, se você enviar 10 perfis para um destino que tenha um valor `maxUsersPerRequest` de 7, haverá uma solicitação com 7 perfis e outra solicitação com 3 perfis.

**Exemplo de solicitação com parâmetro de perfis no corpo**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Exemplo de solicitação sem parâmetro de perfis no corpo**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Exemplo de resposta**

Observe que o conteúdo do parâmetro `results.httpCalls` é específico para sua API REST.

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

Para obter descrições dos parâmetros de solicitação e resposta, consulte [Operações da API de teste de destino](../../testing-api/streaming-destinations/destination-testing-api.md).

## Próximas etapas

Depois de testar seu destino e confirmar que ele está configurado corretamente, use a [API de publicação de destino](../../publishing-api/create-publishing-request.md) para enviar sua configuração ao Adobe para revisão.
