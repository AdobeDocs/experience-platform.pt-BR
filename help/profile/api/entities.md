---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Endpoint da API de Entidades (Acesso ao Perfil)
type: Documentation
description: O Adobe Experience Platform permite acessar os dados do Perfil do cliente em tempo real usando as APIs RESTful ou a interface do usuário. Este guia descreve como acessar entidades, mais conhecidas como "perfis", usando a API de perfil.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 2%

---

# Endpoint de entidades (Acesso ao perfil)

O Adobe Experience Platform permite que você acesse dados do [!DNL Real-Time Customer Profile] usando APIs RESTful ou a interface do usuário. Este guia descreve como acessar entidades, mais conhecidas como &quot;perfis&quot;, usando a API. Para obter mais informações sobre como acessar perfis usando a interface do usuário do [!DNL Platform], consulte o [Guia do usuário do perfil](../ui/user-guide.md).

## Introdução

O ponto de extremidade de API usado neste guia faz parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Acessar dados do perfil por identidade

Você pode acessar uma entidade [!DNL Profile] fazendo uma solicitação GET para o ponto de extremidade `/access/entities` e fornecendo a identidade da entidade como uma série de parâmetros de consulta. Esta identidade consiste em um valor de ID (`entityId`) e o namespace de identidade (`entityIdNS`).

Os parâmetros de consulta fornecidos no caminho da solicitação especificam quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;). Uma lista completa de parâmetros válidos é fornecida na seção [parâmetros de consulta](#query-parameters) do apêndice.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>
>Se um gráfico relacionado vincular mais de 50 identidades, esse serviço retornará o status HTTP 422 e a mensagem &quot;Muitas identidades relacionadas&quot;. Se você receber esse erro, considere adicionar mais parâmetros de consulta para restringir sua pesquisa.

## Acessar dados do perfil por lista de identidades

Você pode acessar várias entidades de perfil por suas identidades fazendo uma solicitação POST para o ponto de extremidade `/access/entities` e fornecendo as identidades na carga. Essas identidades consistem em um valor de ID (`entityId`) e um namespace de identidade (`entityIdNS`).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schema.name` | ***(Obrigatório)*** O nome do esquema XDM ao qual a entidade pertence. |
| `fields` | Os campos XDM a serem retornados, como uma matriz de cadeias de caracteres. Por padrão, todos os campos serão retornados. |
| `identities` | ***(Obrigatório)*** Uma matriz contendo uma lista de identidades para as entidades que você deseja acessar. |
| `identities.entityId` | A ID de uma entidade que você deseja acessar. |
| `identities.entityIdNS.code` | O namespace de uma ID de entidade que você deseja acessar. |
| `timeFilter.startTime` | Hora inicial do filtro de intervalo de tempo, incluída. Deve estar na granularidade de milissegundos. O padrão, se não especificado, é o início do tempo disponível. |
| `timeFilter.endTime` | Filtro de intervalo de hora de término excluído. Deve estar na granularidade de milissegundos. O padrão, se não especificado, é o fim do tempo disponível. |
| `limit` | Número de registros a retornar. Somente se aplica ao número de eventos de experiência retornados. Padrão: 1.000. |
| `orderby` | A ordem de classificação dos eventos de experiência recuperados por carimbo de data/hora, gravados como `(+/-)timestamp`, sendo o padrão `+timestamp`. |
| `withCA` | Sinalizador de recurso para habilitar atributos computados para pesquisa. Padrão: falso. |

**Resposta**
Uma resposta bem-sucedida retorna os campos solicitados das entidades especificadas no corpo da solicitação.

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

## Acessar eventos de série temporal para um perfil por identidade

Você pode acessar eventos de série temporal pela identidade da entidade de perfil associada fazendo uma solicitação GET para o ponto de extremidade `/access/entities`. Esta identidade consiste em um valor de ID (`entityId`) e um namespace de identidade (`entityIdNS`).

Os parâmetros de consulta fornecidos no caminho da solicitação especificam quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;). Uma lista completa de parâmetros válidos é fornecida na seção [parâmetros de consulta](#query-parameters) do apêndice.

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitação**

A solicitação a seguir encontra uma entidade de perfil por ID e recupera os valores das propriedades `endUserIDs`, `web` e `channel` para todos os eventos de série temporal associados à entidade.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de eventos de série temporal e campos associados que foram especificados nos parâmetros de consulta de solicitação.

>[!NOTE]
>
>A solicitação especificou um limite de um (`limit=1`), portanto, o `count` na resposta abaixo é 1 e apenas uma entidade é retornada.

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

Os resultados são paginados ao recuperar eventos de série temporal. Se houver páginas subsequentes de resultados, a propriedade `_page.next` conterá uma ID. Além disso, a propriedade `_links.next.href` fornece um URI de solicitação para recuperar a próxima página. Para recuperar os resultados, faça outra solicitação GET para o ponto de extremidade `/access/entities`. No entanto, substitua `/entities` pelo valor do URI fornecido.

>[!NOTE]
>
>Certifique-se de não repetir acidentalmente `/entities/` no caminho da solicitação. Só deve aparecer uma vez como, `/access/entities?start=...`

**Formato da API**

```http
GET /access/{NEXT_URI}
```

| Parâmetro | Descrição |
|---|---|
| `{NEXT_URI}` | O valor do URI retirado de `_links.next.href`. |

**Solicitação**

A solicitação a seguir recupera a próxima página de resultados usando o URI `_links.next.href` como o caminho da solicitação.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna a próxima página de resultados. Esta resposta não tem páginas subsequentes de resultados, conforme indicado pelos valores de cadeia de caracteres vazios de `_page.next` e `_links.next.href`.

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

## Acessar eventos de série temporal para vários perfis por identidades

Você pode acessar eventos de série temporal de vários perfis associados fazendo uma solicitação POST para o ponto de extremidade `/access/entities` e fornecendo as identidades de perfil na carga. Cada uma dessas identidades consiste em um valor de ID (`entityId`) e um namespace de identidade (`entityIdNS`).

**Formato da API**

```http
POST /access/entities
```

**Solicitação**

A solicitação a seguir recupera IDs de usuário, horários locais e códigos de país para eventos de série temporal associados a uma lista de identidades de perfil:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schema.name` | **(OBRIGATÓRIO)** O esquema XDM da entidade a ser recuperada |
| `relatedSchema.name` | Se `schema.name` for `_xdm.context.experienceevent` esse valor deverá especificar o esquema para a entidade de perfil à qual os eventos de série temporal estão relacionados. |
| `identities` | **(OBRIGATÓRIO)** Uma lista de matriz de perfis da qual recuperar eventos de série temporal associados. Cada entrada na matriz é definida de uma das seguintes formas: 1) usando uma identidade totalmente qualificada que consiste no valor de ID e no namespace ou 2) fornecendo um XID. |
| `fields` | Isole os dados retornados a um conjunto especificado de campos. Use isso para filtrar quais campos de esquema são incluídos nos dados recuperados. Exemplo: personalEmail,person.name,person.gender |
| `mergePolicyId` | Identifica a Política de mesclagem pela qual controlar os dados retornados. Se um não for especificado na chamada de serviço, o padrão de sua organização para esse esquema será usado. Se nenhuma Política de mesclagem padrão tiver sido configurada, o padrão será sem mesclagem de perfis e sem compilação de identidades. |
| `orderby` | A ordem de classificação dos eventos de experiência recuperados por carimbo de data/hora, gravados como `(+/-)timestamp`, sendo o padrão `+timestamp`. |
| `timeFilter.startTime` | Especifique a hora inicial para filtrar objetos de série temporal (em milissegundos). |
| `timeFilter.endTime` | Especifique a hora final para filtrar objetos de série temporal (em milissegundos). |
| `limit` | Valor numérico especificando o número máximo de objetos a serem retornados. Padrão: 1000 |
| `withCA` | Sinalizador de recurso para habilitar atributos computados para pesquisa. Padrão: falso |

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de eventos de série temporal associados aos vários perfis especificados na solicitação.

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

Nesta resposta de exemplo, o primeiro perfil listado (&quot;GkouAW-yD9aoRCPhRYROJ-TestAFW&quot;) fornece um valor para `_links.next.payload`, o que significa que há páginas adicionais de resultados para este perfil. Consulte a seguinte seção sobre [acesso a resultados adicionais](#access-additional-results) para obter detalhes sobre como acessar esses resultados adicionais.

### Acessar resultados adicionais {#access-additional-results}

Ao recuperar eventos de séries de tempo, pode haver muitos resultados sendo retornados, portanto, os resultados geralmente são paginados. Se houver páginas subsequentes de resultados para um perfil específico, o valor `_links.next.payload` desse perfil conterá um objeto de carga.

Usando essa carga no corpo da solicitação, você pode executar uma solicitação POST adicional para o ponto de extremidade `access/entities` a fim de recuperar a página subsequente de dados de série temporal para esse perfil.

## Acessar eventos de série temporal em várias entidades de esquema

Você pode acessar várias entidades conectadas por meio de um descritor de relacionamento. O exemplo de chamada de API a seguir presume que uma relação já foi definida entre dois esquemas. Para obter mais informações sobre descritores de relacionamento, leia o [!DNL Schema Registry] guia do desenvolvedor da API [guia de ponto de extremidade de descritores](../../xdm/api/descriptors.md).

Você pode incluir parâmetros de consulta no caminho da solicitação para especificar quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;). Uma lista completa de parâmetros válidos é fornecida na seção [parâmetros de consulta](#query-parameters) do apêndice.

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Solicitação**

A solicitação a seguir recupera uma entidade contendo um descritor de relacionamento estabelecido anteriormente para acessar informações em diferentes esquemas.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista paginada de eventos de série temporal associados às várias entidades.

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

Os resultados são paginados ao recuperar eventos de série temporal. Se houver páginas subsequentes de resultados, a propriedade `_page.next` conterá uma ID. Além disso, a propriedade `_links.next.href` fornece um URI de solicitação para recuperar a página subsequente fazendo solicitações adicionais do GET para o ponto de extremidade `access/entities`.

## Próximas etapas

Seguindo este guia, você acessou com êxito [!DNL Real-Time Customer Profile] dados de campos de dados, perfis e séries de tempo. Para saber como acessar outros recursos de dados armazenados no [!DNL Platform], consulte a [visão geral sobre Acesso a Dados](../../data-access/home.md).

## Apêndice {#appendix}

A seção a seguir fornece informações adicionais sobre o acesso aos dados do [!DNL Profile] usando a API.

### Parâmetros de consulta {#query-parameters}

Os parâmetros a seguir são usados no caminho para solicitações GET para o ponto de extremidade `/access/entities`. Eles servem para identificar a entidade de perfil que você deseja acessar e filtrar os dados retornados na resposta. Os parâmetros obrigatórios são rotulados, enquanto o restante é opcional.

| Parâmetro | Descrição | Exemplo |
|---|---|---|
| `schema.name` | **(OBRIGATÓRIO)** O esquema XDM da entidade a ser recuperada | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Se `schema.name` for &quot;_xdm.context.experienceevent&quot;, esse valor deverá especificar o esquema da entidade de perfil à qual os eventos de série temporal estão relacionados. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(OBRIGATÓRIO)** A ID da entidade. Se o valor desse parâmetro não for um XID, também deverá ser fornecido um parâmetro de namespace de identidade (consulte `entityIdNS` abaixo). | `entityId=janedoe@example.com` |
| `entityIdNS` | Se `entityId` não for fornecido como um XID, este campo deverá especificar o namespace de identidade. | `entityIdNE=email` |
| `relatedEntityId` | Se `schema.name` for &quot;_xdm.context.experienceevent&quot;, esse valor deverá especificar o namespace de identidade da entidade de perfil relacionada. Este valor segue as mesmas regras que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Se `schema.name` for &quot;_xdm.context.experienceevent&quot;, esse valor deverá especificar o namespace de identidade da entidade especificada em `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtra os dados retornados na resposta. Use isso para especificar quais valores de campo de esquema incluir nos dados recuperados. Para vários campos, separe os valores por vírgula sem espaços entre | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifica a Política de mesclagem pela qual controlar os dados retornados. Se um não for especificado na chamada, o padrão de sua organização para esse esquema será usado. Se nenhuma Política de mesclagem padrão tiver sido configurada, o padrão será sem mesclagem de perfis e sem compilação de identidades. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | A ordem de classificação dos eventos de experiência recuperados por carimbo de data/hora, gravados como `(+/-)timestamp`, sendo o padrão `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Especifique a hora inicial para filtrar objetos de série temporal (em milissegundos). | `startTime=1539838505` |
| `endTime` | Especifique a hora final para filtrar objetos de série temporal (em milissegundos). | `endTime=1539838510` |
| `limit` | Valor numérico especificando o número máximo de objetos a serem retornados. Padrão: 1000 | `limit=100` |
| `property` | Filtra pelo valor da propriedade. Oferece suporte aos seguintes avaliadores: =, !=, &lt;, &lt;=, >, >=. Só podem ser usados com eventos de experiência, com no máximo três propriedades compatíveis. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | Sinalizador de recurso para habilitar atributos computados para pesquisa. Padrão: falso | `withCA=true` |
