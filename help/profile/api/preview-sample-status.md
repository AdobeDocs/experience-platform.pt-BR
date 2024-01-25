---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;visualização;amostra;profile;real-time customer profile;troubleshooting;API;preview;sample
title: Visualizar ponto de extremidade da API Status de amostra (Visualização de perfil)
description: O ponto de extremidade de status da amostra de visualização da API do perfil do cliente em tempo real permite visualizar a amostra bem-sucedida mais recente dos dados do perfil, listar a distribuição do perfil por conjunto de dados e por identidade e gerar relatórios mostrando a sobreposição do conjunto de dados, a sobreposição de identidade e os perfis não compilados.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2906'
ht-degree: 1%

---

# Visualizar ponto de extremidade do status da amostra (Visualização do perfil)

O Adobe Experience Platform permite assimilar dados do cliente de várias fontes para criar um perfil robusto e unificado para cada cliente individual. À medida que os dados são assimilados na Platform, um trabalho de amostra é executado para atualizar a contagem de perfis e outras métricas relacionadas aos dados do Perfil do cliente em tempo real.

Os resultados deste trabalho de amostra podem ser exibidos usando o `/previewsamplestatus` endpoint, parte da API de Perfil do cliente em tempo real. Esse endpoint também pode ser usado para listar distribuições de perfil por conjunto de dados e namespace de identidade, bem como para gerar vários relatórios para obter visibilidade sobre a composição da Loja de perfis da sua organização. Este guia aborda as etapas necessárias para exibir essas métricas usando o `/previewsamplestatus` Endpoint da API.

>[!NOTE]
>
>Há endpoints de estimativa e pré-visualização disponíveis como parte da API do Serviço de segmentação da Adobe Experience Platform que permitem exibir informações de nível de resumo sobre definições de segmento para ajudar a garantir que você esteja isolando o público-alvo esperado. Para encontrar etapas detalhadas para trabalhar com endpoints de pré-visualização e estimativa, visite o [guia de visualizações e estimativas de endpoints](../../segmentation/api/previews-and-estimates.md), parte da [!DNL Segmentation] Guia do desenvolvedor de API.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, reveja o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Fragmentos de perfil versus perfis mesclados

Este guia faz referência a &quot;fragmentos de perfil&quot; e &quot;perfis mesclados&quot;. É importante entender a diferença entre esses termos antes de continuar.

Cada perfil de cliente individual é composto por vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização provavelmente terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados.

Quando os fragmentos de perfil são assimilados na Platform, eles são mesclados (com base em uma política de mesclagem) para criar um único perfil para esse cliente. Portanto, o número total de fragmentos de perfil provavelmente sempre será maior que o número total de perfis mesclados, pois cada perfil é composto de vários fragmentos.

Para saber mais sobre perfis e sua função no Experience Platform, comece lendo o [Visão geral do Perfil do cliente em tempo real](../home.md).

## Como o trabalho de amostra é acionado

Como os dados ativados para o Perfil do cliente em tempo real são assimilados na [!DNL Platform], ele é armazenado no armazenamento de dados do Perfil. Quando a assimilação de registros no Armazenamento de perfis aumenta ou diminui a contagem total de perfis em mais de 5%, um trabalho de amostragem é acionado para atualizar a contagem. O modo como a amostra é acionada depende do tipo de ingestão sendo usado:

* Para **fluxos de trabalho de dados de transmissão**, uma verificação é feita por hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, um trabalho de amostra será automaticamente acionado para atualizar a contagem.
* Para **assimilação em lote** No entanto, dentro de 15 minutos após a assimilação bem-sucedida de um lote no Armazenamento de perfis, se o limite de aumento ou diminuição de 5% for atingido, um trabalho será executado para atualizar a contagem. Usando a API de perfil, é possível visualizar o trabalho de amostra bem-sucedido mais recente, bem como listar a distribuição do perfil por conjunto de dados e por namespace de identidade.

A contagem de perfis e as métricas de perfil por namespace também estão disponíveis nas [!UICONTROL Perfis] seção da interface do Experience Platform. Para obter informações sobre como acessar os dados do perfil usando a interface do, visite o [[!DNL Profile] Guia da interface do usuário](../ui/user-guide.md).

## Exibir status da última amostra {#view-last-sample-status}

Você pode executar uma solicitação do GET para o `/previewsamplestatus` endpoint para exibir os detalhes do último trabalho de amostra bem-sucedido executado para sua organização. Isso inclui o número total de perfis na amostra, bem como a métrica de contagem de perfis ou o número total de perfis que sua organização tem no Experience Platform.

A contagem de perfis é gerada após a mesclagem de fragmentos de perfis para formar um único perfil para cada cliente individual. Em outras palavras, quando os fragmentos de perfil são mesclados, eles retornam uma contagem de &quot;1&quot; perfil, pois todos estão relacionados ao mesmo indivíduo.

A contagem de perfis também inclui perfis com atributos (dados de registro), bem como perfis que contêm apenas dados de série temporal (evento), como perfis do Adobe Analytics. O trabalho de amostra é atualizado regularmente à medida que os dados do perfil são assimilados para fornecer um número total atualizado de perfis na Platform.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui os detalhes do último trabalho de amostra bem-sucedido executado para a organização.

>[!NOTE]
>
>Neste exemplo de resposta, `numRowsToRead` e `totalRows` são iguais entre si. Dependendo do número de perfis que sua organização tem no Experience Platform, esse pode ser o caso. No entanto, geralmente esses dois números são diferentes, com `numRowsToRead` ser o número menor porque representa a amostra como um subconjunto do número total de perfis (`totalRows`).

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
| `numRowsToRead` | O número total de perfis mesclados na amostra. |
| `sampleJobRunning` | Um valor booleano que retorna `true` quando um trabalho de amostra está em andamento. Fornece transparência na latência que ocorre de quando um arquivo em lote é carregado para quando ele é realmente adicionado à Loja de perfil. |
| `cosmosDocCount` | Contagem total de documentos no Cosmos. |
| `totalFragmentCount` | Número total de fragmentos de perfil no Armazenamento de perfis. |
| `lastSuccessfulBatchTimestamp` | Carimbo de data e hora da última assimilação de lote bem-sucedida. |
| `streamingDriven` | *Este campo foi descontinuado e não tem significado para a resposta.* |
| `totalRows` | Número total de perfis mesclados no Experience Platform, também conhecido como &quot;contagem de perfis&quot;. |
| `lastBatchId` | ID de assimilação do último lote. |
| `status` | Status da última amostra. |
| `samplingRatio` | Taxa de perfis mesclados amostrados (`numRowsToRead`) para o total de perfis mesclados (`totalRows`), expresso como uma porcentagem no formato decimal. |
| `mergeStrategy` | Estratégia de mesclagem usada na amostra. |
| `lastSampledTimestamp` | Carimbo de data/hora da última amostra bem-sucedida. |

## Listar distribuição de perfis por conjunto de dados

Para ver a distribuição de perfis por conjunto de dados, execute uma solicitação GET para o `/previewsamplestatus/report/dataset` terminal.

**Formato da API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios tiverem sido executados na data, o relatório mais recente dessa data será retornado. Se não existir um relatório para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` para retornar o relatório mais recente para a data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma `data` matriz, contendo uma lista de objetos de conjunto de dados. A resposta mostrada foi truncada para mostrar três conjuntos de dados.

>[!NOTE]
>
>Se houver vários relatórios para a data, somente o relatório mais recente será retornado. Se não existir um relatório de conjunto de dados para a data fornecida, o Status HTTP 404 (Não encontrado) será retornado.

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
| `sampleCount` | O número total de perfis mesclados amostrados com essa ID de conjunto de dados. |
| `samplePercentage` | A variável `sampleCount` como uma porcentagem do número total de perfis mesclados amostrados (o `numRowsToRead` como retornado na variável [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `fullIDsCount` | O número total de perfis mesclados com essa ID de conjunto de dados. |
| `fullIDsPercentage` | A variável `fullIDsCount` como uma porcentagem do número total de perfis mesclados (a variável `totalRows` como retornado na variável [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `name` | O nome do conjunto de dados, conforme fornecido durante a criação do conjunto. |
| `description` | A descrição do conjunto de dados, conforme fornecida durante a criação do conjunto de dados. |
| `value` | A ID do conjunto de dados. |
| `streamingIngestionEnabled` | Se o conjunto de dados está ativado para assimilação por transmissão. |
| `createdUser` | A ID do usuário que criou o conjunto de dados. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um `date` foi fornecido durante a solicitação, o relatório retornado refere-se à data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |

## Listar distribuição de perfil por namespace de identidade

Você pode executar uma solicitação do GET para o `/previewsamplestatus/report/namespace` para exibir o detalhamento por namespace de identidade em todos os perfis mesclados na Loja de perfis. Isso inclui as identidades padrão fornecidas pelo Adobe, bem como as identidades personalizadas definidas pela sua organização.

Os namespaces de identidade são um componente importante do Serviço de identidade da Adobe Experience Platform que serve como indicadores do contexto ao qual os dados do cliente se relacionam. Para saber mais, comece lendo o [visão geral do namespace de identidade](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>O número total de perfis por namespace (somando os valores mostrados para cada namespace) pode ser maior que a métrica de contagem de perfis, pois um perfil pode ser associado a vários namespaces. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

**Formato da API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios tiverem sido executados na data, o relatório mais recente dessa data será retornado. Se não existir um relatório para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir não especifica um `date` e retornará o relatório mais recente.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui uma `data` com objetos individuais contendo os detalhes de cada namespace. A resposta mostrada foi truncada para mostrar quatro namespaces.

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
| `sampleCount` | O número total de perfis mesclados de amostra no namespace. |
| `samplePercentage` | A variável `sampleCount` como uma porcentagem dos perfis mesclados amostrados (a variável `numRowsToRead` como retornado na variável [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um `date` foi fornecido durante a solicitação, o relatório retornado refere-se à data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |
| `fullIDsFragmentCount` | O número total de fragmentos de perfil no namespace. |
| `fullIDsCount` | O número total de perfis mesclados no namespace. |
| `fullIDsPercentage` | A variável `fullIDsCount` como uma porcentagem do total de perfis mesclados (a variável `totalRows` como retornado na variável [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `code` | A variável `code` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando o [API do serviço de identidade da Adobe Experience Platform](../../identity-service/api/list-namespaces.md) e também é conhecida como a [!UICONTROL Símbolo de identidade] na interface do Experience Platform. Para saber mais, visite o [visão geral do namespace de identidade](../../identity-service/features/namespaces.md). |
| `value` | A variável `id` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando o [API do serviço de identidade](../../identity-service/api/list-namespaces.md). |

## Gerar o relatório de sobreposição do conjunto de dados

O relatório de sobreposição de conjunto de dados fornece visibilidade sobre a composição do Armazenamento de perfis da sua organização, expondo os conjuntos de dados que mais contribuem para seu público-alvo endereçável (perfis mesclados). Além de fornecer insights sobre seus dados, esse relatório pode ajudá-lo a tomar medidas para otimizar o uso da licença, como definir expirações para determinados conjuntos de dados.

Você pode gerar o relatório de sobreposição do conjunto de dados executando uma solicitação GET para o `/previewsamplestatus/report/dataset/overlap` terminal.

Para obter instruções passo a passo que descrevem como gerar o relatório de sobreposição do conjunto de dados usando a linha de comando ou a interface do usuário do Postman, consulte [tutorial para gerar relatórios de sobreposição do conjunto de dados](../tutorials/dataset-overlap-report.md).

**Formato da API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios forem executados na mesma data, o relatório mais recente dessa data será retornado. Se não existir um relatório para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` para retornar o relatório mais recente para a data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status HTTP 200 (OK) e o relatório de sobreposição do conjunto de dados.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Propriedade | Descrição |
|---|---|
| `data` | A variável `data` O objeto contém listas de conjuntos de dados separadas por vírgulas e suas respectivas contagens de perfis. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um `date` foi fornecido durante a solicitação, o relatório retornado refere-se à data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |

### Interpretação do relatório de sobreposição do conjunto de dados

Os resultados do relatório podem ser interpretados a partir dos conjuntos de dados e das contagens de perfil na resposta. Considere o exemplo de relatório a seguir `data` objeto:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Esse relatório fornece as seguintes informações:

* Há 123 perfis compostos de dados provenientes dos seguintes conjuntos de dados: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Há 454.412 perfis compostos de dados provenientes desses dois conjuntos de dados: `5d92921872831c163452edc8` e `5eb2cdc6fa3f9a18a7592a98`.
* Há 107 perfis compostos apenas de dados do conjunto de dados `5eeda0032af7bb19162172a7`.
* Há um total de 454.642 perfis na organização.

## Gerar o relatório de sobreposição de namespace de identidade {#identity-overlap-report}

O relatório de sobreposição de namespace de identidade fornece visibilidade sobre a composição da Loja de perfis da sua organização, expondo os namespaces de identidade que mais contribuem para seu público-alvo endereçável (perfis mesclados). Isso inclui os namespaces de identidade padrão fornecidos pelo Adobe, bem como os namespaces de identidade personalizados definidos pela sua organização.

Você pode gerar o relatório de sobreposição de namespace de identidade executando uma solicitação GET para o `/previewsamplestatus/report/namespace/overlap` terminal.

**Formato da API**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios forem executados na mesma data, o relatório mais recente dessa data será retornado. Se não existir um relatório para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` para retornar o relatório mais recente para a data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status HTTP 200 (OK) e o relatório de sobreposição de namespace de identidade.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Propriedade | Descrição |
|---|---|
| `data` | A variável `data` O objeto contém listas separadas por vírgulas com combinações exclusivas de códigos de namespace de identidade e suas respectivas contagens de perfil. |
| Códigos de namespace | A variável `code` é um formulário curto para cada nome de namespace de identidade. Um mapeamento de cada `code` à sua `name` pode ser encontrado usando o [API do serviço de identidade da Adobe Experience Platform](../../identity-service/api/list-namespaces.md). A variável `code` também é conhecido como [!UICONTROL Símbolo de identidade] na interface do Experience Platform. Para saber mais, visite o [visão geral do namespace de identidade](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se um `date` foi fornecido durante a solicitação, o relatório retornado refere-se à data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |

### Interpretação do relatório de sobreposição de namespace de identidade

Os resultados do relatório podem ser interpretados a partir das identidades e das contagens de perfil na resposta. O valor numérico de cada linha informa quantos perfis são compostos dessa combinação exata de namespaces de identidade padrão e personalizados.

Considere o seguinte trecho do `data` objeto:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Esse relatório fornece as seguintes informações:

* Há 142 perfis compostos de `AAID`, `ECID`, e `Email` identidades padrão, bem como de um identificador personalizado `crmid` namespace de identidade.
* Há 24 perfis compostos de `AAID` e `ECID` namespaces de identidade.
* Há 6.565 perfis que incluem apenas um `ECID` identidade.

## Gerar o relatório de perfis não compilados

Você pode obter mais visibilidade sobre a composição da Loja de perfis da sua organização por meio do relatório de perfis não compilados. Um perfil &quot;não corrigido&quot; é um perfil que contém apenas um fragmento de perfil. Um perfil &quot;desconhecido&quot; é um perfil associado a namespaces de identidade pseudônimos, como `ECID` e `AAID`. Perfis desconhecidos estão inativos, o que significa que eles não adicionaram novos eventos no período especificado. O relatório de perfis não compilados fornece um detalhamento de perfis por um período de 7, 30, 60, 90 e 120 dias.

Você pode gerar o relatório de perfis não compilados executando uma solicitação GET para o `/previewsamplestatus/report/unstitchedProfiles` terminal.

**Formato da API**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Solicitação**

A solicitação a seguir retorna o relatório de perfis não compilados.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status HTTP 200 (OK) e o relatório de perfis não compilados.

>[!NOTE]
>
>Para os fins deste guia, o relatório foi truncado para incluir apenas `"120days"` e &quot;`7days`&quot; períodos. O relatório de perfis não compilados completos fornece um detalhamento de perfis por um período de 7, 30, 60, 90 e 120 dias.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Propriedade | Descrição |
|---|---|
| `data` | A variável `data` objeto contém as informações retornadas para o relatório de perfis não compilados. |
| `totalNumberOfProfiles` | A contagem total de perfis únicos no Armazenamento de perfis. Isso é equivalente à contagem de público-alvo endereçável. Inclui perfis conhecidos e não compilados. |
| `totalNumberOfEvents` | O número total de ExperienceEvents no Armazenamento de perfis. |
| `unstitchedProfiles` | Um objeto que contém um detalhamento de perfis não compilados por período de tempo. O relatório de perfis não compilados fornece um detalhamento dos perfis por períodos de 7, 30, 60, 90 e 120 dias. |
| `countOfProfiles` | A contagem de perfis não compilados para o período de tempo ou a contagem de perfis não compilados para o namespace. |
| `eventsAssociated` | O número de ExperienceEvents para o intervalo de tempo ou o número de eventos para o namespace. |
| `nsDistribution` | Um objeto que contém namespaces de identidade individuais com a distribuição de perfis e eventos não compilados para cada namespace. Observação: somando o total `countOfProfiles` para cada namespace de identidade na variável `nsDistribution` objeto é igual a `countOfProfiles` para o período de tempo. O mesmo é válido para `eventsAssociated` por namespace e o total `eventsAssociated` por período. |
| `reportTimestamp` | O carimbo de data e hora do relatório. |

### Interpretação do relatório de perfis não compilados

Os resultados do relatório podem fornecer insights sobre quantos perfis não compilados e inativos sua organização tem em sua Loja de perfis.

Considere o seguinte trecho do `data` objeto:

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Esse relatório fornece as seguintes informações:

* Há 1.782 perfis que contêm apenas um fragmento de perfil e não têm eventos novos nos últimos sete dias.
* Há 29.151 ExperienceEvents associados aos 1.782 perfis não compilados.
* Há 1.734 perfis não compilados contendo um único fragmento de perfil do namespace de identidade da ECID.
* Há 28.591 eventos associados aos 1.734 perfis não compilados que contêm um único fragmento de perfil do namespace de identidade da ECID.

## Próximas etapas

Agora que você sabe como visualizar dados de amostra no Armazenamento de perfis e executar vários relatórios sobre os dados, também é possível usar os endpoints de estimativa e pré-visualização da API do serviço de segmentação para exibir informações de nível de resumo sobre as definições de segmento. Essas informações ajudam a garantir que você esteja isolando o público-alvo esperado. Para saber mais sobre como trabalhar com visualizações e estimativas usando a API de segmentação, visite o [guia de visualização e estimativa de endpoints](../../segmentation/api/previews-and-estimates.md).

