---
keywords: Experience Platform, home, tópicos populares, recuperar lotes com falha, lotes com falha, assimilação em lote, assimilação em lote, lotes com falha, obter lotes com falha, obter lotes com falha, baixar lotes com falha, baixar lotes com falha, baixar lotes com falha;
solution: Experience Platform
title: Recuperação de Lotes com Falha Usando a API de Acesso a Dados
topic-legacy: tutorial
type: Tutorial
description: Este tutorial aborda etapas para recuperar informações sobre um lote com falha usando APIs de assimilação de dados.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 99f99ad78853236868550d880576b82da2af8878
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# Recuperação de lotes com falha usando a API de acesso a dados

O Adobe Experience Platform fornece dois métodos para fazer upload e assimilar dados. Você pode usar a assimilação em lote, que permite inserir os dados usando vários tipos de arquivo (como CSVs), ou a assimilação de streaming, que permite inserir os dados no [!DNL Platform] uso de endpoints de transmissão em tempo real.

Este tutorial aborda etapas para recuperar informações sobre um lote com falha usando [!DNL Data Ingestion] APIs.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Data Ingestion]](../home.md): Os métodos pelos quais os dados podem ser enviados para [!DNL Experience Platform].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Schema Registry], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- `Content-Type: application/json`

### Exemplo de lote com falha

Este tutorial usará dados de amostra com um carimbo de data e hora formatado incorretamente que define o valor do mês como **00**, conforme mostrado abaixo:

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

A carga acima não será validada corretamente em relação ao esquema XDM devido ao carimbo de data e hora mal formado.

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
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
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

Com a resposta acima, você pode ver quais partes do lote tiveram êxito e falharam. Nessa resposta, você pode ver que o arquivo `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contém o lote com falha.

## Baixe o lote com falha

Depois de saber qual arquivo no lote falhou, você pode baixar o arquivo com falha e ver qual é a mensagem de erro.

**Formato da API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que contém o arquivo com falha. |
| `{FAILED_FILE}` | O nome do arquivo que tem a formatação com falha. |

**Solicitação**

A solicitação a seguir permite baixar o arquivo com erros de assimilação.

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

Como o lote assimilado anterior tinha uma data e hora inválida, o seguinte erro de validação será exibido.

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

Após ler este tutorial, você aprendeu a recuperar erros de lotes com falha. Para mais informações sobre a ingestão em lote, leia o [guia do desenvolvedor de ingestão em lote](../batch-ingestion/overview.md). Para obter mais informações sobre a assimilação de streaming, leia o [tutorial de criação de uma conexão de transmissão](../tutorials/create-streaming-connection.md).

## Apêndice

Esta seção contém informações sobre outros tipos de erros de assimilação que podem ocorrer.

### XDM formatado incorretamente

Como o erro de carimbo de data e hora no fluxo de exemplo anterior, esses erros se devem a um XDM formatado incorretamente. Essas mensagens de erro variam, dependendo da natureza do problema. Como resultado, nenhum exemplo de erro específico pode ser exibido.

### ID de Org de IMS ausente ou inválido

Esse erro é mostrado se a ID da Org de IMS estiver ausente no payload for inválida.

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

### Esquema XDM ausente

Esse erro será mostrado se a variável `schemaRef` para `xdmMeta` está ausente.

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

Esse erro será mostrado se a variável `source` no cabeçalho está faltando seu `name`.

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

Esse erro será mostrado se não houver `xdmEntity` presente.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
