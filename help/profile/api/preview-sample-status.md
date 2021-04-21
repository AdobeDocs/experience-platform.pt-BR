---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, visualização, amostra
title: Visualizar ponto de extremidade da API de status de amostra (Visualização de perfil)
description: Usando o ponto de extremidade de status de amostra de visualização, parte da API de Perfil do cliente em tempo real, é possível visualizar a amostra mais recente e bem-sucedida de seus dados de Perfil, bem como listar a distribuição de perfis por conjunto de dados e por namespace de identidade no Adobe Experience Platform.
topic-legacy: guide
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 1%

---

# Visualizar ponto de extremidade do status da amostra (Visualização do perfil)

O Adobe Experience Platform permite assimilar dados de clientes de várias fontes para criar perfis unificados robustos para clientes individuais. Como os dados ativados para o Perfil do cliente em tempo real são assimilados em [!DNL Platform], eles são armazenados no armazenamento de dados do Perfil.

Quando a assimilação de registros no armazenamento de perfil aumenta ou diminui a contagem total de perfis em mais de 5%, um trabalho de amostragem é disparado para atualizar a contagem. A forma como a amostra é acionada depende do tipo de assimilação que está sendo usado:

* Para **fluxos de trabalho de dados de transmissão**, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, um trabalho de amostra é automaticamente acionado para atualizar a contagem.
* Para **ingestão em lote**, dentro de 15 minutos da assimilação bem-sucedida de um lote no armazenamento de Perfil, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem. Com a API de perfil, é possível visualizar o trabalho de amostra bem-sucedido mais recente, bem como a distribuição de perfil de lista por conjunto de dados e por namespace de identidade.

Essas métricas também estão disponíveis na seção [!UICONTROL Profiles] da interface do usuário do Experience Platform. Para obter informações sobre como acessar os dados do perfil usando a interface do usuário, visite o [[!DNL Profile] guia do usuário](../ui/user-guide.md).

>[!NOTE]
>
>Há endpoints de estimativa e pré-visualização disponíveis como parte da API do Serviço de segmentação do Adobe Experience Platform que permitem exibir informações de nível de resumo relacionadas às definições de segmento para ajudar a garantir que você esteja isolando o público-alvo esperado. Para encontrar etapas detalhadas para trabalhar com visualização de segmento e endpoints de estimativa, visite o [guia de pré-visualizações e estimativas de endpoints](../../segmentation/api/previews-and-estimates.md), parte do [!DNL Segmentation] guia do desenvolvedor da API.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API [!DNL Experience Platform].

## Fragmentos de perfil versus perfis mesclados

Este guia faz referência a &quot;fragmentos de perfil&quot; e &quot;perfis mesclados&quot;. É importante compreender a diferença entre estes termos antes de prosseguir.

Cada perfil de cliente individual é composto de vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados (com base na política de mesclagem) para criar um único perfil para esse cliente. Portanto, o número total de fragmentos de perfil provavelmente sempre será maior que o número total de perfis mesclados, pois cada perfil é composto de vários fragmentos.

## Exibir o status da última amostra {#view-last-sample-status}

Você pode executar uma solicitação de GET para o endpoint `/previewsamplestatus` para visualizar os detalhes do último trabalho de amostra bem-sucedido executado para sua Organização IMS. Isso inclui o número total de perfis na amostra, bem como a métrica de contagem de perfis ou o número total de perfis que sua organização tem no Experience Platform. A contagem de perfis é gerada após a união de fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em diferentes canais, mas esses fragmentos seriam mesclados (de acordo com a política de mesclagem padrão) e retornariam uma contagem de perfil &quot;1&quot; porque estão todos relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de séries de tempo (evento), como perfis do Adobe Analytics. O trabalho de amostra é atualizado regularmente à medida que os dados do perfil são assimilados para fornecer um número total atualizado de perfis no Platform.

**Formato da API**

```http
GET /previewsamplestatus
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui os detalhes do último trabalho de amostra bem-sucedido executado para a organização IMS.

>[!NOTE]
>
>Nesta resposta de exemplo, `numRowsToRead` e `totalRows` são iguais entre si. Dependendo do número de perfis que sua organização tem no Experience Platform, esse pode ser o caso. No entanto, geralmente esses dois números são diferentes, com `numRowsToRead` sendo o número menor, pois representa a amostra como um subconjunto do número total de perfis (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
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
|---|---|
| `numRowsToRead` | O número total de perfis unidos na amostra. |
| `sampleJobRunning` | Um valor booleano que retorna `true` quando um trabalho de amostra está em andamento. Fornece transparência na latência de quando um arquivo em lote é carregado para quando ele é realmente adicionado ao armazenamento de Perfil. |
| `cosmosDocCount` | Contagem total de documentos no Cosmos. |
| `totalFragmentCount` | Número total de fragmentos de perfil no armazenamento de Perfil. |
| `lastSuccessfulBatchTimestamp` | Carimbo de data e hora da última assimilação em lote bem-sucedido. |
| `streamingDriven` | *Este campo foi substituído e não contém significância para a resposta.* |
| `totalRows` | Número total de perfis mesclados no Experience Platform, também conhecidos como &quot;contagem de perfis&quot;. |
| `lastBatchId` | ID da assimilação do último lote. |
| `status` | Status da última amostra. |
| `samplingRatio` | Taxa de perfis mesclados amostrados (`numRowsToRead`) para o total de perfis mesclados (`totalRows`), expressa como uma porcentagem no formato decimal. |
| `mergeStrategy` | Estratégia de mesclagem usada na amostra. |
| `lastSampledTimestamp` | Último carimbo de data e hora de amostra bem-sucedido. |

## Listar distribuição de perfil por conjunto de dados

Para ver a distribuição de perfis por conjunto de dados, é possível executar uma solicitação de GET para o endpoint `/previewsamplestatus/report/dataset`.

**Formato da API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios forem executados na data, o relatório mais recente para essa data será retornado. Se não existir um relatório para a data especificada, um erro 404 será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o parâmetro `date` para retornar o relatório mais recente da data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma matriz `data`, contendo uma lista de objetos do conjunto de dados. A resposta exibida foi truncada para mostrar três conjuntos de dados.

>[!NOTE]
>
>Se existissem vários relatórios para a data, somente o mais recente seria retornado. Se um relatório de conjunto de dados não existisse para a data fornecida, o Status HTTP 404 (Não encontrado) seria retornado.

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
|---|---|
| `sampleCount` | O número total de perfis mesclados com amostra com essa ID de conjunto de dados. |
| `samplePercentage` | O `sampleCount` como uma porcentagem do número total de perfis mesclados de amostra (o valor `numRowsToRead` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `fullIDsCount` | O número total de perfis mesclados com essa ID de conjunto de dados. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do número total de perfis mesclados (o valor `totalRows` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `name` | O nome do conjunto de dados, conforme fornecido durante a criação do conjunto de dados. |
| `description` | A descrição do conjunto de dados, conforme fornecida durante a criação do conjunto de dados. |
| `value` | A ID do conjunto de dados. |
| `streamingIngestionEnabled` | Se o conjunto de dados está ativado para assimilação de streaming. |
| `createdUser` | A ID de usuário do usuário que criou o conjunto de dados. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um parâmetro `date` foi fornecido durante a solicitação, o relatório retornado é da data fornecida. Se nenhum parâmetro `date` for fornecido, o relatório mais recente será retornado. |

## Listar distribuição de perfil por namespace

Você pode executar uma solicitação de GET para o endpoint `/previewsamplestatus/report/namespace` para visualizar o detalhamento por namespace de identidade em todos os perfis mesclados no armazenamento de Perfil. Os namespaces de identidade são um componente importante do Adobe Experience Platform Identity Service que serve como indicadores do contexto ao qual os dados do cliente estão relacionados. Para saber mais, visite a [visão geral do namespace de identidade](../../identity-service/namespaces.md).

>[!NOTE]
>
>O número total de perfis por namespace (somando os valores mostrados para cada namespace) sempre será maior que a métrica de contagem de perfis, pois um perfil pode ser associado a vários namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

**Formato da API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios forem executados na data, o relatório mais recente para essa data será retornado. Se não existir um relatório para a data especificada, um erro 404 será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir não especifica um parâmetro `date` e, portanto, retornará o relatório mais recente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma matriz `data`, com objetos individuais contendo os detalhes de cada namespace. A resposta exibida foi truncada para mostrar quatro namespaces.

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
|---|---|
| `sampleCount` | O número total de perfis mesclados com amostras no namespace. |
| `samplePercentage` | O `sampleCount` como uma porcentagem de perfis mesclados de amostra (o valor `numRowsToRead` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um parâmetro `date` foi fornecido durante a solicitação, o relatório retornado é da data fornecida. Se nenhum parâmetro `date` for fornecido, o relatório mais recente será retornado. |
| `fullIDsFragmentCount` | O número total de fragmentos de perfil no namespace. |
| `fullIDsCount` | O número total de perfis mesclados no namespace. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do total de perfis unidos (o valor `totalRows` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `code` | O `code` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando a [API do serviço de identidade da Adobe Experience Platform](../../identity-service/api/list-namespaces.md) e também é chamada de [!UICONTROL Identity symbol] na interface do usuário do Experience Platform. Para saber mais, visite a [visão geral do namespace de identidade](../../identity-service/namespaces.md). |
| `value` | O valor `id` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando a [API do serviço de identidade](../../identity-service/api/list-namespaces.md). |

## Próximas etapas

Agora que você sabe visualizar os dados de amostra no armazenamento do Perfil, também pode usar a estimativa e os endpoints de visualização da API do Serviço de segmentação para exibir as informações de nível de resumo relacionadas às definições do segmento. Essas informações ajudam a garantir que você esteja isolando o público-alvo esperado em seu segmento. Para saber mais sobre como trabalhar com visualizações e estimativas de segmento usando a API de segmentação, visite o [guia de visualização e estimativa de endpoints](../../segmentation/api/previews-and-estimates.md).
