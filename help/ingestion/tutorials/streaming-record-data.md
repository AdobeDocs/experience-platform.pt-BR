---
keywords: Experience Platform;página inicial;tópicos populares;assimilação de fluxo;assimilação;dados de registro;dados de registro de fluxo;
solution: Experience Platform
title: Transmitir dados de registro usando APIs de assimilação de fluxo
type: Tutorial
description: Este tutorial ajudará você a começar a usar as APIs de assimilação de fluxo, parte das APIs de serviço de assimilação de dados da Adobe Experience Platform.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 3%

---


# Transmitir dados de registro usando APIs de assimilação de fluxo

Este tutorial ajudará você a começar a usar as APIs de assimilação de streaming, parte da Adobe Experience Platform [!DNL Data Ingestion Service] APIs.

## Introdução

Este tutorial requer um conhecimento prático de vários serviços da Adobe Experience Platform. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência.
   - [Guia do desenvolvedor do Registro de esquema](../../xdm/api/getting-started.md): um guia abrangente que cobre cada um dos endpoints disponíveis do [!DNL Schema Registry] API e como fazer chamadas para eles. Isso inclui conhecer o seu `{TENANT_ID}`, que aparece em chamadas neste tutorial, além de saber como criar esquemas, que é usado na criação de um conjunto de dados para assimilação.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Uso de APIs da plataforma

Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../landing/api-guide.md).

## Compor um esquema com base no [!DNL XDM Individual Profile] classe

Para criar um conjunto de dados, primeiro será necessário criar um novo esquema que implemente a variável [!DNL XDM Individual Profile] classe. Para obter mais informações sobre como criar schemas, leia a [Guia do desenvolvedor da API do registro de esquema](../../xdm/api/getting-started.md).

**Formato da API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
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
| `meta:immutableTags` | Neste exemplo, a variável `union` é usada para manter seus dados em [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes do esquema recém-criado.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. Para obter mais informações sobre a ID do locatário, leia a [guia de registro de esquema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Por favor, tome nota do `$id` bem como a `version` atributos, pois ambos serão usados ao criar o conjunto de dados.

## Definir um descritor de identidade primário para o esquema

Em seguida, adicione um [descritor de identidade](../../xdm/api/descriptors.md) para o schema criado acima, usando o atributo de endereço de email de trabalho como o identificador principal. Isso resultará em duas alterações:

1. O endereço de email comercial se tornará um campo obrigatório. Isso significa que as mensagens enviadas sem esse campo terão falha na validação e não serão assimiladas.

2. [!DNL Real-Time Customer Profile] O usará o endereço de email comercial como um identificador para ajudar a compilar mais informações sobre esse indivíduo.

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
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | A variável `$id` que você recebeu anteriormente ao compor o esquema. Deve ser semelhante a: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Códigos do namespace de identidade**
>
> Verifique se os códigos são válidos - o exemplo acima usa &quot;email&quot;, que é um namespace de identidade padrão. Outros namespaces de identidade padrão comumente usados podem ser encontrados no [Perguntas frequentes do serviço de identidade](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Se quiser criar um namespace personalizado, siga as etapas descritas no [visão geral do namespace de identidade](../../identity-service/home.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com informações sobre o descritor de identidade principal recém-criado do esquema.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## Criar um conjunto de dados para dados de registro

Depois de criar o esquema, será necessário criar um conjunto de dados para assimilar dados de registro.

>[!NOTE]
>
>Este conjunto de dados será habilitado para **[!DNL Real-Time Customer Profile]** e **[!DNL Identity Service]**.

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
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
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
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Criar uma conexão de streaming

Depois de criar o esquema e o conjunto de dados, você pode criar uma conexão de transmissão

Para obter mais informações sobre como criar uma conexão de transmissão, leia o [criar um tutorial de conexão de transmissão](./create-streaming-connection.md).

## Assimilar dados de registro na conexão de transmissão {#ingest-data}

Com o conjunto de dados e a conexão de transmissão em vigor, é possível assimilar registros JSON formatados em XDM para assimilar dados de registro em [!DNL Platform].

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | A variável `inletId` valor da conexão de streaming criada anteriormente. |
| `syncValidation` | Um parâmetro de consulta opcional destinado a fins de desenvolvimento. Se definida como `true`, ele pode ser usado para feedback imediato para determinar se a solicitação foi enviada com êxito. Por padrão, esse valor é definido como `false`. Observe que, se você definir esse parâmetro de consulta como `true` que a solicitação será limitada a 60 vezes por minuto por `CONNECTION_ID`. |

**Solicitação**

A assimilação de dados de registro em uma conexão de streaming pode ser feita com ou sem o nome de origem.

A solicitação de exemplo abaixo assimila um registro com um nome de origem ausente na Platform. Se um registro não tiver o nome de origem, ele adicionará a ID de origem da definição da conexão de streaming.

>[!NOTE]
>
>A chamada de API a seguir faz **não** exigir cabeçalhos de autenticação.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
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
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do fluxo recém-transmitido [!DNL Profile].

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
| `{CONNECTION_ID}` | A ID da conexão de streaming criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerado no lado do servidor para o registro que você acabou de enviar. Essa ID ajuda o Adobe a rastrear o ciclo de vida desse registro por vários sistemas e com depuração. |
| `receivedTimeMs` | Um carimbo de data e hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |
| `syncValidation.status` | Como o parâmetro de consulta `syncValidation=true` foi adicionado, esse valor aparecerá. Se a validação tiver êxito, o status será `pass`. |

## Recuperar os dados de registro recém-assimilados

Para validar os registros assimilados anteriormente, é possível usar o [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar os dados do registro.

>[!NOTE]
>
>Se a ID da política de mesclagem não estiver definida e a variável `schema.name` ou `relatedSchema.name` é `_xdm.context.profile`, [!DNL Profile Access] buscará **all** identidades relacionadas.

**Formato da API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `schema.name` | **Obrigatório.** O nome do esquema que você está acessando. |
| `entityId` | A ID da entidade. Se fornecido, você também deve fornecer o namespace da entidade. |
| `entityIdNS` | O namespace da ID que você está tentando recuperar. |

**Solicitação**

Você pode revisar os dados de registro assimilados anteriormente com a solicitação GET a seguir.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das entidades solicitadas. Como você pode ver, este é o mesmo registro que foi assimilado com sucesso anteriormente.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Próximas etapas

Ao ler este documento, agora você entende como assimilar dados de registro em [!DNL Platform] usando conexões de transmissão. Você pode tentar fazer mais chamadas com valores diferentes e recuperar os valores atualizados. Além disso, você pode começar a monitorar os dados assimilados por meio de [!DNL Platform] IU. Para obter mais informações, leia a [monitoramento da assimilação de dados](../quality/monitor-data-ingestion.md) guia.

Para obter mais informações sobre a assimilação por transmissão em geral, leia o [visão geral da assimilação por transmissão](../streaming-ingestion/overview.md).
