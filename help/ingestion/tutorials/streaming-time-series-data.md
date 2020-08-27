---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Transmissão de dados de séries temporais
topic: tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 2%

---


# Transmitir dados de séries de tempo para o Adobe Experience Platform

Este tutorial o ajudará a começar a usar APIs de ingestão de streaming, parte das [!DNL Data Ingestion Service] APIs do Adobe Experience Platform.

## Introdução

Este tutorial requer um conhecimento prático de vários serviços da Adobe Experience Platform. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado através do qual [!DNL Platform] organiza os dados da experiência.
- [[!DNL Perfil do cliente em tempo real]](../../profile/home.md): Fornece um perfil unificado e de consumidor em tempo real, com base em dados agregados de várias fontes.
- [Guia](../../xdm/api/getting-started.md)do desenvolvedor do Registro do schema: Um guia abrangente que abrange cada um dos pontos finais disponíveis da [!DNL Schema Registry] API e como fazer chamadas para eles. Isso inclui conhecer seu `{TENANT_ID}`, que aparece em chamadas ao longo deste tutorial, bem como saber como criar schemas, que são usados na criação de um conjunto de dados para ingestão.

Além disso, este tutorial requer que você já tenha criado uma conexão de streaming. Para obter mais informações sobre como criar uma conexão de streaming, leia o tutorial [](./create-streaming-connection.md)Criar uma conexão de streaming.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de ingestão de streaming.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Compor um schema com base na classe XDM ExperienceEvent

Para criar um conjunto de dados, primeiro será necessário criar um novo schema que implemente a [!DNL XDM ExperienceEvent] classe. Para obter mais informações sobre como criar schemas, leia o guia [do desenvolvedor da API do Registro do](../../xdm/api/getting-started.md)Schema.

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
| `title` | O nome que você deseja usar para o seu schema. Esse nome deve ser exclusivo. |
| `description` | Uma descrição significativa do schema que você está criando. |
| `meta:immutableTags` | Neste exemplo, a `union` tag é usada para persistir seus dados em [[!DNL Real-time Customer Perfil]](../../profile/home.md). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes do schema recém-criado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "{SCHEMA_VERSION}",
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
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. Para obter mais informações sobre a ID do locatário, leia o guia [do Registro do](../../xdm/api/getting-started.md#know-your-tenant-id)schema. |

Anote os atributos `$id` e os `version` atributos, pois ambos serão usados ao criar seu conjunto de dados.

## Definir um descritor de identidade primário para o schema

Em seguida, adicione um descritor [de](../../xdm/api/descriptors.md) identidade ao schema criado acima, usando o atributo de endereço de email de trabalho como o identificador principal. Isso resultará em duas alterações:

1. O endereço de email de trabalho se tornará um campo obrigatório. Isso significa que as mensagens enviadas sem esse campo falharão na validação e não serão ingeridas.

2. [!DNL Real-time Customer Profile] usará o endereço de email como um identificador para ajudar a juntar mais informações sobre esse indivíduo.

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
| `{SCHEMA_REF_ID}` | O `$id` que você recebeu anteriormente ao compor o schema. Deve ser algo parecido com isto: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; códigos de Namespace de **identidade &#x200B;**
>
> Certifique-se de que os códigos sejam válidos - o exemplo acima usa &quot;email&quot;, que é uma namespace de identidade padrão. Outras namespaces de identidade padrão comumente usadas podem ser encontradas nas Perguntas frequentes [do Serviço de](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)identidade.
>
> Se você quiser criar uma namespace personalizada, siga as etapas descritas na visão geral [da namespace de](../../identity-service/home.md)identidade.
**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com informações sobre a namespace de identidade primária recém-criada para o schema.

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

Depois de criar o schema, será necessário criar um conjunto de dados para assimilar os dados do registro.

>[!NOTE]
>
>Esse conjunto de dados será ativado para **[!DNL Real-time Customer Profile]** e **[!DNL Identity]** definindo as tags apropriadas.

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
        "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 e uma matriz que contém a ID do conjunto de dados recém-criado no formato `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## Ingressar dados de série cronológica na conexão de streaming

Com o conjunto de dados e a conexão de streaming ativada, você pode assimilar registros JSON formatados em XDM para assimilar dados de séries de tempo no [!DNL Platform].

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O `id` valor da sua conexão de streaming recém-criada. |
| `synchronousValidation` | Um parâmetro opcional de query destinado a fins de desenvolvimento. Se definido como `true`, ele pode ser usado para feedback imediato para determinar se a solicitação foi enviada com êxito. Por padrão, esse valor é definido como `false`. |

**Solicitação**

>[!NOTE]
>
>Você precisará gerar o seu próprio `xdmEntity._id` e `xdmEntity.timestamp`. Uma boa maneira de gerar uma ID é usar uma UUID. Além disso, a chamada de API a seguir **não** requer cabeçalhos de autenticação.


```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do novo streaming [!DNL Profile].

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
| `{CONNECTION_ID}` | A ID da conexão de streaming criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerou o lado do servidor para o registro que você acabou de enviar. Essa ID ajuda a Adobe a rastrear o ciclo de vida desse registro em vários sistemas e na depuração. |
| `receivedTimeMs`: Um carimbo de data e hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |
| `synchronousValidation.status` | Como o parâmetro query `synchronousValidation=true` foi adicionado, esse valor será exibido. Se a validação tiver êxito, o status será `pass`. |

## Recuperar os dados de séries de tempo ingeridos recentemente

Para validar os registros ingeridos anteriormente, você pode usar a [[!DNL Perfil Access API]](../../profile/api/entities.md) para recuperar os dados das séries de tempo. Isso pode ser feito usando uma solicitação de GET para o `/access/entities` ponto de extremidade e usando parâmetros de query opcionais. Vários parâmetros podem ser usados, separados por E comercial (&amp;).&quot;

>[!NOTE]
>
>Se a ID da política de mesclagem não estiver definida e o `schema.name` ou `relatedSchema.name` for `_xdm.context.profile`, [!DNL Profile Access] buscará **todas** as identidades relacionadas.

**Formato da API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `schema.name` | **Obrigatório.** O nome do schema que você está acessando. |
| `relatedSchema.name` | **Obrigatório.** Como você está acessando um schema `_xdm.context.experienceevent`, esse valor especifica o  para a entidade do perfil ao qual os eventos de série de tempo estão relacionados. |
| `relatedEntityId` | A ID da entidade relacionada. Se fornecido, você também deve fornecer a namespace da entidade. |
| `relatedEntityIdNS` | A namespace da ID que você está tentando recuperar. |

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

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das entidades solicitadas. Como você pode ver, esses são os mesmos dados de série de tempo que foram ingeridos anteriormente.

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

Ao ler este documento, agora você entende como assimilar dados de registro [!DNL Platform] usando conexões de transmissão. Você pode tentar fazer mais chamadas com valores diferentes e recuperar os valores atualizados. Além disso, você pode monitorar seus dados ingeridos por start por meio da [!DNL Platform] interface do usuário. Para mais informações, leia o guia de ingestão [de dados de](../quality/monitor-data-flows.md) monitorização.

Para obter mais informações sobre a ingestão de streaming em geral, leia a visão geral [da ingestão de](../streaming-ingestion/overview.md)streaming.
