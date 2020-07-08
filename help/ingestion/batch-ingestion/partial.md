---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da ingestão em lote parcial de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---



# Ingestão parcial em lote (Beta)

A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos no Adobe Experience Platform, enquanto todos os dados incorretos são armazenados separadamente em lote, juntamente com detalhes sobre o motivo da inválida.

Este documento fornece um tutorial para gerenciar a ingestão parcial em lote.

Além disso, o [apêndice](#appendix) a este tutorial fornece uma referência para tipos de erro de ingestão em lote parcial.

>[!IMPORTANT]
>
>Este recurso só existe usando a API. Entre em contato com sua equipe para obter acesso a este recurso.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços de Adobe Experience Platform envolvidos com a ingestão parcial do lote. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Ingestão](./overview.md)em lote: O método que a Platform ingere e armazena dados de arquivos de dados, como CSV e Parquet.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da Platform.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

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

## Habilitar um conjunto de dados para ingestão parcial em lote na API

<!-- >[!NOTE] This section describes enabling a dataset for partial batch ingestion using the API. For instructions on using the UI, please read the [enable a dataset for partial batch ingestion in the UI](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) step. -->

Você pode criar um novo conjunto de dados ou modificar um conjunto de dados existente com a ingestão parcial ativada.

Para criar um novo conjunto de dados, siga as etapas em [criar um tutorial](../../catalog/api/create-dataset.md)de conjunto de dados. Depois de acessar a etapa *Criar um conjunto de dados* , adicione o seguinte campo no corpo da solicitação:

```json
{
    ...
    "tags" : {
        "partialBatchIngestion":["errorThresholdPercentage:5"]
    },
    ...
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `errorThresholdPercentage` | A porcentagem de erros aceitáveis antes que todo o lote falhe. |

Da mesma forma, para modificar um conjunto de dados existente, siga as etapas no guia [do desenvolvedor do](../../catalog/api/update-object.md)Catálogo.

No conjunto de dados, será necessário adicionar a tag descrita acima.

<!-- ## Enable a dataset for partial batch ingestion in the UI

>[!NOTE]
>
>This section describes enabling a dataset for partial batch ingestion using the UI. If you have already enabled a dataset for partial batch ingestion using the API, you can skip ahead to the next section.

To enable a dataset for partial ingestion through the Platform UI, click **Datasets** in the left navigation. You can either [create a new dataset](#create-a-new-dataset-with-partial-batch-ingestion-enabled) or [modify an existing dataset](#modify-an-existing-dataset-to-enable-partial-batch-ingestion).

### Create a new dataset with partial batch ingestion enabled

To create a new dataset, follow the steps in the [dataset user guide](../../catalog/datasets/user-guide.md). Once you reach the *Configure dataset* step, take note of the *Partial Ingestion* and *Error Diagnostics* fields.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error Diagnostics* toggle only appears when the *Partial Ingestion* toggle is off. This feature allows Platform to generate detailed error messages about your ingested batches. If the *Partial Ingestion* toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%.

### Modify an existing dataset to enable partial batch ingestion

To modify an existing dataset, select the dataset you want to modify. The sidebar on the right populates with information about the dataset. 

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

The *Partial ingestion* toggle allows you to enable or disable the use of partial batch ingestion.

The *Error threshold* allows you to set the percentage of acceptable errors before the entire batch will fail. By default, this value is set to 5%. -->

## Recuperar erros de ingestão em lote parcial

Se os lotes contiverem falhas, será necessário recuperar informações de erro sobre essas falhas para que você possa assimilar os dados novamente.

### Verificar status

Para verificar o status do lote ingerido, forneça a ID do lote no caminho de uma solicitação GET.

**Formato da API**

```http
GET /catalog/batches/{BATCH_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | O `id` valor do lote do qual você deseja verificar o status. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o status do lote.

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            ...
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

Se o lote tiver um erro e o diagnóstico de erro estiver ativado, o status será &quot;bem-sucedido&quot; com mais informações sobre o erro fornecido em um arquivo de erro que pode ser baixado.

## Próximas etapas

Este tutorial aborda como criar ou modificar um conjunto de dados para permitir a ingestão parcial em lote. Para mais informações sobre a ingestão por lote, leia o guia [do desenvolvedor da ingestão por](./api-overview.md)lote.

## Tipos de erro de ingestão parcial em lote {#appendix}

A ingestão parcial em lote tem quatro tipos de erro diferentes ao assimilar dados.

- [Arquivos ilegíveis](#unreadable)
- [schemas ou cabeçalhos inválidos](#schemas-headers)
- [Linhas não analisáveis](#unparsable)
- [Conversão XDM inválida](#conversion)

### Arquivos ilegíveis {#unreadable}

Se o lote ingerido tiver arquivos ilegíveis, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no guia [](../quality/retrieve-failed-batches.md)recuperar lotes com falha.

### schemas ou cabeçalhos inválidos {#schemas-headers}

Se o lote ingerido tiver um schema inválido ou cabeçalhos inválidos, os erros do lote serão anexados ao próprio lote. Mais informações sobre como recuperar o lote com falha podem ser encontradas no guia [](../quality/retrieve-failed-batches.md)recuperar lotes com falha.

### Linhas não analisáveis {#unparsable}

Se o lote ingerido tiver linhas não analisáveis, os erros do lote serão armazenados em um arquivo que pode ser acessado usando o ponto de extremidade descrito abaixo.

**Formato da API**

```http
GET /export/batches/{BATCH_ID}/failed?path=parse_errors
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | O `id` valor do lote do qual você está recuperando informações de erro. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=parse_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das linhas não analisáveis.

```json
{
    "_corrupt_record":"{missingQuotes:"v1"}",
    "_errors": [{
         "code":"1401",
         "message":"Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "a1.json"
}
```

### Conversão XDM inválida {#conversion}

Se o lote ingerido tiver conversões XDM inválidas, os erros do lote serão armazenados em um arquivo que pode ser acessado usando o terminal a seguir.

**Formato da API**

```http
GET /export/batches/{BATCH_ID}/failed?path=conversion_errors
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{BATCH_ID}` | O `id` valor do lote do qual você está recuperando informações de erro. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path=conversion_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das falhas na conversão XDM.

```json
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col3",
        "code":"123",
        "message":"Cannot convert array element from Object to String"
    }],
    "_filename":"a1.json"
},
{
    "col1":"v1",
    "col2":"v2",
    "col3":[{
        "g1":"h1"
    }],
    "_errors":[{
        "column":"col1",
        "code":"100",
        "message":"Cannot convert string to float"
    }],
    "_filename":"a2.json"
}
```
