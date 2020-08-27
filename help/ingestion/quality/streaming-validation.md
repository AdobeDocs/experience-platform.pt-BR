---
keywords: Experience Platform;home;popular topics;streaming
solution: Experience Platform
title: Validação de ingestão de fluxo
topic: overview
description: A ingestão de streaming permite carregar seus dados para a Adobe Experience Platform usando pontos de extremidade de streaming em tempo real. As APIs de ingestão de fluxo oferecem suporte a dois modos de validação - síncrona e assíncrona.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 3%

---


# Validação de ingestão de fluxo

A ingestão de streaming permite carregar seus dados para a Adobe Experience Platform usando pontos de extremidade de streaming em tempo real. As APIs de ingestão de fluxo oferecem suporte a dois modos de validação - síncrona e assíncrona.

## Introdução

Este guia exige uma compreensão prática dos seguintes componentes do Adobe Experience Platform:

- [Sistema do [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!Ingestão de Streaming DNL]](../streaming-ingestion/overview.md): Um dos métodos pelos quais os dados podem ser enviados [!DNL Experience Platform].

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Schema Registry], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: `application/json`

### Cobertura de validação

[!DNL Streaming Validation Service] abrange a validação nos seguintes domínios:
- Intervalo
- Presença
- Enum
- Padrão
- Tipo
- Formato

## Validação síncrona

A validação síncrona é um método de validação que fornece feedback imediato sobre por que uma ingestão falhou. No entanto, após falha, os registros que falham na validação são descartados e impedidos de serem enviados para downstream. Como resultado, a validação síncrona só deve ser utilizada durante o processo de desenvolvimento. Ao fazer a validação síncrona, os chamadores são informados do resultado da validação XDM e, se falhar, do motivo da falha.

Por padrão, a validação síncrona não está ativada. Para ativá-lo, você deve passar o parâmetro opcional de query `synchronousValidation=true` ao fazer chamadas de API. Além disso, a validação síncrona só está disponível no momento se o terminal de fluxo estiver no data center VA7.

Se uma mensagem falhar durante a validação síncrona, ela não será gravada na fila de saída, o que fornece feedback imediato para os usuários.

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O `id` valor da conexão de streaming criada anteriormente. |

**Solicitação**

Envie a seguinte solicitação para assimilar dados à entrada de dados com validação síncrona:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
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

A resposta acima lista quantas violações de schemas foram encontradas e quais foram as violações. Por exemplo, essa resposta afirma que as chaves `workEmail` e as chaves não `person` foram definidas no schema e, portanto, não são permitidas. Ele também sinaliza o valor para `_id` como incorreto, já que o schema esperava um `string`, mas um `long` foi inserido. Observe que, uma vez que cinco erros são encontrados, o serviço de validação **interrompe** o processamento dessa mensagem. No entanto, outras mensagens continuarão a ser analisadas.

## Validação assíncrona

A validação assíncrona é um método de validação que não fornece feedback imediato. Em vez disso, os dados são enviados para um lote com falha [!DNL Data Lake] para evitar perda de dados. Esses dados com falha podem ser recuperados posteriormente para análise e repetição adicionais. Este método deve ser utilizado na produção. Salvo solicitação em contrário, a ingestão de streaming opera em modos de validação assíncronos.

**Formato da API**

```http
POST /collection/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O `id` valor da conexão de streaming criada anteriormente. |

**Solicitação**

Envie a seguinte solicitação para assimilar dados à entrada de dados com validação assíncrona:

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
>Nenhum parâmetro de query extra é necessário, pois a validação assíncrona é ativada por padrão.

**Resposta**

Com a validação assíncrona ativada, uma resposta bem-sucedida retorna o seguinte:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Observe como a resposta declara que a validação síncrona foi ignorada, pois não foi explicitamente solicitada.

## Apêndice

Esta seção contém informações sobre o que os vários códigos de status significam para respostas para assimilação de dados.

### Códigos de status

| Código de status | O que significa |
| ----------- | ------------- |
| 200 | Sucesso. Para a validação síncrona, significa que ela passou nas verificações de validação. Para validação assíncrona, significa que somente recebeu a mensagem com êxito. Os usuários podem descobrir o status de uma eventual mensagem observando o conjunto de dados. |
| 400 | Erro. Há algo errado com seu pedido. Uma mensagem de erro com mais detalhes é recebida dos Serviços de validação de fluxo contínuo. |
| 401 | Erro. Sua solicitação não está autorizada - você precisará solicitar com um token do portador. Para obter mais informações sobre como solicitar acesso, consulte este [tutorial](../../tutorials/authentication.md) ou esta publicação [do](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)blog. |
| 500 | Erro. Erro interno do sistema. |
| 501 | Erro. Isso significa que a validação síncrona **não** é compatível com esse local. |
| 503 | Erro. O serviço está indisponível no momento. Os clientes devem tentar novamente pelo menos três vezes usando uma estratégia de back-off exponencial. |