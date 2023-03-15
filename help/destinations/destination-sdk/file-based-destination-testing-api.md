---
description: Esta página explica como usar o endpoint da API /testing/destinationInstance para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.
title: Teste seu destino baseado em arquivo com perfis de amostra
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# Teste seu destino baseado em arquivo com perfis de amostra

## Visão geral {#overview}

Esta página explica como usar a variável `/testing/destinationInstance` Endpoint da API para testar se o destino baseado em arquivo está configurado corretamente e verificar a integridade dos fluxos de dados para o destino configurado.

Você pode fazer solicitações para o endpoint de teste com ou sem adicionar [perfis de amostra](file-based-sample-profile-generation-api.md) à chamada. Se você não enviar nenhum perfil na solicitação, a API gerará um perfil de amostra automaticamente e o adicionará à solicitação.

Os perfis de amostra gerados automaticamente contêm dados genéricos. Se você quiser testar seu destino com dados de perfil personalizados e mais intuitivos, use o [exemplo de API de geração de perfil](file-based-sample-profile-generation-api.md) para gerar um perfil de amostra, personalize sua resposta e inclua-o na solicitação ao `/testing/destinationInstance` terminal.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de poder usar o `/testing/destinationInstance` verifique se você atende às seguintes condições:

* Você tem um destino baseado em arquivo existente criado por meio do Destination SDK e pode visualizá-lo em seu [catálogo de destinos](../ui/destinations-workspace.md).
* Você criou pelo menos um fluxo de ativação para o destino na interface do usuário do Experience Platform.
* Para fazer a solicitação de API com êxito, é necessário ter a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, no URL, ao navegar por uma conexão com seu destino na interface do Platform.

   ![Imagem da interface mostrando como obter a ID da instância de destino do URL.](assets/get-destination-instance-id.png)
* *Opcional*: se você quiser testar a configuração de destino com uma amostra de perfil adicionada à chamada de API, use o [/sample-profiles](file-based-sample-profile-generation-api.md) endpoint para gerar um perfil de amostra com base no esquema de origem existente. Se você não fornecer um perfil de amostra, a API gerará um e o retornará na resposta.

## Testar a configuração de destino sem adicionar perfis à chamada {#test-without-adding-profiles}

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

Uma resposta bem-sucedida retorna o status HTTP 200 junto com a carga de resposta.

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
| `activations` | Retorna a ID do segmento e a ID de execução do fluxo para cada segmento ativado. O número de entradas de ativação (e arquivos gerados associados) é igual ao número de segmentos mapeados na instância de destino. <br><br> Exemplo: se você mapeou dois segmentos para a instância de destino, a variável `activations` A matriz conterá duas entradas. Cada segmento ativado corresponderá a um arquivo exportado. |
| `results` | Retorna a ID da instância de destino e as IDs de execução de fluxo que você pode usar para chamar a [API de resultados](file-based-destination-results-api.md), para testar ainda mais a integração. |
| `inputProfiles` | Retorna os perfis de amostra gerados automaticamente pela API. |

{style="table-layout:auto"}

## Testar a configuração de destino com perfis adicionados à chamada {#test-with-added-profiles}

Para testar seu destino com dados de perfil personalizados e mais intuitivos, você pode personalizar a resposta obtida no [/sample-profiles](file-based-sample-profile-generation-api.md) com valores de sua escolha e inclua o perfil personalizado na solicitação ao `/testing/destinationInstance` terminal.

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
| `profiles` | Matriz que pode incluir um ou vários perfis. Use o [exemplo de endpoint da API de perfil](file-based-sample-profile-generation-api.md) para gerar perfis que serão usados nesta chamada de API. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 junto com a carga de resposta.

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
| `activations` | Retorna a ID do segmento e a ID de execução do fluxo para cada segmento ativado. O número de entradas de ativação (e arquivos gerados associados) é igual ao número de segmentos mapeados na instância de destino. <br><br> Exemplo: se você mapeou dois segmentos para a instância de destino, a variável `activations` A matriz conterá duas entradas. Cada segmento ativado corresponderá a um arquivo exportado. |
| `results` | Retorna a ID da instância de destino e as IDs de execução de fluxo que você pode usar para chamar a [API de resultados](file-based-destination-results-api.md), para testar ainda mais a integração. |
| `inputProfiles` | Retorna os perfis de amostra personalizados passados na solicitação de API. |

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como testar a configuração de destino baseada em arquivo.

Se você tiver recebido uma resposta de API válida, seu destino está funcionando corretamente. Se quiser ver informações mais detalhadas sobre o fluxo de ativação, use o `results` propriedade da resposta a [exibir resultados de ativação detalhados](file-based-destination-results-api.md).

Se você estiver criando um destino público, poderá [enviar sua configuração de destino](../destination-sdk/submit-destination.md) para Adobe para revisão.
