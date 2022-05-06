---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, visualização, amostra
title: Visualizar ponto de extremidade da API de status de amostra (Visualização de perfil)
description: Usando o ponto de extremidade de status de amostra de visualização, parte da API do Perfil do cliente em tempo real, é possível visualizar a amostra mais bem-sucedida dos dados do Perfil, listar a distribuição do perfil por conjunto de dados e por identidade e gerar relatórios que mostram a sobreposição do conjunto de dados, a sobreposição de identidades e perfis desconhecidos.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2882'
ht-degree: 1%

---

# Visualizar ponto de extremidade do status da amostra (Visualização do perfil)

O Adobe Experience Platform permite assimilar dados de clientes de várias fontes para criar um perfil robusto e unificado para cada um dos clientes individuais. À medida que os dados são assimilados no Platform, um trabalho de amostra é executado para atualizar a contagem de perfis e outras métricas relacionadas aos dados do Perfil do cliente em tempo real.

Os resultados desse trabalho de amostra podem ser exibidos usando o `/previewsamplestatus` endpoint, parte da API do Perfil do cliente em tempo real. Esse endpoint também pode ser usado para listar distribuições de perfil pelo conjunto de dados e namespace de identidade, bem como para gerar vários relatórios para ganhar visibilidade sobre a composição da Loja de perfis da sua organização. Este guia aborda as etapas necessárias para visualizar essas métricas usando o `/previewsamplestatus` Ponto de extremidade da API.

>[!NOTE]
>
>Há endpoints de estimativa e pré-visualização disponíveis como parte da API do Serviço de segmentação do Adobe Experience Platform que permitem exibir informações de nível de resumo relacionadas às definições de segmento para ajudar a garantir que você esteja isolando o público-alvo esperado. Para encontrar etapas detalhadas para trabalhar com visualização de segmento e endpoints de estimativa, visite o [guia de visualizações e estimativas de endpoints](../../segmentation/api/previews-and-estimates.md), parte do [!DNL Segmentation] Guia do desenvolvedor da API.

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Antes de continuar, reveja o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

## Fragmentos de perfil versus perfis mesclados

Este guia faz referência a &quot;fragmentos de perfil&quot; e &quot;perfis mesclados&quot;. É importante compreender a diferença entre estes termos antes de prosseguir.

Cada perfil de cliente individual é composto de vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização provavelmente terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados.

Quando os fragmentos de perfil são assimilados na Platform, eles são mesclados (com base em uma política de mesclagem) para criar um único perfil para esse cliente. Portanto, o número total de fragmentos de perfil provavelmente sempre será maior que o número total de perfis mesclados, pois cada perfil é composto de vários fragmentos.

Para saber mais sobre perfis e sua função no Experience Platform, comece lendo o [Visão geral do perfil do cliente em tempo real](../home.md).

## Como o trabalho de amostra é acionado

Como os dados habilitados para o Perfil do cliente em tempo real são assimilados em [!DNL Platform], ele é armazenado no armazenamento de dados do Perfil . Quando a assimilação de registros na Loja de perfis aumenta ou diminui a contagem total de perfis em mais de 5%, um trabalho de amostragem é disparado para atualizar a contagem. A forma como a amostra é acionada depende do tipo de assimilação que está sendo usado:

* Para **fluxos de trabalho de dados de fluxo**, uma verificação é feita de hora em hora para determinar se o limite de aumento ou diminuição de 5% foi atingido. Se tiver sido, um trabalho de amostra é automaticamente acionado para atualizar a contagem.
* Para **ingestão em lote**, em 15 minutos após a assimilação bem-sucedida de um lote na Loja de perfis, se o limite de aumento ou diminuição de 5% for atingido, uma tarefa será executada para atualizar a contagem. Com a API de perfil, é possível visualizar o trabalho de amostra bem-sucedido mais recente, bem como a distribuição de perfil de lista por conjunto de dados e por namespace de identidade.

A contagem de perfis e os perfis por métricas de namespace também estão disponíveis no [!UICONTROL Perfis] da interface do usuário do Experience Platform. Para obter informações sobre como acessar os dados do perfil usando a interface do usuário, visite o [[!DNL Profile] Guia da interface do usuário](../ui/user-guide.md).

## Exibir o status da última amostra {#view-last-sample-status}

Você pode executar uma solicitação de GET para `/previewsamplestatus` endpoint para exibir os detalhes do último trabalho de amostra bem-sucedido executado para a organização IMS. Isso inclui o número total de perfis na amostra, bem como a métrica de contagem de perfis ou o número total de perfis que sua organização tem no Experience Platform.

A contagem de perfis é gerada após a união de fragmentos de perfil para formar um único perfil para cada cliente individual. Em outras palavras, quando fragmentos de perfil são unidos, eles retornam uma contagem de perfil &quot;1&quot; porque estão todos relacionados ao mesmo indivíduo.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui os detalhes do último trabalho de amostra bem-sucedido executado para a organização.

>[!NOTE]
>
>Neste exemplo de resposta, `numRowsToRead` e `totalRows` são iguais entre si. Dependendo do número de perfis que sua organização tem no Experience Platform, esse pode ser o caso. No entanto, em geral, esses dois números são diferentes, com `numRowsToRead` sendo o número menor, pois representa a amostra como um subconjunto do número total de perfis (`totalRows`).

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
| `sampleJobRunning` | Um valor booleano que retorna `true` quando um trabalho de amostra estiver em andamento. Fornece transparência na latência de quando um arquivo em lote é carregado para quando ele é realmente adicionado à Loja de perfis. |
| `cosmosDocCount` | Contagem total de documentos no Cosmos. |
| `totalFragmentCount` | Número total de fragmentos de perfil na Loja de perfis. |
| `lastSuccessfulBatchTimestamp` | Carimbo de data e hora da última assimilação em lote bem-sucedido. |
| `streamingDriven` | *Este campo foi substituído e não contém significância para a resposta.* |
| `totalRows` | Número total de perfis mesclados no Experience Platform, também conhecidos como &quot;contagem de perfis&quot;. |
| `lastBatchId` | ID da assimilação do último lote. |
| `status` | Status da última amostra. |
| `samplingRatio` | Taxa de amostras de perfis unidos (`numRowsToRead`) para o total de perfis mesclados (`totalRows`), expresso como uma porcentagem em formato decimal. |
| `mergeStrategy` | Estratégia de mesclagem usada na amostra. |
| `lastSampledTimestamp` | Último carimbo de data e hora de amostra bem-sucedido. |

## Listar distribuição de perfil por conjunto de dados

Para ver a distribuição de perfis por conjunto de dados, é possível executar uma solicitação do GET para a função `/previewsamplestatus/report/dataset` endpoint .

**Formato da API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios foram executados na data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` para retornar o relatório mais recente da data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui um `data` , contendo uma lista de objetos do conjunto de dados. A resposta exibida foi truncada para mostrar três conjuntos de dados.

>[!NOTE]
>
>Se houver vários relatórios para a data, somente o relatório mais recente será retornado. Se um relatório de conjunto de dados não existir para a data fornecida, o Status HTTP 404 (Não encontrado) será retornado.

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
| `samplePercentage` | O `sampleCount` como uma porcentagem do número total de perfis mesclados com amostra (a variável `numRowsToRead` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `fullIDsCount` | O número total de perfis mesclados com essa ID de conjunto de dados. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do número total de perfis mesclados (a variável `totalRows` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `name` | O nome do conjunto de dados, conforme fornecido durante a criação do conjunto de dados. |
| `description` | A descrição do conjunto de dados, conforme fornecida durante a criação do conjunto de dados. |
| `value` | A ID do conjunto de dados. |
| `streamingIngestionEnabled` | Se o conjunto de dados está ativado para assimilação de streaming. |
| `createdUser` | A ID de usuário do usuário que criou o conjunto de dados. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se uma `date` foi fornecido durante a solicitação, o relatório retornado é da data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |

## Listar distribuição de perfil por namespace de identidade

Você pode executar uma solicitação de GET para `/previewsamplestatus/report/namespace` endpoint para visualizar o detalhamento por namespace de identidade em todos os perfis mesclados na Loja de perfis. Isso inclui as identidades padrão fornecidas pelo Adobe, bem como as identidades personalizadas definidas pela organização.

Os namespaces de identidade são um componente importante do Adobe Experience Platform Identity Service que serve como indicadores do contexto ao qual os dados do cliente estão relacionados. Para saber mais, comece lendo o [visão geral do namespace de identidade](../../identity-service/namespaces.md).

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
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios foram executados na data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

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

A resposta inclui um `data` , com objetos individuais contendo os detalhes de cada namespace. A resposta exibida foi truncada para mostrar quatro namespaces.

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
| `samplePercentage` | O `sampleCount` como uma porcentagem de perfis mesclados amostras (a variável `numRowsToRead` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se uma `date` foi fornecido durante a solicitação, o relatório retornado é da data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |
| `fullIDsFragmentCount` | O número total de fragmentos de perfil no namespace. |
| `fullIDsCount` | O número total de perfis mesclados no namespace. |
| `fullIDsPercentage` | O `fullIDsCount` como uma porcentagem do total de perfis unidos (a variável `totalRows` como retornado no [status da última amostra](#view-last-sample-status)), expresso em formato decimal. |
| `code` | O `code` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando o [API do serviço de identidade da Adobe Experience Platform](../../identity-service/api/list-namespaces.md) e também é chamada de [!UICONTROL Símbolo de identidade] na interface do usuário do Experience Platform. Para saber mais, visite o [visão geral do namespace de identidade](../../identity-service/namespaces.md). |
| `value` | O `id` para o namespace. Isso pode ser encontrado ao trabalhar com namespaces usando o [API do serviço de identidade](../../identity-service/api/list-namespaces.md). |

## Gerar o relatório de sobreposição de conjunto de dados

O relatório de sobreposição de conjunto de dados fornece visibilidade sobre a composição do Armazenamento de perfil de sua organização, expondo os conjuntos de dados que mais contribuem para o público-alvo endereçável (perfis mesclados). Além de fornecer insights sobre seus dados, este relatório pode ajudar você a tomar ações para otimizar o uso da licença, como definir um TTL para determinados conjuntos de dados.

Você pode gerar o relatório de sobreposição de conjunto de dados executando uma solicitação de GET para o `/previewsamplestatus/report/dataset/overlap` endpoint .

Para obter instruções passo a passo sobre como gerar o relatório de sobreposição de conjunto de dados usando a linha de comando ou a interface do usuário do Postman, consulte o [gerando o tutorial de relatório de sobreposição de conjunto de dados](../tutorials/dataset-overlap-report.md).

**Formato da API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios foram executados na mesma data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` para retornar o relatório mais recente da data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status HTTP 200 (OK) e o relatório de sobreposição de conjunto de dados.

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
| `data` | O `data` O objeto contém listas de conjuntos de dados separadas por vírgulas e suas respectivas contagens de perfil. |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se uma `date` foi fornecido durante a solicitação, o relatório retornado é da data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |

### Interpretação do relatório de sobreposição de conjunto de dados

Os resultados do relatório podem ser interpretados a partir dos conjuntos de dados e das contagens de perfil na resposta. Considere o exemplo de relatório a seguir `data` objeto:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Este relatório fornece as seguintes informações:

* Há 123 perfis compostos de dados provenientes dos seguintes conjuntos de dados: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Há 454.412 perfis compostos de dados provenientes desses dois conjuntos de dados: `5d92921872831c163452edc8` e `5eb2cdc6fa3f9a18a7592a98`.
* Há 107 perfis que são compostos apenas de dados do conjunto de dados `5eeda0032af7bb19162172a7`.
* Há um total de 454.642 perfis na organização.

## Gerar o relatório de sobreposição de namespace de identidade

O relatório de sobreposição de namespace de identidade fornece visibilidade sobre a composição da Loja de perfis de sua organização, expondo os namespaces de identidade que mais contribuem para o público-alvo endereçável (perfis mesclados). Isso inclui os namespaces de identidade padrão fornecidos pelo Adobe, bem como os namespaces de identidade personalizados definidos pela sua organização.

Você pode gerar o relatório de sobreposição de namespace de identidade executando uma solicitação de GET para o `/previewsamplestatus/report/namespace/overlap` endpoint .

**Formato da API**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios foram executados na mesma data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro 404 (Não encontrado) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Solicitação**

A solicitação a seguir usa o `date` para retornar o relatório mais recente da data especificada.

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
| `data` | O `data` contém listas separadas por vírgulas com combinações exclusivas de códigos de namespace de identidade e suas respectivas contagens de perfil. |
| Códigos de namespace | O `code` é um formulário curto para cada nome de namespace de identidade. Um mapeamento de cada `code` para `name` pode ser encontrada usando o [API do serviço de identidade da Adobe Experience Platform](../../identity-service/api/list-namespaces.md). O `code` também é chamada de [!UICONTROL Símbolo de identidade] na interface do usuário do Experience Platform. Para saber mais, visite o [visão geral do namespace de identidade](../../identity-service/namespaces.md). |
| `reportTimestamp` | O carimbo de data e hora do relatório. Se uma `date` foi fornecido durante a solicitação, o relatório retornado é da data fornecida. Se não `date` for fornecido, o relatório mais recente será retornado. |

### Interpretação do relatório de sobreposição de namespace de identidade

Os resultados do relatório podem ser interpretados a partir das identidades e contagens de perfil na resposta. O valor numérico de cada linha informa quantos perfis são compostos dessa combinação exata de namespaces de identidade padrão e personalizados.

Considere o seguinte trecho do `data` objeto:

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Este relatório fornece as seguintes informações:

* Há 142 perfis compostos de `AAID`, `ECID`e `Email` identidades padrão, bem como de um `crmid` namespace de identidade.
* Há 24 perfis compostos de `AAID` e `ECID` namespaces de identidade.
* Há 6.565 perfis que incluem apenas um `ECID` identidade.

## Gerar o relatório de perfis desconhecidos

Você pode obter mais visibilidade sobre a composição da Loja de perfis de sua organização por meio do relatório de perfis desconhecidos. Um &quot;perfil desconhecido&quot; refere-se a qualquer perfil que não tenha sido corrigido e esteja inativo por um determinado período de tempo. Um perfil &quot;não corrigido&quot; é um perfil que contém apenas um fragmento de perfil, enquanto um perfil &quot;inativo&quot; é qualquer perfil que não tenha adicionado novos eventos para o período de tempo especificado. O relatório de perfis desconhecidos fornece um detalhamento de perfis por um período de 7, 30, 60, 90 e 120 dias.

Você pode gerar o relatório de perfis desconhecidos executando uma solicitação GET para a variável `/previewsamplestatus/report/unknownProfiles` endpoint .

**Formato da API**

```http
GET /previewsamplestatus/report/unknownProfiles
```

**Solicitação**

A solicitação a seguir retorna o relatório de perfis desconhecidos.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unknownProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma solicitação bem-sucedida retorna o Status HTTP 200 (OK) e o relatório de perfis desconhecidos.

>[!NOTE]
>
>Para os fins deste guia, o relatório foi truncado para incluir somente `"120days"` e &quot;`7days`&quot; períodos de tempo. O relatório de perfis totalmente desconhecidos fornece um detalhamento de perfis por um período de 7, 30, 60, 90 e 120 dias.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unknownProfiles": {
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
| `data` | O `data` contém as informações retornadas para o relatório de perfis desconhecidos. |
| `totalNumberOfProfiles` | A contagem total de perfis únicos na Loja de perfis. Isso equivale à contagem de público-alvo endereçável. Inclui perfis conhecidos e desconhecidos. |
| `totalNumberOfEvents` | O número total de ExperienceEvents na Loja de perfis. |
| `unknownProfiles` | Um objeto que contém um detalhamento de perfis desconhecidos (não corrigidos e inativos) por período de tempo. O relatório de perfis desconhecidos fornece um detalhamento de perfis para períodos de 7, 30, 60, 90 e 120 dias. |
| `countOfProfiles` | A contagem de perfis desconhecidos para o período ou a contagem de perfis desconhecidos para o namespace. |
| `eventsAssociated` | O número de ExperienceEvents para o intervalo de tempo ou o número de eventos para o namespace. |
| `nsDistribution` | Um objeto que contém namespaces de identidade individuais com a distribuição de perfis e eventos desconhecidos para cada namespace. Observação: Somando o total `countOfProfiles` para cada namespace de identidade no `nsDistribution` é igual a `countOfProfiles` para o período de tempo. O mesmo se aplica a `eventsAssociated` por namespace e o total `eventsAssociated` por período de tempo. |
| `reportTimestamp` | O carimbo de data e hora do relatório. |

### Interpretação do relatório de perfis desconhecidos

Os resultados do relatório podem fornecer informações sobre quantos perfis não corrigidos e inativos sua organização tem em sua Loja de perfis.

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

Este relatório fornece as seguintes informações:

* Há 1.782 perfis que contêm apenas um fragmento de perfil e não têm novos eventos nos últimos sete dias.
* Há 29.151 ExperienceEvents associados aos 1.782 perfis desconhecidos.
* Há 1.734 perfis desconhecidos contendo um único fragmento de perfil do namespace de identidade do ECID.
* Há 28.591 eventos associados aos 1.734 perfis desconhecidos que contêm um único fragmento de perfil do namespace de identidade da ECID.

## Próximas etapas

Agora que você sabe visualizar os dados de amostra na Loja de perfis e executar vários relatórios sobre os dados, também pode usar a estimativa e os endpoints de visualização da API do Serviço de segmentação para exibir informações de resumo sobre as definições do segmento. Essas informações ajudam a garantir que você esteja isolando o público-alvo esperado em seu segmento. Para saber mais sobre como trabalhar com visualizações e estimativas de segmento usando a API de segmentação, visite o [guia de pré-visualização e estimativa de endpoints](../../segmentation/api/previews-and-estimates.md).

