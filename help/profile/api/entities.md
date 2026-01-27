---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Endpoint da API de Entidades (Acesso ao Perfil)
type: Documentation
description: O Adobe Experience Platform permite acessar os dados do Perfil do cliente em tempo real usando as APIs RESTful ou a interface do usuário. Este guia descreve como acessar entidades, mais conhecidas como "perfis", usando a API de perfil.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 17bd3494c2d9b2a05ca86903297ebec85c9350f2
workflow-type: tm+mt
source-wordcount: '2290'
ht-degree: 3%

---

# Endpoint de entidades (Acesso ao perfil)

>[!IMPORTANT]
>
>Você pode **usar somente** esses pontos de extremidade se tiver o Real-Time CDP Ultimate.
>
>Se você tiver o Real-Time CDP Prime, poderá continuar a assimilar e usar eventos de experiência para casos de uso de personalização, bem como visualizar eventos na interface do usuário do Experience Platform, mas **não** poderá pesquisar de forma programática eventos de experiência usando a API.
>
>Se você tiver o Real-Time CDP Ultimate e **não** procurar eventos programaticamente no momento, entre em contato com o Atendimento ao cliente da Adobe para habilitar esse recurso.

O Adobe Experience Platform permite que você acesse dados do [!DNL Real-Time Customer Profile] usando APIs RESTful ou a interface do usuário. Este guia descreve como acessar entidades, mais conhecidas como &quot;perfis&quot;, usando a API. Para obter mais informações sobre como acessar perfis usando a interface do usuário do [!DNL Experience Platform], consulte o [Guia do usuário do perfil](../ui/user-guide.md).

## Introdução

O ponto de extremidade de API usado neste guia faz parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, consulte o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do [!DNL Experience Platform].

## Resolução da entidade

Como parte da atualização da arquitetura, a Adobe está introduzindo a resolução de entidades para Contas e Oportunidades, usando a correspondência de ID determinística com base nos dados mais recentes. O trabalho de resolução da entidade é executado diariamente durante a segmentação em lote, antes da avaliação de públicos-alvo de várias entidades com atributos B2B.

Esse aprimoramento permite que o Experience Platform identifique e unifique vários registros que representam a mesma entidade, melhorando a consistência dos dados e permitindo uma segmentação mais precisa do público-alvo.

Anteriormente, as Contas e Oportunidades dependiam da resolução baseada em gráfico de identidade que conectava as identidades, incluindo todas as assimilações históricas. Na nova abordagem de resolução de entidade, as identidades são vinculadas somente com base nos dados mais recentes.

- Conta e Oportunidade são entidades resolvidas com uma mesclagem baseada em precedência de tempo:
   - Conta: identidades usando o namespace `b2b_account`.
   - Oportunidade: identidades usando o namespace `b2b_opportunity`.
- Todas as outras entidades são simplesmente unificadas e somente as sobreposições de identidade primárias são mescladas com a mesclagem baseada em precedência de tempo.

>[!NOTE]
>
>A resolução da entidade somente oferece suporte a `b2b_account` e `b2b_opportunity`. As identidades de outros namespaces não são usadas na resolução da entidade. Se estiver usando namespaces personalizados, você não poderá encontrar contas e oportunidades.

### Como funciona a resolução da entidade?

- **Antes**: se um número DUNS (Sistema de Numeração Universal de Dados) foi usado como uma identidade adicional e o número DUNS da conta foi atualizado em um sistema de origem como o CRM, a ID da conta será vinculada a números DUNS antigos e novos.
- **Depois**: se o número DUNS foi usado como uma identidade adicional e o número DUNS da conta foi atualizado em um sistema de origem como um CRM, a ID da conta será vinculada somente ao novo número DUNS, refletindo assim o estado atual da conta com mais precisão.

Como resultado dessa atualização, a API [!DNL Profile Access] agora reflete a exibição do perfil de mesclagem mais recente após a conclusão de um ciclo de trabalho de resolução de entidade. Além disso, os dados consistentes fornecem casos de uso, como segmentação, ativação e análise, com precisão e consistência aprimoradas dos dados.

## Recuperar uma entidade {#retrieve-entity}

>[!IMPORTANT]
>
>As seguintes entidades B2B não são mais suportadas para solicitações de pesquisa por meio da API: **Relação Conta-Pessoa, Relação Oportunidade-Pessoa, Campanha, Membro de Campanha, Lista de Marketing e Membro da Lista de Marketing**.
>
>O suporte para essas entidades foi descontinuado. Se você tiver integrações ou fluxos de trabalho existentes que dependem do acesso a essas entidades, atualize-os para usar tipos de entidade compatíveis para garantir a funcionalidade contínua.

Você pode recuperar uma entidade de Perfil fazendo uma solicitação GET para o ponto de extremidade `/access/entities` junto com os parâmetros de consulta necessários.

>[!BEGINTABS]

>[!TAB Entidade de perfil]

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Os parâmetros de consulta fornecidos no caminho da solicitação especificam quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;).

Para acessar uma entidade Perfil, você **deve** fornecer os seguintes parâmetros de consulta:

- `schema.name`: o nome do esquema XDM da entidade. Nesse caso de uso, o `schema.name=_xdm.context.profile`.
- `entityId`: a ID da entidade que você está tentando recuperar.
- `entityIdNS`: O namespace da entidade que você está tentando recuperar. Este valor deve ser fornecido se `entityId` for **não** um XID.

Além disso, o uso do seguinte parâmetro de consulta é *altamente* recomendado:

- `mergePolicyId`: a ID da política de mesclagem com a qual você deseja filtrar os dados. Se nenhuma política de mesclagem for especificada, a política de mesclagem padrão da sua organização será usada.

Uma lista completa de parâmetros válidos é fornecida na seção [parâmetros de consulta](#query-parameters) do apêndice.

**Solicitação**

A solicitação a seguir recupera o email e o nome de um cliente usando uma identidade.

+++ Um exemplo de solicitação para recuperar uma entidade usando uma identidade

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com a entidade solicitada.

+++ Um exemplo de resposta que contém a entidade solicitada

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
                    "id": "johnsmith@example.com",
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

+++

>[!NOTE]
>
>Se um gráfico relacionado vincular mais de 50 identidades, esse serviço retornará o status HTTP 422 e a mensagem &quot;Muitas identidades relacionadas&quot;. Se você receber esse erro, considere adicionar mais parâmetros de consulta para restringir sua pesquisa.

>[!TAB Conta B2B]

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Os parâmetros de consulta fornecidos no caminho da solicitação especificam quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;).

Para acessar os dados da Conta B2B, você **deve** fornecer os seguintes parâmetros de consulta:

- `schema.name`: o nome do esquema XDM da entidade. Nesse caso de uso, esse valor é `schema.name=_xdm.context.account`.
- `entityId`: a ID da entidade que você está tentando recuperar.
- `entityIdNS`: O namespace da entidade que você está tentando recuperar. Este valor deve ser fornecido se `entityId` for **não** um XID.

Além disso, o uso do seguinte parâmetro de consulta é *altamente* recomendado:

- `mergePolicyId`: a ID da política de mesclagem com a qual você deseja filtrar os dados. Se nenhuma política de mesclagem for especificada, a política de mesclagem padrão da sua organização será usada.

Uma lista completa de parâmetros válidos é fornecida na seção [parâmetros de consulta](#query-parameters) do apêndice.

**Solicitação**

+++ Um exemplo de solicitação para recuperar uma conta B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com a entidade solicitada.

+++ Um exemplo de resposta que contém a entidade solicitada

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB Oportunidade B2B]

**Formato da API**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Os parâmetros de consulta fornecidos no caminho da solicitação especificam quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;).

Para acessar uma entidade de Oportunidade B2B, você **deve** fornecer os seguintes parâmetros de consulta:

- `schema.name`: o nome do esquema XDM da entidade. Nesse caso de uso, o `schema.name=_xdm.context.opportunity`.
- `entityId`: a ID da entidade que você está tentando recuperar.
- `entityIdNS`: O namespace da entidade que você está tentando recuperar. Este valor deve ser fornecido se `entityId` for **não** um XID.

Além disso, o uso do seguinte parâmetro de consulta é *altamente* recomendado:

- `mergePolicyId`: a ID da política de mesclagem com a qual você deseja filtrar os dados. Se nenhuma política de mesclagem for especificada, a política de mesclagem padrão da sua organização será usada.

Uma lista completa de parâmetros válidos é fornecida na seção [parâmetros de consulta](#query-parameters) do apêndice.

**Solicitação**

+++ Uma solicitação de amostra para recuperar uma entidade de oportunidade B2B

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com a entidade solicitada.

+++ Um exemplo de resposta que contém a entidade solicitada

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Recuperar várias entidades {#retrieve-entities}

Você pode recuperar várias entidades de Perfil fazendo uma solicitação POST para o ponto de extremidade `/access/entities` e fornecendo as identidades na carga.

>[!BEGINTABS]

>[!TAB Entidades de perfil]

**Formato da API**

```http
POST /access/entities
```

**Solicitação**

A solicitação a seguir recupera os nomes e endereços de email de vários clientes por uma lista de identidades.

+++Uma solicitação de amostra para recuperar várias entidades

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp"
      }'
```

| Propriedade | Tipo | Descrição |
| -------- |----- | ----------- |
| `schema.name` | String | **(Obrigatório)** O nome do esquema XDM ao qual a entidade pertence. |
| `fields` | Matriz | Os campos XDM a serem retornados, como uma matriz de cadeias de caracteres. Por padrão, todos os campos serão retornados. |
| `identities` | Matriz | **(Obrigatório)** Uma matriz contendo uma lista de identidades para as entidades que você deseja acessar. |
| `identities.entityId` | String | A ID de uma entidade que você deseja acessar. |
| `identities.entityIdNS.code` | String | O namespace de uma ID de entidade que você deseja acessar. |
| `timeFilter.startTime` | Número inteiro | Especifica a hora de início para filtrar entidades de Perfil (em milissegundos). Por padrão, esse valor é definido como o início do tempo disponível. |
| `timeFilter.endTime` | Número inteiro | Especifica a hora final para filtrar entidades de Perfil (em milissegundos). Por padrão, esse valor é definido como o fim do tempo disponível. |
| `limit` | Número inteiro | O número máximo de registros para retornar. Por padrão, esse valor é definido como 1000. |
| `orderby` | String | A ordem de classificação dos eventos de experiência recuperados por carimbo de data/hora, gravados como `(+/-)timestamp`, sendo o padrão `+timestamp`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com os campos solicitados das entidades especificadas no corpo da solicitação.

+++ Um exemplo de resposta que contém as entidades solicitadas

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

+++

>[!TAB Conta B2B]

**Formato da API**

```http
POST /access/entities
```

**Solicitação**

A solicitação a seguir recupera as contas B2B solicitadas.

+++Uma solicitação de amostra para recuperar várias entidades

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Propriedade | Tipo | Descrição |
| -------- |----- | ----------- |
| `schema.name` | String | **(Obrigatório)** O nome do esquema XDM ao qual a entidade pertence. |
| `identities` | Matriz | **(Obrigatório)** Uma matriz contendo uma lista de identidades para as entidades que você deseja acessar. |
| `identities.entityId` | String | A ID de uma entidade que você deseja acessar. |
| `identities.entityIdNS.code` | String | O namespace de uma ID de entidade que você deseja acessar. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com as entidades solicitadas.

+++ Um exemplo de resposta que contém as entidades solicitadas

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB Oportunidade B2B]

**Formato da API**

```http
POST /access/entities
```

**Solicitação**

A solicitação a seguir recupera as oportunidades B2B solicitadas.

+++ Uma solicitação de amostra para recuperar várias entidades

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Propriedade | Tipo | Descrição |
| -------- |----- | ----------- |
| `schema.name` | String | **(Obrigatório)** O nome do esquema XDM ao qual a entidade pertence. |
| `identities` | Matriz | **(Obrigatório)** Uma matriz contendo uma lista de identidades para as entidades que você deseja acessar. |
| `identities.entityId` | String | A ID de uma entidade que você deseja acessar. |
| `identities.entityIdNS.code` | String | O namespace de uma ID de entidade que você deseja acessar. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com as entidades solicitadas.

+++ Um exemplo de resposta que contém as entidades solicitadas

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Acessar uma página subsequente de resultados

Os resultados são paginados ao recuperar eventos de série temporal. Se houver páginas subsequentes de resultados, a propriedade `_page.next` conterá uma ID. Além disso, a propriedade `_links.next.href` fornece um URI de solicitação para recuperar a próxima página. Para recuperar os resultados, faça outra solicitação GET para o ponto de extremidade `/access/entities` e substitua `/entities` pelo valor do URI fornecido.

>[!NOTE]
>
>Certifique-se de não repetir `/entities/` acidentalmente no caminho da solicitação. Só deve aparecer uma vez como, `/access/entities?start=...`

**Formato da API**

```http
GET /access/{NEXT_URI}
```

| Parâmetro | Descrição |
|---|---|
| `{NEXT_URI}` | O valor do URI retirado de `_links.next.href`. |

**Solicitação**

A solicitação a seguir recupera a próxima página de resultados usando o URI `_links.next.href` como o caminho da solicitação.

+++ Um exemplo de solicitação para acessar a próxima página de resultados

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna a próxima página de resultados. Esta resposta não tem páginas subsequentes de resultados, conforme indicado pelos valores de cadeia de caracteres vazios de `_page.next` e `_links.next.href`.

+++ Um exemplo de resposta que contém a próxima página de entidades

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

+++

## Excluir uma entidade {#delete-entity}

>[!IMPORTANT]
>
>O ponto de extremidade da entidade de exclusão será descontinuado até o final de outubro de 2025. Se você deseja executar operações de exclusão de registro, é possível usar o [fluxo de trabalho da API de exclusão de registro do ciclo de vida dos dados](/help/hygiene/api/workorder.md) ou o [fluxo de trabalho da interface do usuário para exclusão de registro do ciclo de vida dos dados](/help/hygiene/ui/record-delete.md).
>
>Além disso, as solicitações de exclusão das seguintes entidades B2B já foram descontinuadas:
>
>- Conta
>- Relação Conta-Pessoa
>- Oportunidade
>- Relação oportunidade-pessoa
>- Campaign
>- Membro da campanha
>- Lista de marketing
>- Membros da lista de marketing

Você pode excluir uma entidade do Repositório de Perfis fazendo uma solicitação DELETE para o ponto de extremidade `/access/entities` junto com os parâmetros de consulta necessários.

**Formato da API**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

Os parâmetros de consulta fornecidos no caminho da solicitação especificam quais dados acessar. É possível incluir vários parâmetros, separados por &quot;E&quot; comercial (&amp;).

Para excluir uma entidade, você **deve** fornecer os seguintes parâmetros de consulta:

- `schema.name`: o nome do esquema XDM da entidade. Neste caso de uso, você pode **usar somente** `schema.name=_xdm.context.profile`.
- `entityId`: a ID da entidade que você está tentando recuperar.
- `entityIdNS`: O namespace da entidade que você está tentando recuperar. Este valor deve ser fornecido se `entityId` for **não** um XID.
- `mergePolicyId`: a ID da política de mesclagem da entidade. A política de mesclagem contém informações sobre identificação de identidade e mesclagem de objetos XDM de valor-chave. Se esse valor não for fornecido, a política de mesclagem padrão será usada.

**Solicitação**

A solicitação a seguir exclui a entidade especificada.

+++ Um exemplo de solicitação para excluir uma entidade

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 202 com um corpo de resposta vazio.

## Próximas etapas

Seguindo este guia, você acessou com êxito [!DNL Real-Time Customer Profile] dados de campos de dados, perfis e séries de tempo. Para saber como acessar outros recursos de dados armazenados no [!DNL Experience Platform], consulte a [visão geral sobre Acesso a Dados](../../data-access/home.md).

## Apêndice {#appendix}

A seção a seguir fornece informações adicionais sobre o acesso aos dados do [!DNL Profile] usando a API.

### Parâmetros de consulta {#query-parameters}

Os parâmetros a seguir são usados no caminho para solicitações GET para o ponto de extremidade `/access/entities`. Eles servem para identificar a entidade de perfil que você deseja acessar e filtrar os dados retornados na resposta. Os parâmetros obrigatórios são rotulados, enquanto o restante é opcional.

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `schema.name` | **(Obrigatório)** O nome do esquema XDM da entidade. | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | Se `schema.name` for `_xdm.context.experienceevent`, esse valor **deverá** especificar o esquema para a entidade de perfil à qual os eventos de série temporal estão relacionados. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Obrigatório)** A ID da entidade. Se o valor desse parâmetro não for um XID, também deverá ser fornecido um parâmetro de namespace de identidade (`entityIdNS`). | `entityId=janedoe@example.com` |
| `entityIdNS` | Se `entityId` não for fornecido como um XID, este campo **deve** especificar o namespace de identidade. | `entityIdNS=email` |
| `relatedEntityId` | Se `schema.name` for `_xdm.context.experienceevent`, esse valor **deverá** especificar a ID da entidade de perfil relacionada. Este valor segue as mesmas regras que `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Se `schema.name` for &quot;_xdm.context.experienceevent&quot;, esse valor deverá especificar o namespace de identidade da entidade especificada em `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtra os dados retornados na resposta. Use isso para especificar quais valores de campo de esquema incluir nos dados recuperados. Para vários campos, separe os valores por vírgula sem espaços entre eles. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | *Recomendado* Identifica a política de mesclagem pela qual controlar os dados retornados. Se um não for especificado na chamada, o padrão de sua organização para esse esquema será usado. Se nenhuma política de mesclagem padrão tiver sido definida para o esquema solicitado, a API retornará um código de status de erro HTTP 422. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | A ordem de classificação das entidades recuperadas por carimbo de data e hora. Isso é gravado como `(+/-)timestamp`, com o padrão sendo `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Especifica a hora de início para filtrar as entidades (em milissegundos). | `startTime=1539838505` |
| `endTime` | Especifica a hora final para filtrar entidades (em milissegundos). | `endTime=1539838510` |
| `limit` | Especifica o número máximo de entidades para retornar. Por padrão, esse valor é definido como 1000. | `limit=100` |
| `property` | Filtra pelo valor da propriedade. Esse parâmetro de consulta oferece suporte aos seguintes avaliadores: =, !=, &lt;, &lt;=, >, >=. Isso só pode ser usado com eventos de experiência, com no máximo três propriedades compatíveis. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
