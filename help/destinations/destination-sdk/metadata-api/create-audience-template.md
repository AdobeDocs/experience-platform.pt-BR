---
description: Esta página exemplifica a chamada da API usada para criar um modelo de público-alvo por meio do Adobe Experience Platform Destination SDK.
title: Criar um modelo de público-alvo
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 4%

---


# Criar um modelo de público-alvo

>[!IMPORTANT]
>
>**Ponto de acesso da API**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Para alguns destinos criados com o Destination SDK, é necessário criar uma configuração de metadados de público-alvo para criar, atualizar ou excluir metadados de segmento de maneira programática no destino. Esta página mostra como usar o `/authoring/audience-templates` Ponto de extremidade da API para criar a configuração.

Para obter uma descrição detalhada dos recursos que podem ser configurados por meio desse terminal, consulte [gerenciamento de metadados do público-alvo](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Introdução às operações da API do modelo de público-alvo {#get-started}

Antes de continuar, reveja o [guia de introdução](../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Criar um modelo de público-alvo {#create}

Você pode criar um novo modelo de público-alvo criando um `POST` à `/authoring/audience-templates` endpoint .

**Formato da API**

```http
POST /authoring/audience-templates
```

+++Solicitação

A solicitação a seguir cria um novo modelo de público-alvo, configurado pelos parâmetros fornecidos no payload. A carga abaixo inclui todos os parâmetros aceitos pela `/authoring/audience-templates` endpoint . Observe que não é necessário adicionar todos os parâmetros na chamada do e que o modelo é personalizável, de acordo com os requisitos da API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Propriedade | Tipo | Descrição |
| -------- | ----------- | ----------- |
| `name` | String | O nome do modelo de metadados do público-alvo para o seu destino. Esse nome aparecerá em qualquer mensagem de erro específica do parceiro na interface do usuário do Experience Platform, seguido da mensagem de erro analisada em `metadataTemplate.create.errorSchemaMap`. |
| `url` | String | O URL e o terminal da API, usado para criar, atualizar, excluir ou validar públicos/segmentos na plataforma. Dois exemplos do setor são: `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` e `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | String | O método usado no terminal para criar, atualizar, excluir ou validar programaticamente o segmento/público-alvo no destino. Por exemplo: `POST`, `PUT`, `DELETE` |
| `headers.header` | String | Especifica todos os cabeçalhos HTTP que devem ser adicionados à chamada para sua API. Por exemplo, `"Content-Type"` |
| `headers.value` | String | Especifica o valor dos cabeçalhos HTTP que devem ser adicionados à chamada para sua API. Por exemplo, `"application/x-www-form-urlencoded"` |
| `requestBody` | String | Especifica o conteúdo do corpo da mensagem que deve ser enviado para sua API. Os parâmetros que devem ser adicionados à variável `requestBody` dependem dos campos aceitos pela API. Para obter um exemplo, consulte a [primeiro exemplo de modelo](../functionality/audience-metadata-management.md#example-1) no documento de funcionalidade Metadados de público-alvo . |
| `responseFields.name` | String | Especifique quaisquer campos de resposta que sua API retorne quando chamada. Para obter um exemplo, consulte a [exemplos de modelo](../functionality/audience-metadata-management.md#examples) no documento de funcionalidade Metadados de público-alvo . |
| `responseFields.value` | String | Especifique o valor de qualquer campo de resposta que sua API retorna quando chamada. |
| `responseErrorFields.name` | String | Especifique quaisquer campos de resposta que sua API retorne quando chamada. Para obter um exemplo, consulte a [ exemplos de modelo](../functionality/audience-metadata-management.md#examples) no documento de funcionalidade Metadados de público-alvo . |
| `responseErrorFields.value` | String | Analisa todas as mensagens de erro retornadas nas respostas de chamada da API do seu destino. Essas mensagens de erro serão exibidas para os usuários na interface do usuário do Experience Platform. |
| `validations.field` | String | Indica se as validações devem ser executadas para qualquer campo antes que as chamadas de API sejam feitas ao seu destino. Por exemplo, você pode usar `{{validations.accountId}}` para validar a ID da conta do usuário. |
| `validations.regex` | String | Indica como o campo deve ser estruturado para que a validação seja aprovada. |

{style="table-layout:auto"}

+++

+++Resposta

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do modelo de público-alvo recém-criado.

+++

## Tratamento de erros da API

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe quando usar modelos de público-alvo e como configurar um modelo de público-alvo usando o `/authoring/audience-templates` Ponto de extremidade da API. Ler [como usar o Destination SDK para configurar seu destino](../guides/configure-destination-instructions.md) para entender onde essa etapa se encaixa no processo de configuração do seu destino.
