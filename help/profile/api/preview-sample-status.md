---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;visualização;amostra;;profile;real-time customer profile;troubleshooting;API;preview;sample
title: Visualizar ponto de extremidade da API Status de amostra (Visualização de perfil)
description: O ponto de extremidade de status da amostra de visualização da API do perfil do cliente em tempo real permite visualizar a amostra bem-sucedida mais recente dos dados do perfil, listar a distribuição do perfil por conjunto de dados e por identidade e gerar relatórios mostrando a sobreposição do conjunto de dados, a sobreposição de identidade e os perfis não compilados.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: bb2cfb479031f9e204006ba489281b389e6c6c04
workflow-type: tm+mt
source-wordcount: '2306'
ht-degree: 1%

---

# Visualizar ponto de extremidade do status da amostra (Visualização do perfil)

O Adobe Experience Platform permite assimilar dados do cliente de várias fontes para criar um perfil robusto e unificado para cada cliente individual. À medida que os dados são assimilados na Experience Platform, um trabalho de amostra é executado para atualizar a contagem de perfis e outras métricas relacionadas aos dados do Perfil do cliente em tempo real.

Os resultados deste trabalho de amostra podem ser exibidos usando o ponto de extremidade `/previewsamplestatus`, parte da API de Perfil do Cliente em Tempo Real. Esse endpoint também pode ser usado para listar distribuições de perfil por conjunto de dados e namespace de identidade, bem como para gerar vários relatórios para obter visibilidade sobre a composição do armazenamento de perfis de sua organização. Este guia aborda as etapas necessárias para exibir essas métricas usando o ponto de extremidade da API `/previewsamplestatus`.

>[!NOTE]
>
>Há endpoints de estimativa e pré-visualização disponíveis como parte da API do Serviço de segmentação da Adobe Experience Platform que permitem exibir informações de nível de resumo sobre definições de segmento para ajudar a garantir que você esteja isolando o público-alvo esperado. Para encontrar etapas detalhadas para trabalhar com endpoints de visualização e estimativa, visite o [guia de endpoints de visualizações e estimativas](../../segmentation/api/previews-and-estimates.md), parte do guia do desenvolvedor da API [!DNL Segmentation].

## Introdução

O ponto de extremidade de API usado neste guia faz parte da [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Fragmentos de perfil versus perfis mesclados

Este guia faz referência a &quot;fragmentos de perfil&quot; e &quot;perfis mesclados&quot;. É importante entender a diferença entre esses termos antes de continuar.

Cada perfil de cliente individual é composto por vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização provavelmente terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados.

Quando os fragmentos de perfil são assimilados na Experience Platform, eles são mesclados (com base em uma política de mesclagem) para criar um único perfil para esse cliente. Portanto, o número total de fragmentos de perfil provavelmente sempre será maior que o número total de perfis mesclados, pois cada perfil é composto de vários fragmentos.

Para saber mais sobre os perfis e suas funções na Experience Platform, comece lendo a [Visão geral do Perfil do cliente em tempo real](../home.md).

## Como o trabalho de amostra é acionado

Como os dados habilitados para o Perfil de cliente em tempo real são assimilados no [!DNL Experience Platform], eles são armazenados no armazenamento de dados do Perfil. Quando a assimilação de registros no armazenamento de Perfil aumenta ou diminui a contagem total de perfis em mais de 3%, um trabalho de amostragem é acionado para atualizar a contagem. O modo como a amostra é acionada depende do tipo de ingestão sendo usado:

* Para **fluxos de trabalho de transmissão de dados**, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 3% foi atingido. Se tiver sido, um trabalho de amostra será automaticamente acionado para atualizar a contagem.
* Para **assimilação em lote**, dentro de 15 minutos após a assimilação bem-sucedida de um lote no repositório de perfis, se o limite de aumento ou diminuição de 3% for atingido, um trabalho será executado para atualizar a contagem. Usando a API de perfil, é possível visualizar o trabalho de amostra bem-sucedido mais recente, bem como listar a distribuição do perfil por conjunto de dados e por namespace de identidade.

A contagem de perfis e as métricas de namespace também estão disponíveis na seção [!UICONTROL Profiles] da interface do Experience Platform. Para obter informações sobre como acessar os dados do Perfil usando a interface do usuário, consulte o [[!DNL Profile] guia da interface](../ui/user-guide.md).

## Exibir status da última amostra {#view-last-sample-status}

Você pode exibir os detalhes do último trabalho de amostra bem-sucedido executado para sua organização fazendo uma solicitação GET para o ponto de extremidade `/previewsamplestatus`. Esse relatório inclui o número total de perfis na amostra, bem como a métrica de contagem de perfis ou o número total de perfis que sua organização tem na Experience Platform.

A contagem de perfis é gerada após a mesclagem de fragmentos de perfis para formar um único perfil para cada cliente individual. Em outras palavras, quando os fragmentos de perfil são mesclados, eles retornam uma contagem de &quot;1&quot; perfil, pois todos estão relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de série temporal (evento), como perfis do Adobe Analytics. O trabalho de amostra é atualizado regularmente à medida que os dados do perfil são assimilados, a fim de fornecer um número total atualizado de perfis no Experience Platform.

**Formato da API**

```http
GET /previewsamplestatus
```

**Solicitação**

+++ Uma solicitação de amostra para exibir o último status de amostra.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 e inclui os detalhes do último trabalho de amostra bem-sucedido executado para a organização.

+++ Uma resposta de amostra que contém o último status de amostra.

>[!NOTE]
>
>Nesta resposta de exemplo, `numRowsToRead` e `totalRows` são iguais um ao outro. Dependendo do número de perfis que sua organização tem no Experience Platform, esse pode ser o caso. No entanto, geralmente esses dois números são diferentes, com `numRowsToRead` sendo o número menor porque representa a amostra como um subconjunto do número total de perfis (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `numRowsToRead` | O número total de perfis mesclados na amostra. |
| `sampleJobRunning` | Um valor booleano que retorna `true` quando um trabalho de exemplo está em andamento. Fornece transparência na latência que ocorre de quando um arquivo em lote é carregado para quando ele é realmente adicionado ao armazenamento de Perfil. |
| `docCount` | Contagem total de documentos no banco de dados. |
| `totalFragmentCount` | Número total de fragmentos de perfil no armazenamento Perfil. |
| `lastSuccessfulBatchTimestamp` | Carimbo de data e hora da última assimilação de lote bem-sucedida. |
| `streamingDriven` | *Este campo foi descontinuado e não tem significado para a resposta.* |
| `totalRows` | Número total de perfis mesclados no Experience Platform, também conhecido como contagem de perfis. |
| `lastBatchId` | ID de assimilação do último lote. |
| `status` | Status da última amostra. |
| `samplingRatio` | Taxa de perfis mesclados da amostra (`numRowsToRead`) para o total de perfis mesclados (`totalRows`), expressa como uma porcentagem no formato decimal. |
| `mergeStrategy` | Estratégia de mesclagem usada na amostra. |
| `lastSampledTimestamp` | Carimbo de data/hora da última amostra bem-sucedida. |

+++

## Listar distribuição de perfis por conjunto de dados

Você pode ver a distribuição de perfis por conjunto de dados fazendo uma solicitação GET para o ponto de extremidade `/previewsamplestatus/report/dataset`.

**Formato da API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parâmetros de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios tiverem sido executados na data, o relatório mais recente dessa data será retornado. Se não existir um relatório para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. | `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o parâmetro `date` para retornar o relatório mais recente para a data especificada.

+++ Uma solicitação de amostra para recuperar a distribuição do perfil por conjunto de dados.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Resposta**

>[!NOTE]
>
>Se houver vários relatórios para a data, somente o relatório mais recente será retornado. Se não existir um relatório de conjunto de dados para a data fornecida, o Status HTTP 404 (Não encontrado) será retornado.

Uma resposta bem-sucedida retorna o status HTTP 200 e inclui uma matriz `data`, contendo uma lista de objetos de conjunto de dados.

+++ Uma resposta de amostra que contém os objetos de conjunto de dados mais recentes.

>[!NOTE]
>
>A resposta a seguir mostrada foi truncada para mostrar três conjuntos de dados.

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sampleCount` | O número total de perfis mesclados amostrados com essa ID de conjunto de dados. |
| `samplePercentage` | O `sampleCount` como uma porcentagem do número total de perfis mesclados de amostra (o valor `numRowsToRead`, conforme retornado no [último status de amostra](#view-last-sample-status)), expresso em formato decimal. |
| `fullIDsCount` | O número total de perfis mesclados com essa ID de conjunto de dados. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do número total de perfis mesclados (o valor `totalRows`, conforme retornado no [último status de amostra](#view-last-sample-status)), expresso em formato decimal. |
| `name` | O nome do conjunto de dados, conforme fornecido durante a criação do conjunto. |
| `description` | A descrição do conjunto de dados, conforme fornecida durante a criação do conjunto de dados. |
| `value` | A ID do conjunto de dados. |
| `streamingIngestionEnabled` | Se o conjunto de dados está ativado para assimilação por transmissão. |
| `createdUser` | A ID do usuário que criou o conjunto de dados. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um parâmetro `date` foi fornecido durante a solicitação, o relatório retornado será para a data fornecida. Se nenhum parâmetro `date` for fornecido, o relatório mais recente será retornado. |

+++

## Listar distribuição de perfil por namespace de identidade

Você pode executar uma solicitação GET para o ponto de extremidade `/previewsamplestatus/report/namespace` a fim de exibir o detalhamento por namespace de identidade em todos os perfis mesclados em seu repositório de perfis. Isso inclui as identidades padrão fornecidas pelo Adobe, bem como as identidades personalizadas definidas pela sua organização.

Os namespaces de identidade são um componente importante do Serviço de identidade da Adobe Experience Platform que serve como indicadores do contexto ao qual os dados do cliente se relacionam. Para saber mais, comece lendo a [visão geral do namespace de identidade](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>O número total de perfis por namespace (somando os valores mostrados para cada namespace) pode ser maior que a métrica de contagem de perfis, pois um perfil pode ser associado a vários namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

**Formato da API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parâmetros de consulta | Descrição | Exemplo |
| --------------- | ----------- | ------- |
| `date` | Especifica a data do relatório a ser retornado. Se vários relatórios tiverem sido executados na data, o relatório mais recente dessa data será retornado. Se não existir um relatório para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: `YYYY-MM-DD`. | `date=2025-6-20` |

**Solicitação**

A solicitação a seguir não especifica um parâmetro `date` e retornará o relatório mais recente.

+++ Um exemplo de solicitação para retornar o relatório mais recente para distribuição de perfil por namespace. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 e inclui uma matriz `data`, com objetos individuais contendo os detalhes de cada namespace. A resposta mostrada foi truncada para mostrar quatro namespaces.

+++ Uma resposta de amostra contém informações sobre a distribuição de perfil por namespace.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `sampleCount` | O número total de perfis mesclados de amostra no namespace. |
| `samplePercentage` | O `sampleCount` como uma porcentagem de perfis mesclados amostrados (o valor `numRowsToRead`, conforme retornado no [último status de amostra](#view-last-sample-status)), expresso em formato decimal. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um parâmetro `date` foi fornecido durante a solicitação, o relatório retornado será para a data fornecida. Se nenhum parâmetro `date` for fornecido, o relatório mais recente será retornado. |
| `fullIDsFragmentCount` | O número total de fragmentos de perfil no namespace. |
| `fullIDsCount` | O número total de perfis mesclados no namespace. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do total de perfis mesclados (o valor `totalRows`, conforme retornado no [último status de amostra](#view-last-sample-status)), expresso em formato decimal. |
| `code` | O `code` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando a [API do Serviço de Identidade da Adobe Experience Platform](../../identity-service/api/list-namespaces.md) e também é conhecido como [!UICONTROL Identity symbol] na interface do usuário do Experience Platform. Para saber mais, visite a [visão geral do namespace de identidade](../../identity-service/features/namespaces.md). |
| `value` | O valor `id` do namespace. Isso pode ser encontrado ao trabalhar com namespaces usando a [API do Serviço de Identidade](../../identity-service/api/list-namespaces.md). |

+++

## Listar as estatísticas do conjunto de dados {#dataset-stats}

Você pode gerar um relatório que forneça estatísticas sobre o conjunto de dados fazendo uma solicitação GET para o ponto de extremidade `/previewsamplestatus/report/dataset_stats`.

**Formato da API**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Solicitação**

+++ Uma solicitação de amostra para gerar o relatório de estatísticas do conjunto de dados.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre as estatísticas do conjunto de dados.

+++ Um exemplo de resposta que contém informações sobre as estatísticas do conjunto de dados.

>[!NOTE]
>
>A resposta a seguir foi truncada para mostrar três conjuntos de dados.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `120days` | O número de registros que permanecerão no conjunto de dados após 120 dias de expiração. |
| `14days` | O número de registros que permanecerão no conjunto de dados após 14 dias de expiração. |
| `30days` | O número de registros que permanecerão no conjunto de dados após 30 dias de expiração. |
| `365days` | O número de registros que permanecerão no conjunto de dados após a expiração de 365 dias. |
| `60days` | O número de registros que permanecerão no conjunto de dados após uma expiração de dados de 60 dias. |
| `7days` | O número de registros que permanecerão no conjunto de dados após uma expiração de dados de 7 dias. |
| `90days` | O número de registros que permanecerão no conjunto de dados após uma expiração de dados de 90 dias. |
| `datasetId` | A ID do conjunto de dados. |
| `datasetType` | O tipo de conjunto de dados. Este valor pode ser `Profiles` ou `ExperienceEvents`. |
| `percentEvents` | A porcentagem de registros de Eventos de experiência que estão no conjunto de dados. |
| `percentProfiles` | A porcentagem de registros do Perfil que estão dentro do conjunto de dados. |
| `profileFragments` | O número total de fragmentos de perfil existentes no conjunto de dados. |
| `records` | O número total de registros de perfil assimilados no conjunto de dados. |
| `totalProfiles` | O número total de Perfis assimilados no conjunto de dados. |

+++

## Obter o tamanho do conjunto de dados {#character-count}

Você pode usar esse endpoint para obter o tamanho do conjunto de dados em bytes semana a semana.

**Formato da API**

```http
GET /previewsamplestatus/report/character_count
```

**Solicitação**

+++Um exemplo de solicitação para gerar o relatório de contagem de caracteres.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/character_count \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o tamanho do conjunto de dados durante as semanas.

+++ Uma resposta de amostra que contém informações sobre o tamanho do conjunto de dados após as expirações de dados.

>[!NOTE]
>
>A resposta a seguir foi truncada para mostrar três conjuntos de dados.

```json
{
    "data": [
        {
            "datasetIds": [
                {
                    "datasetId": "67aba91a453f7d298cd2a643",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 107773533894,
                            "week": "2025-10-26"
                        }
                    ]
                },
                {
                    "datasetId": "67aa6c867c3110298b017f0e",
                    "recordType": "timeseries",
                    "weeks": [
                        {
                            "size": 242902062440,
                            "week": "2025-10-26"
                        },
                        {
                            "size": 837539413062,
                            "week": "2025-10-19"
                        },
                        {
                            "size": 479253986484,
                            "week": "2025-10-12"
                        },
                        {
                            "size": 358911988990,
                            "week": "2025-10-05"
                        },
                        {
                            "size": 349701073042,
                            "week": "2025-09-28"
                        }
                    ]
                },
                {
                    "datasetId": "680c043667c0d7298c9ea275",
                    "recordType": "keyvalue",
                    "weeks": [
                        {
                            "size": 18392459832,
                            "week": "2025-10-26"
                        }
                    ]
                }
            ],
            "modelName": "_xdm.context.profile",
            "reportTimestamp": "2025-10-30T00:28:30.069Z"
        }
    ],
    "reportTimestamp": "2025-10-30T00:28:30.069Z"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `datasetId` | A ID do conjunto de dados. |
| `recordType` | O tipo de dados no conjunto de dados. O tipo de registro afeta o valor da variável `weeks`. Os valores suportados incluem `keyvalue` e `timeseries`. |
| `weeks` | Uma matriz que contém as informações de tamanho sobre o conjunto de dados. Para conjuntos de dados do tipo de registro `keyvalue`, isso contém a semana mais recente, bem como o tamanho total do conjunto de dados em bytes. Para conjuntos de dados do tipo de registro `timeseries`, contém todas as semanas desde a assimilação do conjunto de dados até a semana mais recente e o tamanho total do conjunto de dados em bytes para cada uma dessas semanas. |
| `modelName` | O nome do modelo do conjunto de dados. Os valores possíveis incluem `_xdm.context.profile` e `_xdm.context.experienceevent`. |
| `reportTimestamp` | A data e a hora em que o relatório foi gerado. |

+++

## Próximas etapas

Agora que você sabe como visualizar dados de amostra no armazenamento de perfis e executar vários relatórios sobre os dados, também é possível usar os endpoints de estimativa e pré-visualização da API do serviço de segmentação para exibir informações de nível de resumo sobre as definições de segmento. Essas informações ajudam a garantir que você esteja isolando o público-alvo esperado. Para saber mais sobre como trabalhar com visualizações e estimativas usando a API de segmentação, visite o [manual de visualizações e estimativas de endpoints](../../segmentation/api/previews-and-estimates.md).

