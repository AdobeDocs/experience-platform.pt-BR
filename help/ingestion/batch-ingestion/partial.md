---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da ingestão parcial em lote do Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---



# Ingestão parcial em lote

A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos na Adobe Experience Platform, enquanto todos os dados incorretos são armazenados em lote separadamente, juntamente com detalhes sobre o motivo do erro.

Este documento fornece um tutorial para gerenciar a ingestão parcial em lote.

Além disso, o [apêndice](#partial-batch-ingestion-error-types) a este tutorial fornece uma referência para tipos de erro de ingestão em lote parcial.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços da Adobe Experience Platform envolvidos com a ingestão parcial de lote. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Ingestão](./overview.md)em lote: O método que a Plataforma ingere e armazena dados de arquivos de dados, como CSV e Parquet.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para APIs de plataforma.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

## Habilitar um conjunto de dados para ingestão parcial em lote na API

>[!NOTE] Esta seção descreve como ativar um conjunto de dados para a ingestão parcial de lote usando a API. Para obter instruções sobre como usar a interface do usuário, leia a etapa [ativar um conjunto de dados para a ingestão parcial em lote na etapa da interface do usuário](#enable-a-dataset-for-partial-batch-ingestion-in-the-ui) .

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

## Habilitar um conjunto de dados para a ingestão em lote parcial na interface do usuário

>[!NOTE] Esta seção descreve como ativar um conjunto de dados para a ingestão parcial em lote usando a interface do usuário. Se você já tiver ativado um conjunto de dados para a ingestão parcial em lote usando a API, poderá pular para a próxima seção.

Para ativar um conjunto de dados para ingestão parcial por meio da interface do usuário da plataforma, clique em **Conjuntos** de dados na navegação à esquerda. Você pode [criar um novo conjunto](#create-a-new-dataset-with-partial-batch-ingestion-enabled) de dados ou [modificar um conjunto de dados](#modify-an-existing-dataset-to-enable-partial-batch-ingestion)existente.

### Criar um novo conjunto de dados com a ingestão em lote parcial ativada

Para criar um novo conjunto de dados, siga as etapas no guia [do usuário do](../../catalog/datasets/user-guide.md)conjunto de dados. Depois de atingir a etapa *Configurar conjunto de dados* , anote os campos *Ingestão* parcial e Diagnóstico *de* erro.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-focus.png)

A alternância de ingestão ** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância *Error Diagnostics* só é exibida quando a alternância *Ingestão* parcial está desativada. Esse recurso permite que a Platform gere mensagens de erro detalhadas sobre os lotes ingeridos. Se a alternância *de ingestão* parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-dataset-partial-ingestion-focus.png)

O limite *de* Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Modificar um conjunto de dados existente para permitir a ingestão parcial em lote

Para modificar um conjunto de dados existente, selecione o conjunto de dados que deseja modificar. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/modify-dataset-focus.png)

A alternância de ingestão ** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

O limite *de* Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

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

## Tipos de erro de ingestão parcial em lote

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
