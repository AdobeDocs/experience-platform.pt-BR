---
keywords: Experience Platform;página inicial;tópicos populares;assimilação por transmissão;assimilação;dados de série temporal;transmitir dados de série temporal;
solution: Experience Platform
title: Transmitir dados de série temporal usando APIs de assimilação de fluxo
type: Tutorial
description: Este tutorial ajudará você a começar a usar as APIs de assimilação de fluxo, parte das APIs de serviço de assimilação de dados da Adobe Experience Platform.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---

# Transmitir dados de série temporal usando APIs de assimilação de fluxo

Este tutorial ajudará você a começar a usar as APIs de assimilação de streaming, parte das APIs do Adobe Experience Platform [!DNL Data Ingestion Service].

## Introdução

Este tutorial requer um conhecimento prático de vários serviços da Adobe Experience Platform. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de múltiplas fontes.
- [Guia do desenvolvedor do Registro de Esquema](../../xdm/api/getting-started.md): um guia abrangente que cobre cada um dos pontos de extremidade disponíveis da API [!DNL Schema Registry] e como fazer chamadas para eles. Isso inclui conhecer seu `{TENANT_ID}`, que aparece em chamadas neste tutorial, bem como saber como criar esquemas, que é usado na criação de um conjunto de dados para assimilação.

Além disso, este tutorial requer que você já tenha criado uma conexão de transmissão. Para obter mais informações sobre como criar uma conexão de streaming, leia o [tutorial Criar uma conexão de streaming](./create-streaming-connection.md).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../landing/api-guide.md).

## Compor um esquema com base na classe XDM ExperienceEvent

Para criar um conjunto de dados, primeiro será necessário criar um novo esquema que implemente a classe [!DNL XDM ExperienceEvent]. Para obter mais informações sobre como criar esquemas, leia o [guia do desenvolvedor da API do Registro de Esquemas](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `title` | O nome que você deseja usar para o esquema. Esse nome deve ser exclusivo. |
| `description` | Uma descrição significativa do esquema que você está criando. |
| `meta:immutableTags` | Neste exemplo, a tag `union` é usada para manter seus dados em [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

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
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. Para obter mais informações sobre a ID do Locatário, leia o [guia de registro de esquema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Anote os atributos `$id` e `version`, pois ambos serão usados ao criar seu conjunto de dados.

## Definir um descritor de identidade primário para o esquema

Em seguida, adicione um [descritor de identidade](../../xdm/api/descriptors.md) ao esquema criado acima, usando o atributo de endereço de email de trabalho como o identificador principal. Isso resultará em duas alterações:

1. O endereço de email comercial se tornará um campo obrigatório. Isso significa que as mensagens enviadas sem esse campo terão falha na validação e não serão assimiladas.

2. [!DNL Real-Time Customer Profile] usará o endereço de email comercial como um identificador para ajudar a compilar mais informações sobre esse indivíduo.

### Solicitação

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | O `$id` que você recebeu anteriormente quando compôs o esquema. Deve ser mais ou menos assim: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**Códigos de Namespace de Identidade**
>
> Verifique se os códigos são válidos - o exemplo acima usa &quot;email&quot;, que é um namespace de identidade padrão. Outros namespaces de identidade padrão comumente usados podem ser encontrados nas [Perguntas frequentes sobre o Serviço de Identidade](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Se quiser criar um namespace personalizado, siga as etapas descritas em [visão geral sobre namespace de identidade](../../identity-service/home.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com informações sobre o namespace de identidade primário recém-criado para o esquema.

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
    "imsOrg": "{ORG_ID}"
}
```

## Criar um conjunto de dados para dados de série temporal

Depois de criar o esquema, será necessário criar um conjunto de dados para assimilar dados de registro.

>[!NOTE]
>
>Este conjunto de dados será habilitado para **[!DNL Real-Time Customer Profile]** e **[!DNL Identity]** definindo as marcas apropriadas.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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


## Criar uma conexão de streaming

Depois de criar o esquema e o conjunto de dados, será necessário criar uma conexão de transmissão para assimilar seus dados.

Para obter mais informações sobre como criar uma conexão de streaming, leia o [tutorial Criar uma conexão de streaming](./create-streaming-connection.md).

## Assimilar dados de série temporal à conexão de transmissão

Com o conjunto de dados, a conexão de transmissão e o fluxo de dados criados, você pode assimilar registros JSON formatados em XDM para assimilar dados de série temporal em [!DNL Experience Platform].

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da sua conexão de streaming recém-criada. |
| `syncValidation` | Um parâmetro de consulta opcional destinado a fins de desenvolvimento. Se definido como `true`, ele pode ser usado para feedback imediato para determinar se a solicitação foi enviada com êxito. Por padrão, esse valor está definido como `false`. Observe que se você definir este parâmetro de consulta como `true`, a solicitação será limitada a 60 vezes por minuto por `CONNECTION_ID`. |

**Solicitação**

A assimilação de dados de série temporal em uma conexão de streaming pode ser feita com ou sem o nome de origem.

A solicitação de exemplo abaixo assimila dados de série temporal com um nome de origem ausente na Experience Platform. Se o nome de origem dos dados estiver ausente, ele adicionará a ID de origem da definição da conexão de streaming.

`xdmEntity._id` e `xdmEntity.timestamp` são campos obrigatórios para dados de série temporal. O atributo `xdmEntity._id` representa um identificador exclusivo do próprio registro, **não**, uma ID exclusiva da pessoa ou dispositivo cujo registro é.

Você precisará gerar seus próprios `xdmEntity._id` e `xdmEntity.timestamp` para o registro de uma forma que permaneça consistente se o registro precisar ser assimilado novamente. Idealmente, o sistema de origem conterá esses valores. Se uma ID não estiver disponível, considere concatenar valores de outros campos no registro para criar um valor exclusivo que possa ser gerado novamente de forma consistente a partir do registro na reassimilação.

>[!NOTE]
>
>A chamada de API a seguir **não** requer cabeçalhos de autenticação.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
    "datasetId": "{DATASET_ID}",
    "flowId": "{FLOW_ID}",
    "imsOrgID": "{ORG_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            },
        "identityMap": {
                "Email": [
                  {
                    "id": "acme_user@gmail.com",
                    "primary": true
                  }
                ]
              },
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
    "datasetId": "{DATASET_ID}",
    "flowId": "{FLOW_ID}",
    "imsOrgID": "{ORG_ID}",
      "source": {
        "name": "ACME source"
      }
    }
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do [!DNL Profile] recém-transmitido.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{CONNECTION_ID}` | O `inletId` da conexão de streaming criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerado no lado do servidor para o registro que você acabou de enviar. Essa ID ajuda a Adobe a rastrear o ciclo de vida desse registro por vários sistemas e com depuração. |
| `receivedTimeMs`: Um carimbo de data/hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |  |
| `syncValidation.status` | Como o parâmetro de consulta `syncValidation=true` foi adicionado, este valor aparecerá. Se a validação tiver êxito, o status será `pass`. |

## Recuperar os dados de série temporal recém-assimilados

Para validar os registros assimilados anteriormente, você pode usar o [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar os dados da série temporal. Isso pode ser feito usando uma solicitação GET para o ponto de extremidade `/access/entities` e usando parâmetros de consulta opcionais. Vários parâmetros podem ser usados, separados por &quot;E&quot; comercial (&amp;).&quot;

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
| `schema.name` | **Obrigatório.** O nome do esquema que você está acessando. |
| `relatedSchema.name` | **Obrigatório.** Como você está acessando um `_xdm.context.experienceevent`, esse valor especifica o esquema da entidade de perfil à qual os eventos de série temporal estão relacionados. |
| `relatedEntityId` | A ID da entidade relacionada. Se fornecido, você também deve fornecer o namespace da entidade. |
| `relatedEntityIdNS` | O namespace da ID que você está tentando recuperar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das entidades solicitadas. Como você pode ver, esses são os mesmos dados de série temporal que foram assimilados anteriormente.

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

Após a leitura deste documento, você entende como assimilar dados de registro no [!DNL Experience Platform] usando conexões de streaming. Você pode tentar fazer mais chamadas com valores diferentes e recuperar os valores atualizados. Além disso, você pode começar a monitorar os dados assimilados por meio da interface do usuário do [!DNL Experience Platform]. Para obter mais informações, leia o [guia de assimilação de dados de monitoramento](../quality/monitor-data-ingestion.md).

Para obter mais informações sobre a assimilação por transmissão em geral, leia a [visão geral da assimilação por transmissão](../streaming-ingestion/overview.md).
