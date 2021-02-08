---
keywords: Experience Platform;home;popular topics;segmentação;Segmentação;Serviço de segmentação;pré-visualizações;estimativas;pré-visualizações e estimativas;estimativas e pré-visualizações;api;API;
solution: Experience Platform
title: Pontos finais da API de pré-visualizações e estimativas
topic: developer guide
description: À medida que a definição do segmento é desenvolvida, você pode usar as ferramentas de estimativa e pré-visualização no Adobe Experience Platform para visualização de informações de nível de resumo, a fim de ajudar a garantir que você esteja isolando a audiência esperada.
translation-type: tm+mt
source-git-commit: eba6de210dcbc12b829b09ba6e7083d342517ba2
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---


# Pré-visualizações e endpoints de estimativas

À medida que você desenvolve uma definição de segmento, você pode usar as ferramentas de estimativa e pré-visualização no Adobe Experience Platform para visualização de informações de nível de resumo para ajudar a garantir que você esteja isolando a audiência que espera.

* **As** visualizações fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o esperado.

* **As** estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho da audiência projetada, o intervalo de confiança e o desvio padrão do erro.

>[!NOTE]
>
>Para acessar métricas semelhantes relacionadas aos dados do Perfil do cliente em tempo real, como o número total de fragmentos do perfil e perfis mesclados em namespaces específicas ou o armazenamento de dados do Perfil como um todo, consulte o guia de ponto final [pré-visualização (status da amostra da pré-visualização)](../../profile/api/preview-sample-status.md), parte do guia do desenvolvedor da API do Perfil.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas à API com êxito, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Como as estimativas são geradas

Quando a ingestão de registros no repositório de Perfis aumenta ou diminui a contagem total de perfis em mais de 5%, uma tarefa de amostragem é acionada para atualizar a contagem. A forma como a amostragem de dados é acionada depende do método de ingestão:

* **Inclusão em lote:** para ingestão em lote, em 15 minutos após a ingestão bem-sucedida de um lote no repositório de Perfis, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem.
* **Inclusão de transmissão:** Para workflows de dados de transmissão, é feita uma verificação de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi cumprido. Se houver, uma tarefa será acionada automaticamente para atualizar a contagem.

O tamanho da amostra da verificação depende do número geral de entidades na loja de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto completo de dados |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

>[!NOTE]
>
>As estimativas geralmente levam de 10 a 15 segundos para serem executadas, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

## Criar uma nova pré-visualização {#create-preview}

Você pode criar uma nova pré-visualização, fazendo uma solicitação POST para o terminal `/preview`.

>[!NOTE]
>
>Uma tarefa de estimativa é criada automaticamente quando uma tarefa de pré-visualização é criada. Esses dois trabalhos compartilharão a mesma ID.

**Formato da API**

```http
POST /preview
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `predicateExpression` | A expressão PQL para query dos dados. |
| `predicateType` | O tipo de predicado para a expressão do query em `predicateExpression`. Atualmente, o único valor aceito para essa propriedade é `pql/text`. |
| `predicateModel` | O nome da classe de schema [!DNL Experience Data Model] (XDM) na qual os dados do perfil se baseiam. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) com detalhes da sua pré-visualização recém-criada.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `state` | O estado atual do trabalho de pré-visualização. Quando criado, estará no estado &quot;NOVO&quot;. Subsequentemente, ele estará no estado &quot;EM EXECUÇÃO&quot; até a conclusão do processamento, e nesse ponto se tornará &quot;RESULT_READY&quot; ou &quot;FALHA&quot;. |
| `previewId` | A ID da tarefa de pré-visualização, a ser usada para fins de pesquisa ao exibir uma estimativa ou pré-visualização, conforme descrito na próxima seção. |

## Recuperar os resultados de uma pré-visualização específica {#get-preview}

Você pode recuperar informações detalhadas sobre uma pré-visualização específica fazendo uma solicitação de GET para o terminal `/preview` e fornecendo a ID da pré-visualização no caminho da solicitação.

**Formato da API**

```http
GET /preview/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | O valor `previewId` da pré-visualização que você deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre a pré-visualização especificada.

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
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `results` | Uma lista de IDs de entidade, juntamente com suas identidades relacionadas. Os links fornecidos podem ser usados para procurar as entidades especificadas, usando o [terminal da API de acesso ao perfil](../../profile/api/entities.md). |

## Recuperar os resultados de um trabalho de estimativa específico {#get-estimate}

Depois de criar um trabalho de pré-visualização, você pode usar seu `previewId` no caminho de uma solicitação de GET para o terminal `/estimate` para visualização de informações estatísticas sobre a definição do segmento, incluindo tamanho de audiência projetado, intervalo de confiança e desvio padrão do erro.

**Formato da API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | Um trabalho de estimativa só é acionado quando um trabalho de pré-visualização é criado e os dois trabalhos compartilham o mesmo valor de ID para fins de pesquisa. Especificamente, esse é o valor `previewId` retornado quando o trabalho de pré-visualização foi criado. |

**Solicitação**

A solicitação a seguir recupera os resultados de um trabalho de estimativa específico.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do trabalho de estimativa.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | Uma matriz de objetos que mostra o número de perfis dentro do segmento detalhado por namespace de identidade. O número total de perfis por namespace (somando os valores mostrados para cada namespace) pode ser maior que a métrica de contagem de perfis porque um perfil pode estar associado a várias namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, várias namespaces serão associadas a esse cliente individual. |
| `state` | O estado atual do trabalho de pré-visualização. O estado será &quot;EM EXECUÇÃO&quot; até que o processamento seja concluído, e nesse momento ele se tornará &quot;RESULT_READY&quot; ou &quot;FALHA&quot;. |
| `_links.preview` | Quando `state` for &quot;RESULT_READY&quot;, esse campo fornecerá um URL para a visualização da estimativa. |

## Próximas etapas

Depois de ler este guia, você deve conhecer melhor como trabalhar com pré-visualizações e estimativas usando a API de segmentação. Para saber como acessar métricas relacionadas aos dados do Perfil do cliente em tempo real, como o número total de fragmentos do perfil e perfis mesclados em namespaces específicos ou o armazenamento de dados do Perfil como um todo, visite o guia de ponto final [pré-visualização do perfil (`/previewsamplestatus`)](../../profile/api/preview-sample-status.md).