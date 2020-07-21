---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da ingestão em lote parcial de Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 1%

---



# Ingestão parcial em lote

A ingestão parcial em lote é a capacidade de assimilar dados que contenham erros, até um certo limite. Com esse recurso, os usuários podem assimilar com êxito todos os dados corretos no Adobe Experience Platform, enquanto todos os dados incorretos são armazenados separadamente em lote, juntamente com detalhes sobre o motivo da inválida.

Este documento fornece um tutorial para gerenciar a ingestão parcial em lote.

Além disso, o [apêndice](#appendix) a este tutorial fornece uma referência para tipos de erro de ingestão em lote parcial.

## Introdução

Este tutorial requer um conhecimento prático dos vários serviços de Adobe Experience Platform envolvidos com a ingestão parcial do lote. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Ingestão](./overview.md)em lote: O método que [!DNL Platform] ingere e armazena dados de arquivos de dados, como CSV e Parquet.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para [!DNL Platform] APIs.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

## Habilitar um lote para ingestão parcial em lote na API {#enable-api}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para ingestão parcial em lote usando a API. Para obter instruções sobre como usar a interface do usuário, leia a etapa [ativar um lote para a ingestão parcial em lote na UI](#enable-ui) .

Você pode criar um novo lote com a ingestão parcial ativada.

Para criar um novo lote, siga as etapas no guia [do desenvolvedor da ingestão em](./api-overview.md)lote. Depois de atingir a etapa *Criar lote* , adicione o seguinte campo no corpo da solicitação:

```json
{
    ...
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
    ...
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `enableErrorDiagnostics` | Um sinalizador que permite [!DNL Platform] gerar mensagens de erro detalhadas sobre o lote. |
| `partialIngestionPercentage` | A porcentagem de erros aceitáveis antes que todo o lote falhe. Assim, neste exemplo, um máximo de 5% do lote pode ser de erros, antes que falhe. |


## Habilitar um lote para ingestão parcial em lote na interface do usuário {#enable-ui}

>[!NOTE]
>
>Esta seção descreve como ativar um lote para ingestão parcial em lote usando a interface do usuário. Se você já tiver ativado um lote para a ingestão parcial por lote usando a API, poderá pular para a próxima seção.

Para habilitar um lote para ingestão parcial por meio da [!DNL Platform] interface do usuário, você pode criar um novo lote por meio de conexões de origem, criar um novo lote em um conjunto de dados existente ou criar um novo lote por meio do &quot;Fluxo[!UICONTROL do]mapa CSV para XDM&quot;.

### Criar uma nova conexão de origem {#new-source}

Para criar uma nova conexão de origem, siga as etapas listadas na visão geral [](../../sources/home.md)Fontes. Depois de atingir a etapa de detalhes *[!UICONTROL do]* Dataflow, anote os campos de ingestão ** parcial e diagnóstico *[!UICONTROL de]* erro.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

A alternância de ingestão ** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância do diagnóstico ** Error só é exibida quando a alternância de ingestão ** parcial está desativada. Esse recurso permite [!DNL Platform] gerar mensagens de erro detalhadas sobre os lotes ingeridos. Se a *[!UICONTROL alternância de ingestão]* parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

O limite *[!UICONTROL de]* Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

### Usar um conjunto de dados existente {#existing-dataset}

Para usar um conjunto de dados existente, selecione um start selecionando um conjunto de dados. A barra lateral à direita é preenchida com informações sobre o conjunto de dados.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

A alternância de ingestão ** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância do diagnóstico ** Error só é exibida quando a alternância de ingestão ** parcial está desativada. Esse recurso permite [!DNL Platform] gerar mensagens de erro detalhadas sobre os lotes ingeridos. Se a *[!UICONTROL alternância de ingestão]* parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

O limite *[!UICONTROL de]* Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

Agora, você pode fazer upload de dados usando o botão **Adicionar dados** e eles serão ingeridos com a ingestão parcial.

### Usar o fluxo &quot;[!UICONTROL Mapear CSV para o schema]XDM&quot; {#map-flow}

Para usar o fluxo &quot;[!UICONTROL Mapear CSV para o schema]XDM&quot;, siga as etapas listadas no tutorial [](../tutorials/map-a-csv-file.md)Mapear um arquivo CSV. Depois de atingir a etapa *[!UICONTROL Adicionar dados]* , anote os campos *[!UICONTROL Inclusão]* parcial e Diagnóstico *[!UICONTROL de]* erro.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

A alternância de ingestão ** parcial permite ativar ou desativar o uso da ingestão em lote parcial.

A alternância do diagnóstico ** Error só é exibida quando a alternância de ingestão ** parcial está desativada. Esse recurso permite [!DNL Platform] gerar mensagens de erro detalhadas sobre os lotes ingeridos. Se a *[!UICONTROL alternância de ingestão]* parcial estiver ativada, os diagnósticos de erro aprimorados serão aplicados automaticamente.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

O limite *[!UICONTROL de]* Erro permite que você defina a porcentagem de erros aceitáveis antes que todo o lote falhe. Por padrão, esse valor é definido como 5%.

## Recuperar erros de ingestão em lote parcial {#retrieve-errors}

Se os lotes contiverem falhas, será necessário recuperar informações de erro sobre essas falhas para que você possa assimilar os dados novamente.

### Verificar status {#check-status}

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
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
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

## Próximas etapas {#next-steps}

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
