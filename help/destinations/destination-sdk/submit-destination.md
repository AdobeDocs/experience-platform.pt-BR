---
description: Esta página fornece todas as informações que você precisa enviar para revisar um destino criado com o Destination SDK.
title: Enviar para revisão de um destino criado no Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 7c6d0c8d4d1eea16f13359e9d7a895d767ad3c00
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# Enviar para revisão de um destino criado no Destination SDK

## Visão geral {#overview}

Antes que seu destino possa ser publicado na [Catálogo de destinos Experience Platform](/help/destinations/catalog/overview.md), você deve fornecer ao Adobe determinadas informações sobre o destino e os testes que você realizou, para garantir que os usuários aproveitem a melhor experiência possível ao ativar dados na sua plataforma.

Esta página lista todas as informações que você precisa fornecer ao enviar ou atualizar um destino criado pelo Adobe Experience Platform Destination SDK. Para enviar um destino com êxito no Adobe Experience Platform, envie um email para <aepdestsdk@adobe.com> que inclui:

* Uma descrição dos casos de uso que seu destino resolve. Isso não é necessário se você estiver atualizando uma configuração de destino existente.
* Teste os resultados após usar o ponto de extremidade da API de destino de teste para executar uma chamada HTTP para o seu destino. Compartilhe com o Adobe:
   * Uma chamada de API feita para o terminal de destino.
   * A resposta da API recebida do terminal de destino.
* Prova de que você enviou uma solicitação de publicação de destino para seu destino usando o [API de publicação de destino](./destination-publish-api.md).
* (Somente para integrações produzidas) uma PR de documentação (solicitação de pull), seguindo as instruções descritas na [processo de documentação de autoatendimento](./docs-framework/documentation-instructions.md).
* Um arquivo de imagem que será exibido como um logotipo para seu cartão de destino no catálogo de destinos do Experience Platform.

>[!IMPORTANT]
>
>* O tempo de resposta da publicação do Adobe é de cinco dias úteis.
>
>* Se a equipe do Adobe solicitar que você faça atualizações em suas configurações após o envio inicial, é necessário enviar outra solicitação de publicação de destino depois de fazer as atualizações.
>
>* Mesmo depois que seu destino estiver no catálogo de Experience Platform, se precisar fazer atualizações em suas configurações, envie uma nova solicitação de publicação de destino para que as atualizações sejam refletidas nas configurações.


Você pode encontrar informações detalhadas sobre cada item nas seções abaixo:

## Descrição do caso de uso

Forneça uma descrição dos casos de uso que seu destino resolve para os clientes do Experience Platform. Suas descrições podem ser semelhantes aos casos de uso de parceiros existentes:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): As APIs DataX estão disponíveis para anunciantes que desejam direcionar um grupo de público-alvo específico desconectado de endereços de email no Verizon Media (VMG) podem criar rapidamente um novo segmento e encaminhar o grupo de público-alvo desejado usando a API quase em tempo real do VMG.

## Resultados dos testes após usar a API de destino de teste

Forneça os resultados do teste depois de usar a variável [testar API de destino](./test-destination.md) endpoint para executar uma chamada HTTP para o destino. Isso inclui:

* A solicitação completa da API (cabeçalhos e corpo) feita para o endpoint de destino, usando a API de teste.
* A resposta da API recebida do terminal de destino.

Por exemplo, sua solicitação e resposta podem ser semelhantes às amostras abaixo:

**Solicitação**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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

**Resposta**

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

## Prova de que você enviou uma solicitação de publicação de destino

Depois de testar seu destino com sucesso, você deve usar a variável [API de publicação de destino](./destination-publish-api.md) para enviar o destino ao Adobe para revisão e publicação.

Forneça a ID da solicitação de publicação para o seu destino. Para obter informações sobre como recuperar a ID da solicitação de publicação, leia [Listar solicitações de publicação de destino](./destination-publish-api.md#retrieve-list).

## PR da documentação de destino (solicitação de pull) para integrações produzidas

Se você for um Fornecedor Independente de Software (ISV) ou um Integrador de Sistema (SI) criando um [integração produzida](./overview.md#productized-custom-integrations), use o [processo de documentação de autoatendimento](./docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para o seu destino. Como parte do processo de envio, forneça a solicitação de pull (PR) para a documentação de destino.

## Logotipo para o seu destino

O catálogo de destinos inclui um logotipo para cada cartão de destino. No email de envio, inclua uma imagem com o logotipo do destino.

Os requisitos da imagem são:
* **Formato**: `SVG`
* **Tamanho**: menos de 2 MB

## Baixar email de amostra

[Baixar](./assets/sample-email-submit-destination.rtf) um email de amostra com todas as informações que você precisa fornecer ao Adobe.
