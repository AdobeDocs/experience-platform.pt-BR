---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;preview;sample
solution: Adobe Experience Platform
title: Pré-visualização do perfil - API do Perfil do cliente em tempo real
description: A Adobe Experience Platform permite que você ingira dados do cliente de várias fontes para criar perfis unificados robustos para clientes individuais. Como os dados habilitados para o Perfil de cliente em tempo real são ingeridos na Plataforma, eles são armazenados no armazenamento de dados do Perfil. À medida que o número de registros no repositório de Perfis aumenta ou diminui, uma tarefa de amostra é executada que inclui informações sobre quantos fragmentos de perfil e perfis mesclados estão no repositório de dados. Usando a API de Perfil, você pode pré-visualização a amostra mais recente bem-sucedida, bem como a distribuição de perfis por conjunto de dados e por namespace de identidade.
topic: guide
translation-type: tm+mt
source-git-commit: 2edba7cba4892f5c8dd41b15219bf45597bd5219
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---


# Ponto de extremidade do status da amostra da pré-visualização (pré-visualização do Perfil)

A Adobe Experience Platform permite que você ingira dados do cliente de várias fontes para criar perfis unificados robustos para clientes individuais. Como os dados habilitados para o Perfil do cliente em tempo real são ingeridos, [!DNL Platform]eles são armazenados no armazenamento de dados do Perfil.

Quando a ingestão de registros no repositório de Perfis aumenta ou diminui a contagem total de perfis em mais de 5%, uma tarefa é acionada para atualizar a contagem. Para workflows de dados de fluxo contínuo, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi cumprido. Se houver, uma tarefa será acionada automaticamente para atualizar a contagem. Para ingestão em lote, em 15 minutos após a ingestão bem-sucedida de um lote no repositório de Perfis, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem. Usando a API de Perfil, você pode pré-visualização o trabalho de amostra mais recente e bem-sucedido, bem como a distribuição de perfis por conjunto de dados e por namespace de identidade.

Essas métricas também estão disponíveis na seção [!UICONTROL Perfil] da interface do usuário do Experience Platform. Para obter informações sobre como acessar os dados do Perfil usando a interface do usuário, visite o guia [[!DNL Profile] do](../ui/user-guide.md)usuário.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Real-time Customer Profile] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, reveja o guia [de](getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Status da última amostra da visualização {#view-last-sample-status}

Você pode executar uma solicitação de GET para o `/previewsamplestatus` ponto de extremidade para visualização dos detalhes do último trabalho de amostra bem-sucedido executado para sua Organização IMS. Isso inclui o número total de perfis na amostra, bem como a métrica de contagem de perfis ou o número total de perfis que sua organização tem dentro do Experience Platform. A contagem de perfis é gerada após a união de fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, sua organização pode ter vários fragmentos de perfil relacionados a um único cliente que interage com sua marca em canais diferentes, mas esses fragmentos seriam unidos (de acordo com a política de mesclagem padrão) e retornariam uma contagem de perfis &quot;1&quot;, pois estão todos relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de séries cronológicas (eventos), como perfis Adobe Analytics. O trabalho de amostra é atualizado regularmente à medida que os dados do Perfil são ingeridos para fornecer um número total atualizado de perfis na Plataforma.

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
>Neste exemplo de resposta, `numRowsToRead` e `totalRows` são iguais entre si. Dependendo do número de perfis que sua organização tiver no Experience Platform, isso pode ser o caso. No entanto, geralmente esses dois números são diferentes, sendo `numRowsToRead` o menor, porque representa a amostra como um subconjunto do número total de perfis (`totalRows`).

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
| `sampleJobRunning` | Um valor booliano que retorna `true` quando um trabalho de amostra está em andamento. Fornece transparência na latência que ocorre quando um arquivo em lote é carregado para quando ele é realmente adicionado à loja de Perfis. |
| `cosmosDocCount` | Contagem total de documentos no Cosmos. |
| `totalFragmentCount` | O número total de fragmentos de perfil no repositório de Perfis. |
| `lastSuccessfulBatchTimestamp` | Carimbo de data e hora da última ingestão em lote bem-sucedida. |
| `streamingDriven` | *Este campo foi descontinuado e não contém significância para a resposta.* |
| `totalRows` | O número total de perfis unidos na plataforma Experience, também conhecidos como a &quot;contagem de perfis&quot;. |
| `lastBatchId` | ID de ingestão do último lote. |
| `status` | Status da última amostra. |
| `samplingRatio` | Rácio entre perfis unidos amostrados (`numRowsToRead`) e o total de perfis unidos (`totalRows`), expresso em percentagem no formato decimal. |
| `mergeStrategy` | Estratégia de mesclagem usada na amostra. |
| `lastSampledTimestamp` | Último carimbo de data e hora de amostra bem-sucedido. |

## Distribuição de perfis de lista por conjunto de dados

Para ver a distribuição de perfis por conjunto de dados, é possível executar uma solicitação de GET para o `/previewsamplestatus/report/dataset` ponto de extremidade.

**Formato da API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios forem executados na data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro 404 será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` parâmetro para retornar o relatório mais recente para a data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma `data` matriz que contém uma lista de objetos de conjunto de dados. A resposta mostrada foi truncada para mostrar três conjuntos de dados.

>[!NOTE]
>
>Se existissem vários relatórios para a data, somente os mais recentes seriam retornados. Se um relatório de conjunto de dados não existisse para a data fornecida, o Status HTTP 404 (Não encontrado) seria retornado.

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
| `sampleCount` | O número total de perfis unidos de amostra com essa ID de conjunto de dados. |
| `samplePercentage` | A `sampleCount` porcentagem do número total de perfis unidos de amostra (o `numRowsToRead` valor retornado no status [da](#view-last-sample-status)última amostra), expresso em formato decimal. |
| `fullIDsCount` | O número total de perfis unidos com essa ID de conjunto de dados. |
| `fullIDsPercentage` | A `fullIDsCount` porcentagem do número total de perfis unidos (o `totalRows` valor retornado no status [da](#view-last-sample-status)última amostra), expresso em formato decimal. |
| `name` | O nome do conjunto de dados, conforme fornecido durante a criação do conjunto de dados. |
| `description` | A descrição do conjunto de dados, conforme fornecida durante a criação do conjunto de dados. |
| `value` | A ID do conjunto de dados. |
| `streamingIngestionEnabled` | Se o conjunto de dados está habilitado para a ingestão em streaming. |
| `createdUser` | A ID de usuário do usuário que criou o conjunto de dados. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um `date` parâmetro foi fornecido durante a solicitação, o relatório retornado é a data fornecida. Se nenhum `date` parâmetro for fornecido, o relatório mais recente será retornado. |



## Distribuição de perfis de lista por namespace

Você pode executar uma solicitação de GET para o `/previewsamplestatus/report/namespace` ponto de extremidade para visualização do detalhamento por namespace de identidade em todos os perfis unidos em sua loja de Perfis. As namespaces de identidade são um componente importante do Adobe Experience Platform Identity Service que serve como indicadores do contexto ao qual os dados do cliente se relacionam. Para saber mais, visite a visão geral [](../../identity-service/namespaces.md)da namespace de identidade.

>[!NOTE]
>
>O número total de perfis por namespace (somando os valores mostrados para cada namespace) sempre será maior que a métrica de contagem de perfis porque um perfil pode estar associado a várias namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, várias namespaces serão associadas a esse cliente individual.

**Formato da API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios forem executados na data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro 404 será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir não especifica um `date` parâmetro e, portanto, retornará o relatório mais recente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma `data` matriz, com objetos individuais contendo os detalhes de cada namespace. A resposta mostrada foi truncada para mostrar quatro namespaces.

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
| `sampleCount` | O número total de perfis unidos de amostra na namespace. |
| `samplePercentage` | O `sampleCount` como uma porcentagem de perfis unidos de amostra (o `numRowsToRead` valor retornado no status [da](#view-last-sample-status)última amostra), expresso em formato decimal. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um `date` parâmetro foi fornecido durante a solicitação, o relatório retornado é a data fornecida. Se nenhum `date` parâmetro for fornecido, o relatório mais recente será retornado. |
| `fullIDsFragmentCount` | O número total de fragmentos de perfil na namespace. |
| `fullIDsCount` | O número total de perfis unidos na namespace. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do total de perfis unidos (o `totalRows` valor retornado no status [da](#view-last-sample-status)última amostra), expresso em formato decimal. |
| `code` | O `code` da namespace. Isso pode ser encontrado ao trabalhar com o namespace usando a API [do](../../identity-service/api/list-namespaces.md) Adobe Experience Platform Identity Service e também é conhecido como o símbolo [!UICONTROL de] identidade na interface do usuário do Experience Platform. Para saber mais, visite a visão geral [](../../identity-service/namespaces.md)da namespace de identidade. |
| `value` | O `id` valor da namespace. Isso pode ser encontrado ao trabalhar com o namespace usando a API [do Serviço de](../../identity-service/api/list-namespaces.md)identidade. |

## Próximas etapas

Você também pode usar estimativas e pré-visualizações semelhantes para obter informações de nível de resumo da visualização relacionadas às definições de segmento, para ajudar a garantir que você esteja isolando a audiência esperada. Para encontrar etapas detalhadas para trabalhar com pré-visualizações de segmentos e estimativas usando a [!DNL Adobe Experience Platform Segmentation Service] API, visite o guia [de pontos de extremidade de](../../segmentation/api/previews-and-estimates.md)pré-visualizações e estimativas, parte do guia do desenvolvedor de [!DNL Segmentation] API.

