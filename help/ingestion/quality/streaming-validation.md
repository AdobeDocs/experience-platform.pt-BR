---
keywords: Experience Platform;página inicial;tópicos populares;fluxo;assimilação de fluxo;assimilação de fluxo validação;validação;validação de assimilação de fluxo;validar;Validação síncrona;validação síncrona;Validação assíncrona;validação assíncrona;
solution: Experience Platform
title: Validação de assimilação de fluxo
type: Tutorial
description: A assimilação de streaming permite fazer upload de dados no Adobe Experience Platform usando endpoints de streaming em tempo real. As APIs de assimilação de streaming são compatíveis com dois modos de validação - síncrono e assíncrono.
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 15%

---

# Validação de assimilação de streaming

A assimilação de streaming permite fazer upload de dados no Adobe Experience Platform usando endpoints de streaming em tempo real. As APIs de assimilação de streaming são compatíveis com dois modos de validação - síncrono e assíncrono.

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Um dos métodos pelos quais os dados podem ser enviados para [!DNL Experience Platform].

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas da [!DNL Experience Platform].

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para APIs da [!DNL Experience Platform], você deve concluir primeiro o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Schema Registry], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: `application/json`

### Cobertura de validação

[!DNL Streaming Validation Service] abrange validação nas seguintes áreas:

- Intervalo
- Presença
- Enumeração
- Padrão
- Tipo
- Formato

## Validação síncrona

A validação síncrona é um método de validação que fornece feedback imediato sobre por que uma assimilação falhou. No entanto, após a falha, os registros que falham na validação são descartados e impedidos de serem enviados para o downstream. Como resultado, a validação síncrona só deve ser usada durante o processo de desenvolvimento. Ao fazer a validação síncrona, os chamadores são informados sobre o resultado da validação do XDM e, se falhar, o motivo da falha.

Por padrão, a validação síncrona não está ativada. Para habilitá-lo, você deve transmitir o parâmetro de consulta opcional `syncValidation=true` ao fazer chamadas de API. Além disso, a validação síncrona está disponível no momento apenas se o terminal de fluxo estiver no data center do VA7.

>[!NOTE]
>
>O parâmetro de consulta `syncValidation` está disponível apenas para o único ponto de extremidade de mensagem e não pode ser usado para o ponto de extremidade de lote.

Se uma mensagem falhar durante a validação síncrona, ela não será gravada na fila de saída, o que fornece feedback imediato para os usuários.

>[!NOTE]
>
>As alterações no esquema podem não estar imediatamente disponíveis, pois as alterações são armazenadas em cache. Aguarde até quinze minutos para que o cache seja atualizado.

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão de streaming criada anteriormente. |

**Solicitação**

Envie a seguinte solicitação para assimilar dados na entrada de dados com validação síncrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | O corpo JSON de um dado que você deseja assimilar. |

**Resposta**

Com a validação síncrona ativada, uma resposta bem-sucedida inclui todos os erros de validação encontrados em sua carga:

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

A resposta acima lista quantas violações de esquema foram encontradas e quais foram as violações. Por exemplo, esta resposta indica que as chaves `workEmail` e `person` não foram definidas no esquema e, portanto, não são permitidas. Também sinaliza o valor de `_id` como incorreto, já que o esquema esperava um `string`, mas foi inserido um `long`. Observe que depois que cinco erros forem encontrados, o serviço de validação **parará** o processamento dessa mensagem. No entanto, outras mensagens continuarão sendo analisadas.

## Validação assíncrona

A validação assíncrona é um método de validação que não fornece feedback imediato. Em vez disso, os dados são enviados para um lote com falha no [!DNL Data Lake] para evitar perda de dados. Esses dados com falha podem ser recuperados posteriormente para análise adicional e repetição. Esse método deve ser usado na produção. A menos que solicitado de outra forma, a assimilação por transmissão opera no modo de validação assíncrono.

**Formato da API**

```http
POST /collection/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão de streaming criada anteriormente. |

**Solicitação**

Envie a seguinte solicitação para assimilar dados na entrada de dados com validação assíncrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | O corpo JSON de um dado que você deseja assimilar. |

>[!NOTE]
>
>Nenhum parâmetro de consulta extra é necessário, pois a validação assíncrona está habilitada por padrão.

**Resposta**

Com a validação assíncrona ativada, uma resposta bem-sucedida retorna o seguinte:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

Observe como a resposta indica que a validação síncrona foi ignorada, pois não foi explicitamente solicitada.

## Apêndice

Esta seção contém informações sobre o que os vários códigos de status significam para respostas para assimilação de dados.

### Códigos de status

| Código de status | O que significa |
| ----------- | ------------- |
| 200 | Sucesso. Para validação síncrona, significa que ele passou nas verificações de validação. Para validação assíncrona, significa que só recebeu a mensagem com êxito. Os usuários podem descobrir o status da mensagem eventual observando o conjunto de dados. |
| 400 | Erro. Há algo errado com a sua solicitação. Uma mensagem de erro com mais detalhes é recebida dos Serviços de validação de transmissão. |
| 401 | Erro. Sua solicitação não é autorizada - será necessário solicitar com um token de portador. Para obter mais informações sobre como solicitar acesso, confira este [tutorial](https://www.adobe.com/go/platform-api-authentication-en) ou esta [publicação do blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Erro. Erro interno do sistema. |
| 501 | Erro. Isto significa que a validação síncrona **não** tem suporte para este local. |
| 503 | Erro. Serviço indisponível no momento. Os clientes devem tentar novamente pelo menos três vezes usando uma estratégia de retirada exponencial. |
