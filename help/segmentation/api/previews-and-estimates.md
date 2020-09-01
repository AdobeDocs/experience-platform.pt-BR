---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;previews;estimates;previews and estimates;estimates and previews;api;API;
solution: Experience Platform
title: Pré-visualizações e endpoints de estimativas
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 2%

---


# Pré-visualizações e endpoints de estimativas

À medida que você desenvolve a definição do segmento, você pode usar as ferramentas de estimativa e pré-visualização dentro das informações de nível de resumo da visualização para ajudar a garantir que você esteja isolando a audiência esperada. [!DNL Adobe Experience Platform] **As pré-visualizações** fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o esperado. **As estimativas** fornecem informações estatísticas sobre uma definição de segmento, como o tamanho da audiência projetada, o intervalo de confiança e o desvio padrão do erro.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, consulte o guia [de](./getting-started.md) introdução para obter informações importantes que você precisa saber para fazer chamadas à API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

## Como as estimativas são geradas

A forma como a amostragem de dados é acionada depende do método de ingestão.

Para a ingestão em lote, o armazenamento de perfis é verificado automaticamente a cada quinze minutos para ver se um novo lote foi ingerido com êxito desde a execução do último trabalho de amostragem. Se for esse o caso, a loja de perfis é analisada posteriormente para verificar se houve pelo menos uma mudança de 5% no número de registros. Se essas condições forem atendidas, um novo trabalho de amostragem será acionado.

Para a ingestão em streaming, a loja de perfis é automaticamente verificada a cada hora para ver se houve pelo menos uma mudança de 5% no número de registros. Se essa condição for cumprida, um novo trabalho de amostragem será acionado.

O tamanho da amostra da verificação depende do número geral de entidades na loja de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto completo de dados |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

>[!NOTE]
>
>As estimativas geralmente levam de 10 a 15 segundos para serem executadas, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

## Create a new preview {#create-preview}

Você pode criar uma nova pré-visualização, enviando uma solicitação de POST para o `/preview` terminal.

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
| `predicateModel` | O nome do schema [!DNL Experience Data Model] (XDM) no qual os dados do perfil se baseiam. |

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

Você pode recuperar informações detalhadas sobre uma pré-visualização específica, fazendo uma solicitação de GET para o `/preview` terminal e fornecendo a ID da pré-visualização no caminho da solicitação.

**Formato da API**

```http
GET /preview/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | O `previewId` valor da pré-visualização que você deseja recuperar. |

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
        },
        "state": "RESULT_READY",
        "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
        }
    }],
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `results` | Uma lista de IDs de entidade, juntamente com suas identidades relacionadas. Os links fornecidos podem ser usados para procurar as entidades especificadas, usando a API de acesso ao Perfil [[!DNL]](../../profile/api/entities.md). |

## Recuperar os resultados de uma ordem de produção de estimativa específica {#get-estimate}

Depois de criar um trabalho de pré-visualização, você pode usá-lo `previewId` no caminho de uma solicitação de GET para o `/estimate` terminal para visualização de informações estatísticas sobre a definição do segmento, incluindo o tamanho de audiência projetado, o intervalo de confiança e o desvio padrão do erro.

**Formato da API**

```http
GET /estimate/{PREVIEW_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{PREVIEW_ID}` | Um trabalho de estimativa só é acionado quando um trabalho de pré-visualização é criado e os dois trabalhos compartilham o mesmo valor de ID para fins de pesquisa. Especificamente, esse é o `previewId` valor retornado quando o trabalho de pré-visualização foi criado. |

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
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `state` | O estado atual do trabalho de pré-visualização. Será &quot;EM EXECUÇÃO&quot; até que o processamento seja concluído, e nesse momento ele se tornará &quot;RESULT_READY&quot; ou &quot;FALHA&quot;. |
| `_links.preview` | Quando o estado atual da tarefa de pré-visualização é &quot;RESULT_READY&quot;, este atributo fornece um URL para visualização da estimativa. |

## Próximas etapas

Depois de ler esse guia, agora você tem um melhor entendimento de como trabalhar com pré-visualizações e estimativas. Para saber mais sobre os outros pontos de extremidade da [!DNL Segmentation Service] API, leia a visão geral [do guia do desenvolvedor do Serviço de](./overview.md)segmentação.