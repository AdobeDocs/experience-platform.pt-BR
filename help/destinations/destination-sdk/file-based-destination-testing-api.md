---
description: Esta página explica como usar o endpoint da API /testing/destinationInstance para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.
title: Teste seu destino baseado em arquivo com perfis de amostra
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 2%

---


# Teste seu destino baseado em arquivo com perfis de amostra

## Visão geral {#overview}

Esta página explica como usar a variável `/testing/destinationInstance` Ponto de extremidade de API para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.

Você pode fazer solicitações ao endpoint de teste com ou sem adicionar [perfis de amostra](file-based-sample-profile-generation-api.md) à chamada . Se você não enviar perfis na solicitação, a API gera um perfil de amostra automaticamente e o adiciona à solicitação.

Os perfis de amostra gerados automaticamente contêm dados genéricos. Se quiser testar seu destino com dados de perfil personalizados e mais intuitivos, use a [exemplo de API de geração de perfil](file-based-sample-profile-generation-api.md) para gerar um perfil de amostra, personalize sua resposta e inclua-a na solicitação para o `/testing/destinationInstance` endpoint .

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de usar a variável `/testing/destinationInstance` , certifique-se de atender às seguintes condições:

* Você tem um destino com base em arquivo existente criado por meio do Destination SDK e pode vê-lo em seu [catálogo de destinos](../ui/destinations-workspace.md).
* Você criou pelo menos um fluxo de ativação para o seu destino na interface do usuário do Experience Platform.
* Para fazer a solicitação da API com êxito, é necessário a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, do URL, ao navegar em uma conexão com seu destino na interface do usuário da plataforma.

   ![Imagem da interface do usuário que mostra como obter a ID da instância de destino do URL.](assets/get-destination-instance-id.png)
* *Opcional*: Se você quiser testar a configuração de destino com um perfil de amostra adicionado à chamada da API, use a variável [/sample-profiles](file-based-sample-profile-generation-api.md) endpoint para gerar um perfil de amostra com base no esquema de origem existente. Se você não fornecer um perfil de amostra, a API gerará um e o retornará na resposta.

## Teste a configuração de destino sem adicionar perfis à chamada {#test-without-adding-profiles}

**Formato da API**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Solicitação**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Parâmetros de caminho | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino para a qual você está gerando perfis de amostra. Consulte a [pré-requisitos](#prerequisites) para obter detalhes sobre como obter essa ID. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com a carga da resposta.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"crmid-P1A7l"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string",
               "lastName":"string"
            }
         }
      }
   ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `activations` | Retorna a ID do segmento e a ID da execução do fluxo para cada segmento ativado. O número de entradas de ativação (e arquivos gerados associados) é igual ao número de segmentos mapeados na instância de destino. <br><br> Exemplo: Se você mapeou dois segmentos para a instância de destino, a variável `activations` matriz conterá duas entradas. Cada segmento ativado corresponderá a um arquivo exportado. |
| `results` | Retorna a ID da instância de destino e as IDs de execução de fluxo que você pode usar para chamar a função [API de resultados](file-based-destination-results-api.md), para testar ainda mais a integração. |
| `inputProfiles` | Retorna os perfis de amostra gerados automaticamente pela API. |

{style=&quot;table-layout:auto&quot;}

## Teste a configuração de destino com perfis adicionados à chamada {#test-with-added-profiles}

Para testar seu destino com dados de perfil personalizados e mais intuitivos, você pode personalizar a resposta obtida do [/sample-profiles](file-based-sample-profile-generation-api.md) endpoint com valores de sua escolha e inclua o perfil personalizado na solicitação para o `/testing/destinationInstance` endpoint .

**Formato da API**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Solicitação**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Parâmetro | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino do destino que você está testando.  A ID da instância de destino para a qual você está gerando perfis de amostra. Consulte a [pré-requisitos](#prerequisites) para obter detalhes sobre como obter essa ID. |
| `profiles` | Matriz que pode incluir um ou vários perfis. Use o [exemplo de endpoint da API de perfil](file-based-sample-profile-generation-api.md) para gerar perfis para usar nesta chamada de API. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com a carga da resposta.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `activations` | Retorna a ID do segmento e a ID da execução do fluxo para cada segmento ativado. O número de entradas de ativação (e arquivos gerados associados) é igual ao número de segmentos mapeados na instância de destino. <br><br> Exemplo: Se você mapeou dois segmentos para a instância de destino, a variável `activations` matriz conterá duas entradas. Cada segmento ativado corresponderá a um arquivo exportado. |
| `results` | Retorna a ID da instância de destino e as IDs de execução de fluxo que você pode usar para chamar a função [API de resultados](file-based-destination-results-api.md), para testar ainda mais a integração. |
| `inputProfiles` | Retorna os perfis de amostra personalizados transmitidos na solicitação de API. |

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Após a leitura deste documento, você agora sabe como testar sua configuração de destino baseada em arquivo.

Se você recebeu uma resposta de API válida, seu destino está funcionando corretamente. Se você quiser ver informações mais detalhadas sobre o seu fluxo de ativação, poderá usar a variável `results` propriedade da resposta para [exibir resultados detalhados de ativação](file-based-destination-results-api.md).

Se estiver criando um destino público, agora é possível [enviar sua configuração de destino](../destination-sdk/submit-destination.md) para Adobe para revisão.