---
description: Esta página fornece todas as informações necessárias para enviar um destino produzido para revisão quando criado usando o Destination SDK.
title: Enviar um destino produzido para revisão
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# Enviar um destino produzido para revisão

## Visão geral {#overview}

>[!IMPORTANT]
>
>* O processo documentado aqui só é necessário para parceiros que enviam destinos (públicos) produzidos. Se você estiver criando um destino privado para seu próprio uso, não será necessário produzir e compartilhar esses materiais com a Adobe.
>
>* O tempo de resposta padrão da Adobe para revisar solicitações de publicação de destino é de cinco dias úteis.
>
>* Se a equipe do Adobe solicitar que você faça atualizações em suas configurações após o envio inicial, será necessário enviar outra solicitação de publicação de destino depois de fazer as atualizações.
>
>* Mesmo depois que o destino estiver ativo no catálogo do Experience Platform, se precisar fazer atualizações nas configurações, você deverá enviar uma nova solicitação de publicação de destino para que as atualizações sejam refletidas nas configurações.
>
>* A linha do tempo de revisão e os artefatos necessários são os mesmos para novos destinos e destinos existentes que você está atualizando.

Antes de publicar seu destino no [catálogo de destinos do Experience Platform](/help/destinations/catalog/overview.md), forneça à Adobe determinadas informações sobre o destino e os testes que você realizou, para garantir que os usuários desfrutem da melhor experiência possível ao ativar dados para sua plataforma.

Esta página lista todas as informações que você precisa fornecer ao enviar ou atualizar um destino criado usando o Adobe Experience Platform Destination SDK. Para enviar um destino no Adobe Experience Platform com êxito, envie um email para <aepdestsdk@adobe.com> que inclua:

* Uma descrição dos casos de uso que seu destino resolve. Isso só será necessário se você estiver enviando uma nova configuração de destino.
* Uma descrição do motivo para o envio do seu destino. Isso só será necessário se você estiver atualizando uma configuração de destino existente.
* Teste os resultados após usar o endpoint da API de destino de teste para executar uma chamada HTTP no destino. Compartilhe com a Adobe uma chamada de API feita para o terminal de destino e a resposta da API recebida do terminal.
* Uma gravação de tela que mostra a experiência do usuário para alguém se conectar ao seu destino e prosseguir com as etapas de ativação.
* Requisitos adicionais para destinos baseados em arquivo:
   * Compartilhe uma solicitação e uma amostra de resposta após usar a API de teste para [testar seu destino baseado em arquivo com perfis de amostra](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Anexe um arquivo de amostra gerado pelo destino e exportado para o local de armazenamento.
   * Envie alguma forma de prova de que você assimilou com êxito o arquivo exportado do local de armazenamento no sistema.
* Prova de que você enviou uma solicitação de publicação de destino para o seu destino usando a [API de publicação de destino](../publishing-api/create-publishing-request.md).
* Uma PR (solicitação de pull) de documentação, seguindo as instruções descritas no [processo de documentação de autoatendimento](../docs-framework/documentation-instructions.md).
* Um arquivo de imagem que será exibido como um logotipo para seu cartão de destino no catálogo de destinos do Experience Platform.

Você pode encontrar informações detalhadas sobre cada item nas seções abaixo:

## Descrição do caso de uso {#use-case-description}

Forneça uma descrição dos casos de uso que seu destino resolve para os clientes do Experience Platform. Suas descrições podem ser semelhantes aos casos de uso de parceiros existentes:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): crie públicos-alvo a partir de suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): as APIs DataX estão disponíveis para anunciantes que desejam direcionar um grupo de público-alvo específico digitado de endereços de email na Verizon Media (VMG). Elas podem criar rapidamente um novo público-alvo e enviar por push o grupo de público-alvo desejado usando a API quase em tempo real do VMG.

## Motivo da atualização {#reason-for-update}

>[!NOTE]
>
>Esta seção só é necessária ao atualizar uma configuração existente.

Forneça uma breve descrição do problema que seu envio resolve para o destino existente. Por exemplo, seu envio pode atualizar o nome, a descrição e o logotipo do seu destino conforme você muda da versão beta para a disponível geral. Ou o envio pode corrigir um erro descoberto na configuração de destino.

## Resultados do teste após usar a API de destino de teste {#testing-api-response}

Forneça resultados de teste após usar o ponto de extremidade da [API de destino de teste](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) para executar uma chamada HTTP para o seu destino. Isso inclui:

* A solicitação completa da API (cabeçalhos e corpo) feita para o endpoint de destino usando a API de teste.
* A resposta da API recebida do endpoint de destino.

Por exemplo, sua solicitação e resposta podem ser semelhantes às amostras abaixo:

**Solicitação**

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

## Requisitos adicionais para destinos baseados em arquivo {#additional-file-based-destination-requirements}

Para destinos baseados em arquivo, você deve fornecer prova adicional de que configurou corretamente o destino. Certifique-se de incluir os itens abaixo:

### Teste de resposta da API {#testing-api-response-file-based}

Inclua uma solicitação e uma amostra de resposta após usar a API de teste para [testar seu destino baseado em arquivo com perfis de amostra](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Anexar arquivo exportado {#attach-exported-file}

No seu [email de envio](#download-sample-email), anexe um arquivo CSV que foi exportado para o local de armazenamento pelo destino que você configurou.

### Prova de assimilação bem-sucedida {#proof-of-successful-ingestion}

Por fim, você deve fornecer alguma forma de prova de que os dados foram assimilados com êxito em seu sistema após serem exportados para o local de armazenamento fornecido. Forneça qualquer um dos itens abaixo:

* Capturas de tela ou um breve vídeo de captura de tela, em que você obtém o arquivo manualmente do local de armazenamento e o assimila no sistema.
* Capturas de tela ou um breve vídeo de captura de tela em que a interface do usuário do sistema confirma que o nome de arquivo gerado pelo Experience Platform foi assimilado com êxito no sistema.
* Registra linhas do seu sistema que o Adobe pode correlacionar com o nome do arquivo ou com os dados gerados a partir do Experience Platform.

## Prova de que você enviou uma solicitação de publicação de destino {#destination-publishing-request-proof}

Depois de testar o destino com êxito, você deve usar a [API de publicação de destino](../publishing-api/create-publishing-request.md) para enviar o destino ao Adobe para revisão e publicação.

Forneça a ID da solicitação de publicação para o destino. Para obter informações sobre como recuperar a ID da solicitação de publicação, leia como [recuperar solicitações de publicação de destino](../publishing-api/retrieve-publishing-request.md).

## PR (pull request) da documentação de destino para integrações produzidas {#documentation-pr}

Se você for um ISV (Fornecedor Independente de Software) ou um SI (Integrador de Sistemas) criando uma [integração de produtos](../overview.md#productized-custom-integrations), deverá usar o [processo de documentação de autoatendimento](../docs-framework/documentation-instructions.md) para criar uma página de documentação do produto para o seu destino. Como parte do processo de envio, forneça a solicitação de pull (PR) para sua documentação de destino.

## Logotipo para o seu destino {#logo}

O catálogo de destinos inclui um logotipo para cada cartão de destino. No email de envio, inclua uma imagem com o logotipo do seu destino.

Os requisitos de imagem são:

* **Formato**: `SVG`
* **Tamanho**: menos de 2 MB

## Baixar email de amostra {#download-sample-email}

[Baixe](../assets/guides/sample-email-submit-destination.rtf) um email de exemplo com todas as informações que você precisa fornecer à Adobe.
