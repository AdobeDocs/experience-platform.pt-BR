---
keywords: Experience Platform; home; tópicos populares; assimilação de streaming; ingestão; dados de séries de tempo; dados de séries de tempo de fluxo;
solution: Experience Platform
title: Transmitir dados da série de tempo usando APIs de assimilação de fluxo
topic-legacy: tutorial
type: Tutorial
description: Este tutorial ajudará você a começar a usar APIs de assimilação de streaming, parte das APIs do serviço de assimilação de dados da Adobe Experience Platform.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 2%

---

# Transmitir dados da série de tempo usando APIs de assimilação de fluxo

Este tutorial ajudará você a começar a usar APIs de assimilação de streaming, parte das APIs [!DNL Data Ingestion Service] do Adobe Experience Platform.

## Introdução

Este tutorial requer um conhecimento prático de vários serviços da Adobe Experience Platform. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual  [!DNL Platform] organiza os dados de experiência.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Guia](../../xdm/api/getting-started.md) do desenvolvedor do Registro de Schema: Um guia abrangente que abrange cada um dos endpoints disponíveis da  [!DNL Schema Registry] API e como fazer chamadas para eles. Isso inclui conhecer seu `{TENANT_ID}`, que aparece nas chamadas em todo este tutorial, bem como saber como criar esquemas, que são usados na criação de um conjunto de dados para assimilação.

Além disso, este tutorial exige que você já tenha criado uma conexão de transmissão. Para obter mais informações sobre como criar uma conexão de transmissão, leia o [tutorial de conexão de transmissão](./create-streaming-connection.md).

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de assimilação de streaming.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Compor um esquema com base na classe XDM ExperienceEvent

Para criar um conjunto de dados, primeiro será necessário criar um novo esquema que implemente a classe [!DNL XDM ExperienceEvent] . Para obter mais informações sobre como criar schemas, leia o [Guia do desenvolvedor da API do Registro de Schema](../../xdm/api/getting-started.md).

**Formato da API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `title` | O nome que deseja usar para o esquema. Este nome deve ser exclusivo. |
| `description` | Uma descrição significativa para o esquema que você está criando. |
| `meta:immutableTags` | Neste exemplo, a tag `union` é usada para persistir seus dados em [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes do esquema recém-criado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados sejam namespacados corretamente e estejam contidos na Organização IMS. Para obter mais informações sobre a ID do locatário, leia o [guia do Registro do esquema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Anote os atributos `$id` e `version`, pois ambos serão usados ao criar seu conjunto de dados.

## Definir um descritor de identidade primário para o esquema

Em seguida, adicione um [descritor de identidade](../../xdm/api/descriptors.md) ao schema criado acima, usando o atributo de endereço de email de trabalho como o identificador principal. Isso resultará em duas alterações:

1. O endereço de email de trabalho se tornará um campo obrigatório. Isso significa que as mensagens enviadas sem esse campo falharão na validação e não serão assimiladas.

2. [!DNL Real-time Customer Profile] O usará o endereço de email como um identificador para ajudar a unir mais informações sobre esse indivíduo.

### Solicitação

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | O `$id` que você recebeu anteriormente ao compor o esquema. Deve ser algo como isto: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Códigos de Namespace de Identidade**
>
> Certifique-se de que os códigos sejam válidos - o exemplo acima usa &quot;email&quot; que é um namespace de identidade padrão. Outros namespaces de identidade padrão comumente usados podem ser encontrados nas [Perguntas frequentes do serviço de identidade](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Se quiser criar um namespace personalizado, siga as etapas descritas em [visão geral do namespace de identidade](../../identity-service/home.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com informações sobre o namespace de identidade primária recém-criado para o schema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Criar um conjunto de dados para dados de séries de tempo

Depois de criar o esquema, será necessário criar um conjunto de dados para assimilar dados de registro.

>[!NOTE]
>
>Esse conjunto de dados será ativado para **[!DNL Real-time Customer Profile]** e **[!DNL Identity]** ao definir as tags apropriadas.

**Formato da API**

```http
POST /catalog/dataSets
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 e uma matriz contendo a ID do conjunto de dados recém-criado no formato `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Assimilar dados da série de tempo à conexão de transmissão

Com o conjunto de dados e a conexão de transmissão no lugar, é possível assimilar registros JSON formatados em XDM para assimilar dados de séries de tempo em [!DNL Platform].

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão de transmissão recém-criada. |
| `synchronousValidation` | Um parâmetro de consulta opcional destinado a fins de desenvolvimento. Se definido como `true`, ele poderá ser usado para feedback imediato para determinar se a solicitação foi enviada com êxito. Por padrão, esse valor é definido como `false`. |

**Solicitação**

Inserir dados de séries de tempo em uma conexão de transmissão pode ser feita com ou sem o nome de origem.

A solicitação de exemplo abaixo assimila dados de séries de tempo com um nome de origem ausente na Plataforma. Se os dados não tiverem o nome de origem, ele adicionará a ID de origem da definição de conexão de transmissão.

>[!IMPORTANT]
>
>Você precisará gerar seus próprios `xdmEntity._id` e `xdmEntity.timestamp`. Uma boa maneira de gerar uma ID é usar a função UUID na Preparação de dados. Mais informações sobre a função UUID podem ser encontradas no [Guia de funções de preparação de dados](../../data-prep/functions.md). O atributo `xdmEntity._id` representa um identificador exclusivo para o próprio registro, **não** uma ID exclusiva da pessoa ou dispositivo cujo registro é. A ID de pessoa ou dispositivo será específica em qualquer atributo atribuído como um identificador de pessoa ou dispositivo do esquema.
>
>`xdmEntity._id` e `xdmEntity.timestamp` são os únicos campos obrigatórios para dados de séries de tempo. Além disso, a chamada da API a seguir **not** requer cabeçalhos de autenticação.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
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
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
            }
        }
    }
}'
```

Se você quiser incluir um nome de origem, o exemplo a seguir mostra como incluí-lo.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do recém-transmitido [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{CONNECTION_ID}` | A ID da conexão de transmissão criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerou no lado do servidor para o registro que você acabou de enviar. Essa ID ajuda o Adobe a rastrear o ciclo de vida desse registro em vários sistemas e com a depuração. |
| `receivedTimeMs`: Um carimbo de data e hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |
| `synchronousValidation.status` | Como o parâmetro de consulta `synchronousValidation=true` foi adicionado, esse valor será exibido. Se a validação tiver êxito, o status será `pass`. |

## Recuperar os dados de séries de tempo recém-assimilados

Para validar os registros assimilados anteriormente, você pode usar o [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar os dados da série de tempo. Isso pode ser feito usando uma solicitação GET para o endpoint `/access/entities` e parâmetros de consulta opcionais. Vários parâmetros podem ser usados, separados por &quot;E&quot; comercial (&amp;).&quot;

>[!NOTE]
>
>Se a ID da política de mesclagem não estiver definida e o `schema.name` ou `relatedSchema.name` for `_xdm.context.profile`, [!DNL Profile Access] buscará **todas** identidades relacionadas.

**Formato da API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `schema.name` | **Obrigatório.** O nome do schema que você está acessando. |
| `relatedSchema.name` | **Obrigatório.** Como você está acessando um  `_xdm.context.experienceevent`, esse valor especifica o schema para a entidade de perfil ao qual os eventos de série de tempo estão relacionados. |
| `relatedEntityId` | A ID da entidade relacionada. Se fornecido, você também deve fornecer o namespace da entidade. |
| `relatedEntityIdNS` | O namespace da ID que você está tentando recuperar. |

**Solicitação**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das entidades solicitadas. Como você pode ver, esses são os mesmos dados de séries de tempo que foram assimilados anteriormente.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Próximas etapas

Ao ler este documento, agora você entende como assimilar dados de registro em [!DNL Platform] usando conexões de transmissão. Você pode tentar fazer mais chamadas com valores diferentes e recuperar os valores atualizados. Além disso, você pode começar a monitorar seus dados assimilados por meio da interface do usuário [!DNL Platform]. Para obter mais informações, leia o guia [de monitoramento da assimilação de dados](../quality/monitor-data-ingestion.md).

Para obter mais informações sobre a assimilação de streaming em geral, leia a [visão geral da assimilação de streaming](../streaming-ingestion/overview.md).
