---
keywords: Experience Platform;página inicial;tópicos populares;recuperar lotes com falha;lotes com falha;assimilação em lote;Assimilação em lote;Lotes com falha;Obter lotes com falha;obter lotes com falha;Baixar lotes com falha;baixar lotes com falha;
solution: Experience Platform
title: Recuperação de lotes com falha usando a API de acesso a dados
type: Tutorial
description: Este tutorial aborda etapas para recuperar informações sobre um lote com falha usando APIs de assimilação de dados.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# Recuperação de lotes com falha usando a API de acesso a dados

O Adobe Experience Platform fornece dois métodos para fazer upload e assimilar dados. Você pode usar a assimilação em lote, que permite inserir os dados usando vários tipos de arquivos (como CSVs), ou a assimilação por streaming, que permite inserir os dados no [!DNL Platform] usar endpoints de transmissão em tempo real.

Este tutorial aborda etapas para recuperar informações sobre um lote com falha usando [!DNL Data Ingestion] APIs.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Data Ingestion]](../home.md): os métodos pelos quais os dados podem ser enviados para o [!DNL Experience Platform].

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo as que pertencem à [!DNL Schema Registry], são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- `Content-Type: application/json`

### Lote com falha de amostra

Este tutorial usará dados de amostra com um carimbo de data e hora formatado incorretamente que define o valor do mês a ser **00**, como se vê a seguir:

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

A carga acima não será validada corretamente no esquema XDM devido ao carimbo de data e hora malformado.

## Recuperar o lote com falha

**Formato da API**

```http
GET /batches/{BATCH_ID}/failed
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{BATCH_ID}` | A ID do lote que você está procurando. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Com a resposta acima, você pode ver quais partes do lote tiveram êxito e falharam. Nessa resposta, é possível ver que o arquivo `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contém o lote com falha.

## Baixar o lote com falha

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

A solicitação a seguir permite baixar o arquivo que continha erros de assimilação.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Como o lote assimilado anterior tinha uma data-hora inválida, o seguinte erro de validação será mostrado.

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

Depois de ler este tutorial, você aprendeu a recuperar erros de lotes com falha. Para obter mais informações sobre a assimilação em lote, leia o [guia do desenvolvedor de assimilação em lote](../batch-ingestion/overview.md). Para obter mais informações sobre a assimilação por transmissão, leia o [tutorial de criação de uma conexão de transmissão](../tutorials/create-streaming-connection.md).

## Apêndice

Esta seção contém informações sobre outros tipos de erro de assimilação que podem ocorrer.

### XDM formatado incorretamente

Assim como o erro de carimbo de data e hora no fluxo de exemplo anterior, esses erros se devem ao XDM formatado incorretamente. Essas mensagens de erro variam de acordo com a natureza do problema. Como resultado, nenhum exemplo de erro específico pode ser mostrado.

### ID de organização IMS ausente ou inválida

Esse erro será exibido se a ID da Organização IMS estiver ausente na carga for inválida.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Esquema XDM ausente

Esse erro é exibido se a variável `schemaRef` para o `xdmMeta` está ausente.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Nome de origem ausente

Esse erro é exibido se a variável `source` o cabeçalho não tem o respectivo `name`.

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

Esse erro é exibido se não houver `xdmEntity` presente.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
