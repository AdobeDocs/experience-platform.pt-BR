---
keywords: Experience Platform, home, tópicos populares, streaming, assimilação de streaming, validação de assimilação de streaming, validação, validação de assimilação de streaming, validar, validação síncrona, validação síncrona, validação assíncrona, validação assíncrona;
solution: Experience Platform
title: Validação de Assimilação de Fluxo
topic-legacy: tutorial
type: Tutorial
description: A assimilação de streaming permite carregar seus dados no Adobe Experience Platform usando endpoints de streaming em tempo real. As APIs de assimilação de streaming oferecem suporte a dois modos de validação - síncrona e assíncrona.
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: 958bd461be0eb3ed59b44759407bed40a3edc00a
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 4%

---

# Validação da assimilação de fluxo

A assimilação de streaming permite carregar seus dados no Adobe Experience Platform usando endpoints de streaming em tempo real. As APIs de assimilação de streaming oferecem suporte a dois modos de validação - síncrona e assíncrona.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md): Um dos métodos pelos quais os dados podem ser enviados para [!DNL Experience Platform].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Schema Registry], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: `application/json`

### Cobertura da validação

[!DNL Streaming Validation Service] abrange a validação nos seguintes domínios:
- Intervalo
- Presença
- Enum
- Padrão
- Tipo
- Formato

## Validação síncrona

>[!WARNING]
>
>O `syncValidation` O parâmetro de consulta só está disponível para o endpoint de mensagem única e não pode ser usado para o endpoint de lote.

A validação síncrona é um método de validação que fornece feedback imediato sobre por que uma assimilação falhou. No entanto, após uma falha, os registros que falham na validação são descartados e impedidos de serem enviados downstream. Como resultado, a validação síncrona só deve ser usada durante o processo de desenvolvimento. Ao fazer a validação síncrona, os chamadores são informados do resultado da validação XDM e, se ele falhar, do motivo da falha.

Por padrão, a validação síncrona não está ativada. Para habilitá-lo, você deve transmitir o parâmetro de consulta opcional `syncValidation=true` ao fazer chamadas de API. Além disso, a validação síncrona só está disponível no momento se o terminal de fluxo estiver no data center do VA7.

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
| `{CONNECTION_ID}` | O `id` valor da conexão de transmissão criada anteriormente. |

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

Com a validação síncrona ativada, uma resposta bem-sucedida inclui todos os erros de validação encontrados em sua carga útil:

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

A resposta acima lista quantas violações de esquema foram encontradas e quais foram as violações. Por exemplo, essa resposta declara que as chaves `workEmail` e `person` não foram definidas no schema e, portanto, não são permitidas. Também sinaliza o valor para `_id` como incorreto, já que o schema esperava um `string`, mas um `long` foi inserido em vez disso. Observe que, uma vez que cinco erros são encontrados, o serviço de validação **stop** processando essa mensagem. No entanto, outras mensagens continuarão a ser analisadas.

## Validação assíncrona

A validação assíncrona é um método de validação que não fornece feedback imediato. Em vez disso, os dados são enviados para um lote com falha no [!DNL Data Lake] para evitar perda de dados. Esses dados com falha podem ser recuperados posteriormente para análise e repetição adicionais. Esse método deve ser usado na produção. Salvo solicitação em contrário, a assimilação de streaming opera no modo de validação assíncrona.

**Formato da API**

```http
POST /collection/{CONNECTION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O `id` valor da conexão de transmissão criada anteriormente. |

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
>Nenhum parâmetro de consulta extra é necessário, pois a validação assíncrona é habilitada por padrão.

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

Observe como a resposta declara que a validação síncrona foi ignorada, pois não foi explicitamente solicitada.

## Apêndice

Esta seção contém informações sobre o que significam os vários códigos de status para respostas para assimilação de dados.

### Códigos de status

| Código de status | O que significa |
| ----------- | ------------- |
| 200 | Sucesso. Para validação síncrona, significa que ela passou nas verificações de validação. Para validação assíncrona, significa que somente recebeu a mensagem com êxito. Os usuários podem descobrir o status de uma eventual mensagem observando o conjunto de dados. |
| 400 | Erro. Há algo errado com seu pedido. Uma mensagem de erro com mais detalhes é recebida dos Serviços de validação de fluxo. |
| 401° | Erro. Sua solicitação não está autorizada - será necessário solicitar com um token portador. Para obter mais informações sobre como solicitar acesso, confira esta [tutorial](https://www.adobe.com/go/platform-api-authentication-en) ou [publicação do blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Erro. Há um erro interno do sistema. |
| 501° | Erro. Isso significa que a validação síncrona é **not** suportado para esta localização. |
| 503 | Erro. O serviço está indisponível no momento. Os clientes devem tentar novamente pelo menos três vezes usando uma estratégia exponencial de recuo. |
