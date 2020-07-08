---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---


# Criar um segmento

Este documento fornece um tutorial para desenvolver, testar, visualizar e salvar uma definição de segmento usando a API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentação.

Para obter informações sobre como criar segmentos usando a interface do usuário, consulte o guia [do Construtor de](../ui/overview.md)segmentos.

## Introdução

Este tutorial requer uma compreensão funcional dos vários serviços de Adobe Experience Platform envolvidos na criação de segmentos de audiência. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [Serviço](../home.md)de segmentação de Adobe Experience Platform: Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da Platform.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para as APIs da Platform, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. Todas as solicitações às APIs do Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Desenvolver uma definição de segmento

A primeira etapa da segmentação é definir um segmento, representado em uma construção chamada definição **de** segmento. Uma definição de segmento é um objeto que encapsula um query gravado em Linguagem de Query do Perfil (PQL). Esse objeto também é chamado de predicado **PQL**. Os predicados de PQL definem as regras para o segmento com base nas condições relacionadas a qualquer registro ou série de tempo que você fornece ao Perfil do cliente em tempo real. Consulte o guia [](../pql/overview.md) PQL para obter mais informações sobre como escrever query PQL.

Você pode criar uma nova definição de segmento, fazendo uma solicitação POST para o `/segment/definitions` terminal na API do Perfil do cliente em tempo real. O exemplo a seguir descreve como formatar uma solicitação de definição, incluindo quais informações são necessárias para que um segmento seja definido com sucesso.

As definições de segmentos podem ser avaliadas de duas formas: segmentação em lote e segmentação em streaming. A segmentação em lote avalia os segmentos com base em uma programação predefinida ou quando a avaliação é acionada manualmente, enquanto a segmentação em streaming avalia os segmentos assim que os dados são ingeridos no Platform. Este tutorial usará a segmentação **em** lote. Para obter mais informações sobre a segmentação de streaming, leia a [visão geral da segmentação](../api/streaming-segmentation.md)de streaming.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

A solicitação a seguir cria uma nova definição de segmento para um schema chamado &quot;MyProfile&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Propriedade | Descrição |
| --------- | ------------ | 
| `name` | **Obrigatório.** Um nome exclusivo pelo qual fazer referência ao segmento. |
| `schema` | **Obrigatório.** O schema associado às entidades no segmento. Consiste em um campo `id` ou `name` . |
| `expression` | **Obrigatório.** Uma entidade que contém informações de campos sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, apenas &quot;PQL&quot; é suportado. |
| `expression.format` | Indica a estrutura da expressão no valor. Atualmente, o formato a seguir é compatível: <ul><li>`pql/text`: Uma representação textual de uma definição de segmento, de acordo com a gramática PQL publicada.  Por exemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Uma expressão que esteja em conformidade com o tipo indicado em `expression.format`. |
| `mergePolicyId` | O identificador da política de mesclagem a ser usada para os dados exportados. Para obter mais informações, leia o documento [de configuração da política de](../../profile/api/merge-policies.md)mesclagem. |
| `description` | Uma descrição legível da definição. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento recém-criada, incluindo sua somente leitura gerada pelo sistema, `id` que será usada posteriormente neste tutorial.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Estimativa e pré-visualização de uma audiência {#estimate-and-preview-an-audience}

À medida que você desenvolve sua definição de segmento, você pode usar as ferramentas de estimativa e pré-visualização no Perfil do cliente em tempo real para visualização de informações de nível de resumo, para ajudar a garantir que você esteja isolando a audiência esperada. As estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho da audiência projetada e o intervalo de confiança. As Pré-visualizações fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o esperado.

Ao estimar e visualizar sua audiência, você pode testar e otimizar seus predicados de PQL até que produzam um resultado desejável, onde eles poderão ser usados em uma definição de segmento atualizada.

Há duas etapas necessárias para pré-visualização ou obter uma estimativa do seu segmento:

1. [Criar um trabalho de pré-visualização](#create-a-preview-job)
2. [Estimativa de Visualização ou pré-visualização](#view-an-estimate-or-preview) usando a ID do trabalho de pré-visualização

### Como as estimativas são geradas

As amostras de dados são usadas para avaliar segmentos e estimar o número de perfis qualificados. Novos dados são carregados na memória todas as manhãs (entre 12AM-2AM PT, que é 7-9AM UTC), e todos os query de segmentação são estimados usando os dados de amostra desse dia. Consequentemente, quaisquer novos campos adicionados ou dados adicionais recolhidos serão refletidos nas estimativas do dia seguinte.

O tamanho da amostra depende do número total de entidades na loja de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto completo de dados |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

As estimativas geralmente são executadas de 10 a 15 segundos, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

### Criar um trabalho de pré-visualização

Você pode criar um novo trabalho de pré-visualização fazendo uma solicitação POST para o `/preview` terminal.

**Formato da API**

```http
POST /preview
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de pré-visualização. O corpo da solicitação contém as informações do query relacionadas ao segmento.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `predicateExpression` | A expressão PQL para query dos dados. |
| `predicateModel` | O nome do schema XDM no qual os dados do Perfil se baseiam. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do trabalho de pré-visualização recém-criado, incluindo sua ID e o estado de processamento atual.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `state` | O estado atual do trabalho de pré-visualização. Estará no estado &quot;EM EXECUÇÃO&quot; até que o processamento seja concluído, e nesse momento ele se tornará &quot;RESULT_READY&quot; ou &quot;FALHA&quot;. |
| `previewId` | A ID da tarefa de pré-visualização, a ser usada para fins de pesquisa ao visualizar uma estimativa ou pré-visualização, conforme descrito na seção a seguir. |

### Visualização de uma estimativa ou pré-visualização

Os processos de estimativa e pré-visualização são executados de forma assíncrona, pois query diferentes podem demorar tempos diferentes para serem concluídos. Depois que um query é iniciado, você pode usar chamadas de API para recuperar (GET) o estado atual da estimativa ou pré-visualização à medida que ela avança.

Usando a API Perfil do cliente em tempo real, você pode pesquisar o estado atual de uma tarefa de pré-visualização pela ID. Se o estado for &quot;RESULT_READY&quot;, você poderá visualização os resultados. Dependendo de se você deseja visualização uma estimativa ou uma pré-visualização, cada uma tem seu próprio terminal na API. Os exemplos para ambos são fornecidos abaixo.

### Visualização de uma estimativa

**Formato da API**

```http
GET /estimate/{PREVIEW_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{PREVIEW_ID}` | A ID do trabalho de pré-visualização que você deseja visualização. |

**Solicitação**

A solicitação a seguir recupera uma estimativa, usando a `previewId` criada na etapa anterior.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da estimativa.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `state` | O estado atual do trabalho de pré-visualização. Será &quot;EM EXECUÇÃO&quot; até que o processamento seja concluído, e nesse momento ele se tornará &quot;RESULT_READY&quot; ou &quot;FALHA&quot;. |
| `_links.preview` | Quando o estado atual da tarefa de pré-visualização é &quot;RESULT_READY&quot;, este atributo fornece um URL para visualização da estimativa. |

### Visualização de uma pré-visualização

**Formato da API**

```http
GET /preview/{PREVIEW_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{PREVIEW_ID}` | A ID do trabalho de pré-visualização que você deseja visualização. |

**Solicitação**

A solicitação a seguir recupera uma pré-visualização usando a `previewId` criada na etapa anterior.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna detalhes da pré-visualização.

```json
{
   "results": [{
         "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
               "XID_COOKIE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
               },
               "XID_PROFILE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
               }
            }
         }
      },
      {
         "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
               "XID_COOKIE_ID_2-1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

               },
               "XID_PROFILE_ID_2": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
               }
            }
         },
         "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Próximas etapas

Depois de desenvolver, testar e salvar sua definição de segmento, você pode criar um trabalho de segmento para criar uma audiência usando a API de Perfil do cliente em tempo real. Consulte o tutorial sobre como [avaliar e acessar os resultados](./evaluate-a-segment.md) do segmento para obter etapas detalhadas sobre como fazer isso.