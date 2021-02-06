---
keywords: Experience Platform;home;popular topics;recuperar lotes com falha;lotes com falha;ingestão em lote;lote ingestão;Lotes com falha;Obter lotes com falha;Obter lotes com falha;Baixar lotes com falha;baixar lotes com falha;baixar lotes com falha;
solution: Experience Platform
title: Recuperando Lotes com Falha Usando a API de Acesso a Dados
topic: tutorial
type: Tutorial
description: Este tutorial aborda as etapas para recuperar informações sobre um lote com falha usando APIs de ingestão de dados.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---


# Recuperando lotes com falha usando a API de acesso a dados

A Adobe Experience Platform fornece dois métodos para fazer upload e ingestão de dados. Você pode usar a ingestão em lote, que permite inserir seus dados usando vários tipos de arquivo (como CSVs), ou a ingestão em streaming, que permite inserir seus dados em [!DNL Platform] usando pontos finais de streaming em tempo real.

Este tutorial aborda as etapas para recuperar informações sobre um lote com falha usando [!DNL Data Ingestion] APIs.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Data Ingestion]](../home.md): Os métodos pelos quais os dados podem ser enviados  [!DNL Experience Platform].

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Schema Registry], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: `application/json`

### Amostra de lote com falha

Este tutorial usará dados de amostra com um carimbo de data e hora formatado incorretamente que define o valor do mês como **00**, como visto abaixo:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

A carga acima não será validada corretamente em relação ao schema XDM devido ao carimbo de data e hora malformado.

## Recuperar o lote com falha

**Formato da API**

```http
GET /batches/{BATCH_ID}/failed
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você está pesquisando. |

**Solicitação**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
```

**Resposta**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Com a resposta acima, você pode ver quais partes do lote foram bem-sucedidas e falharam. Nessa resposta, você pode ver que o arquivo `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contém o lote com falha.

## Baixar o lote com falha

Depois de saber qual arquivo no lote falhou, você pode baixar o arquivo que falhou e ver qual é a mensagem de erro.

**Formato da API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que contém o arquivo com falha. |
| `{FAILED_FILE}` | O nome do arquivo que apresenta a falha de formatação. |

**Solicitação**

A solicitação a seguir permite baixar o arquivo com erros de ingestão.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Como o lote ingerido anterior tinha uma data e hora inválida, o seguinte erro de validação será exibido.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Próximas etapas

Após ler este tutorial, você aprendeu a recuperar erros de lotes com falha. Para obter mais informações sobre a ingestão em lote, leia o [guia do desenvolvedor de ingestão em lote](../batch-ingestion/overview.md). Para obter mais informações sobre a assimilação de streaming, leia o [tutorial de criação de uma conexão de streaming](../tutorials/create-streaming-connection.md).

## Apêndice

Esta seção contém informações sobre outros tipos de erros de ingestão que podem ocorrer.

### XDM formatado incorretamente

Como o erro de carimbo de data e hora no fluxo de exemplo anterior, esses erros se devem ao XDM formatado incorretamente. Essas mensagens de erro variam, dependendo da natureza do problema. Como resultado, nenhum exemplo de erro específico pode ser exibido.

### ID de Org IMS ausente ou inválida

Esse erro é exibido se a ID de organização IMS estiver ausente na carga for inválida.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Schema XDM ausente

Esse erro será exibido se `schemaRef` para `xdmMeta` estiver ausente.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Nome de origem ausente

Esse erro será exibido se `source` no cabeçalho estiver faltando seu `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### Entidade XDM ausente

Esse erro será exibido se não houver `xdmEntity` presente.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
