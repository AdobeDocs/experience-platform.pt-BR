---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entidades - API de Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 1%

---


# Ponto de extremidade Entidades (acesso ao Perfil)

O Adobe Experience Platform permite acessar os dados do Perfil do cliente em tempo real usando RESTful APIs ou a interface do usuário. Este guia descreve como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API. Para obter mais informações sobre como acessar perfis usando a interface do usuário do Platform, consulte o guia [do usuário do](../ui/user-guide.md)Perfil.

## Introdução

O endpoint da API usado neste guia faz parte da API [de Perfil do cliente em tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)real. Antes de continuar, consulte o guia [de](getting-started.md) introdução para obter links para a documentação relacionada, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Acessar dados do perfil por identidade

Você pode acessar uma entidade de Perfil fazendo uma solicitação GET ao ponto de `/access/entities` extremidade e fornecendo a identidade da entidade como uma série de parâmetros de query. Essa identidade consiste em um valor de ID (`entityId`) e a namespace de identidade (`entityIdNS`).

Os parâmetros de Query fornecidos no caminho da solicitação especificam quais dados devem ser acessados. É possível incluir vários parâmetros, separados por E comercial (&amp;). É fornecida uma lista completa de parâmetros válidos na seção Parâmetros [do](#query-parameters) query do apêndice.

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitação**

A solicitação a seguir recupera o email e o nome de um cliente usando uma identidade:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

>[!NOTE]
>Se um gráfico relacionado vincular mais de 50 identidades, esse serviço retornará o status HTTP 422 e a mensagem &quot;Muitas identidades relacionadas&quot;. Se você receber esse erro, considere adicionar mais parâmetros de query para restringir sua pesquisa.

## Acessar dados do perfil por lista de identidades

Você pode acessar várias entidades de perfil por suas identidades, fazendo uma solicitação POST ao `/access/entities` ponto final e fornecendo as identidades na carga. Essas identidades consistem em um valor de ID (`entityId`) e uma namespace de identidade (`entityIdNS`).

**Formato da API**

```http
POST /access/entities
```

**Solicitação**

A solicitação a seguir recupera os nomes e endereços de email de vários clientes por uma lista de identidades:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Propriedade | Descrição |
|---|---|
| `schema.name` | ***(Obrigatório)*** O nome do schema XDM ao qual a entidade pertence. |
| `fields` | Os campos XDM a serem retornados, como uma matriz de sequências de caracteres. Por padrão, todos os campos serão retornados. |
| `identities` | ***(Obrigatório)*** Uma matriz contendo uma lista de identidades para as entidades que você deseja acessar. |
| `identities.entityId` | A ID de uma entidade que você deseja acessar. |
| `identities.entityIdNS.code` | A namespace de uma ID de entidade que você deseja acessar. |
| `timeFilter.startTime` | Tempo de Start do filtro de intervalo de tempo, incluído. Deve estar em milissegundos de granularidade. O padrão, se não for especificado, é o início do tempo disponível. |
| `timeFilter.endTime` | Fim do filtro de intervalo de tempo, excluído. Deve estar em milissegundos de granularidade. O padrão, se não for especificado, é o fim do tempo disponível. |
| `limit` | Número de registros a serem retornados. Aplica-se somente ao número de eventos de experiência retornados. Padrão: 1.000. |
| `orderby` | A ordem de classificação dos eventos de experiência recuperados por carimbo de data e hora, gravado como `(+/-)timestamp` o padrão sendo `+timestamp`. |
| `withCA` | Sinalizador de recurso para ativar atributos calculados para pesquisa. Padrão: false. |

**Resposta** Uma resposta bem-sucedida retorna os campos solicitados de entidades especificadas no corpo da solicitação.

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## eventos de série de tempo de acesso para um perfil por identidade

Você pode acessar eventos de séries de tempo pela identidade da entidade associada ao perfil, fazendo uma solicitação GET ao `/access/entities` endpoint. Essa identidade consiste em um valor de ID (`entityId`) e uma namespace de identidade (`entityIdNS`).

Os parâmetros de Query fornecidos no caminho da solicitação especificam quais dados devem ser acessados. É possível incluir vários parâmetros, separados por E comercial (&amp;). É fornecida uma lista completa de parâmetros válidos na seção Parâmetros [do](#query-parameters) query do apêndice.

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitação**

A solicitação a seguir localiza uma entidade de perfil por ID e recupera os valores das propriedades `endUserIDs`, `web`e `channel` para todos os eventos de série de tempo associados à entidade.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de eventos de séries de tempo e campos associados que foram especificados nos parâmetros de query da solicitação.

>[!NOTE]
>A solicitação especificou um limite de um (`limit=1`), portanto, a resposta `count` abaixo é 1 e apenas uma entidade é retornada.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Acessar uma página subsequente de resultados

Os resultados são paginados ao recuperar eventos de séries de tempo. Se houver páginas subsequentes de resultados, a `_page.next` propriedade conterá uma ID. Além disso, a `_links.next.href` propriedade fornece um URI de solicitação para recuperar a próxima página. Para recuperar os resultados, faça outra solicitação GET para o `/access/entities` ponto de extremidade, no entanto, é necessário substituir `/entities` pelo valor do URI fornecido.

>[!NOTE]
>Certifique-se de não repetir acidentalmente `/entities/` no caminho da solicitação. Só deve aparecer uma vez como, `/access/entities?start=...`

**Formato da API**

```http
GET /access/{NEXT_URI}
```

| Parâmetro | Descrição |
|---|---|
| `{NEXT_URI}` | O valor de URI obtido a partir de `_links.next.href`. |

**Solicitação**

A solicitação a seguir recupera a próxima página de resultados usando o `_links.next.href` URI como caminho de solicitação.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a próxima página de resultados. Essa resposta não tem páginas subsequentes de resultados, conforme indicado pelos valores de sequência vazia de `_page.next` e `_links.next.href`.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## eventos de série de tempo de acesso para vários perfis por identidades

Você pode acessar eventos de séries de tempo de vários perfis associados, fazendo uma solicitação POST ao `/access/entities` endpoint e fornecendo as identidades do perfil na carga. Essas identidades consistem em um valor (`entityId`) de ID e uma namespace de identidade (`entityIdNS`).

**Formato da API**

```http
POST /access/entities
```

**Solicitação**

A solicitação a seguir recupera IDs de usuário, horários locais e códigos de país para eventos de séries de tempo associados a uma lista de identidades de perfil:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| Propriedade | Descrição |
|---|---|
| `schema.name` | **(OBRIGATÓRIO)** O schema XDM da entidade a ser recuperada |
| `relatedSchema.name` | Se `schema.name` for esse `_xdm.context.experienceevent` valor, deverá especificar o schema para a entidade do perfil ao qual os eventos de série de tempo estão relacionados. |
| `identities` | **(OBRIGATÓRIO)** Uma lista de matriz de perfis dos quais recuperar eventos de séries de tempo associados. Cada entrada no storage é definida de uma das duas maneiras: 1) usando uma identidade totalmente qualificada que consiste no valor de ID e namespace ou 2) fornecendo um XID. |
| `fields` | Isola os dados retornados para um conjunto de campos especificado. Use essa opção para filtrar quais campos de schema estão incluídos nos dados recuperados. Exemplo: personalEmail,pessoa.nome,pessoa.gênero |
| `mergePolicyId` | Identifica a Política de Mesclagem pela qual os dados retornados serão controlados. Se um não for especificado na chamada de serviço, o padrão de sua organização para esse schema será usado. Se nenhuma Política de Mesclagem padrão tiver sido configurada, o padrão não será mesclagem de perfil e nenhuma identificação. |
| `orderby` | A ordem de classificação dos eventos de experiência recuperados por carimbo de data e hora, gravado como `(+/-)timestamp` o padrão sendo `+timestamp`. |
| `timeFilter.startTime` | Especifique a hora do start para filtrar objetos de série de tempo (em milissegundos). |
| `timeFilter.endTime` | Especifique a hora de término para filtrar objetos de série de tempo (em milissegundos). |
| `limit` | Valor numérico que especifica o número máximo de objetos a serem retornados. Padrão: 1000 |
| `withCA` | Sinalizador de recurso para ativar atributos calculados para pesquisa. Padrão: false |

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de eventos de séries de tempo associados aos vários perfis especificados na solicitação.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

Neste exemplo de resposta, o primeiro perfil listado (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) fornece um valor para `_links.next.payload`, o que significa que há páginas adicionais de resultados para esse perfil. Consulte a seção a seguir sobre como [acessar resultados](#access-additional-results) adicionais para obter detalhes sobre como acessar esses resultados adicionais.

### Acessar resultados adicionais {#access-additional-results}

Ao recuperar eventos de séries de tempo, pode haver muitos resultados sendo retornados, portanto, os resultados são paginados com frequência. Se houver páginas subsequentes de resultados para um determinado perfil, o `_links.next.payload` valor desse perfil conterá um objeto payload.

Usando essa carga no corpo da solicitação, você pode executar uma solicitação POST adicional ao `access/entities` ponto final para recuperar a página subsequente dos dados da série de tempo desse perfil.

## eventos de série de tempo de acesso em várias entidades do schema

Você pode acessar várias entidades conectadas por meio de um descritor de relacionamento. A chamada de API de exemplo a seguir supõe que uma relação já tenha sido definida entre dois schemas. Para obter mais informações sobre descritores de relacionamento, leia o guia do desenvolvedor da API do Registro do Schema, guia do ponto de extremidade [dos descritores](../../xdm/api/descriptors.md).

É possível incluir parâmetros de query no caminho da solicitação para especificar quais dados serão acessados. É possível incluir vários parâmetros, separados por E comercial (&amp;). É fornecida uma lista completa de parâmetros válidos na seção Parâmetros [do](#query-parameters) query do apêndice.

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitação**

A solicitação a seguir recupera uma entidade que contém um descritor de relacionamento estabelecido anteriormente para acessar informações em diferentes schemas.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de eventos de séries de tempo associados às várias entidades.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Acessar uma página subsequente de resultados

Os resultados são paginados ao recuperar eventos de séries de tempo. Se houver páginas subsequentes de resultados, a `_page.next` propriedade conterá uma ID. Além disso, a `_links.next.href` propriedade fornece um URI de solicitação para recuperar a página subsequente, fazendo solicitações GET adicionais para o `access/entities` terminal.

## Próximas etapas

Ao seguir este guia, você acessou com êxito os campos de dados, perfis e dados de séries de tempo do Perfil do cliente em tempo real. Para saber como acessar outros recursos de dados armazenados no Platform, consulte a visão geral [do Acesso aos](../../data-access/home.md)dados.

## Apêndice {#appendix}

A seção a seguir fornece informações complementares sobre como acessar dados do Perfil usando a API.

### Query parameters {#query-parameters}

Os parâmetros a seguir são usados no caminho para solicitações GET para o ponto de extremidade `/access/entities` . Eles servem para identificar a entidade do perfil que você deseja acessar e filtrar os dados retornados na resposta. Os parâmetros obrigatórios são rotulados, enquanto os demais são opcionais.

| Parâmetro | Descrição | Exemplo |
|---|---|---|
| `schema.name` | **(OBRIGATÓRIO)** O schema XDM da entidade a ser recuperada | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Se `schema.name` for &quot;_xdm.context.experience.event&quot;, esse valor deverá especificar o schema para a entidade do perfil ao qual os eventos de série de tempo estão relacionados. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBRIGATÓRIO)** A ID da entidade. Se o valor desse parâmetro não for um XID, um parâmetro de namespace de identidade também deverá ser fornecido (consulte `entityIdNS` abaixo). | `entityId=janedoe@example.com` |
| `entityIdNS` | Se não `entityId` for fornecido como um XID, esse campo deverá especificar a namespace de identidade. | `entityIdNE=email` |
| `relatedEntityId` | Se `schema.name` for &quot;_xdm.context.experience.event&quot;, esse valor deverá especificar a namespace de identidade da entidade do perfil relacionada. Esse valor segue as mesmas regras que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Se `schema.name` for &quot;_xdm.context.experience.event&quot;, esse valor deverá especificar a namespace de identidade para a entidade especificada em `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtros os dados retornados na resposta. Use-o para especificar quais valores de campo de schema incluir nos dados recuperados. Para vários campos, separe os valores por vírgula sem espaços entre | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifica a Política de Mesclagem pela qual os dados retornados serão controlados. Se um não for especificado na chamada, o padrão de sua organização para esse schema será usado. Se nenhuma Política de Mesclagem padrão tiver sido configurada, o padrão não será mesclagem de perfil e nenhuma identificação. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | A ordem de classificação dos eventos de experiência recuperados por carimbo de data e hora, gravado como `(+/-)timestamp` o padrão sendo `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Especifique a hora do start para filtrar objetos de série de tempo (em milissegundos). | `startTime=1539838505` |
| `endTime` | Especifique a hora de término para filtrar objetos de série de tempo (em milissegundos). | `endTime=1539838510` |
| `limit` | Valor numérico que especifica o número máximo de objetos a serem retornados. Padrão: 1000 | `limit=100` |
| `withCA` | Sinalizador de recurso para ativar atributos calculados para pesquisa. Padrão: false | `withCA=true` |