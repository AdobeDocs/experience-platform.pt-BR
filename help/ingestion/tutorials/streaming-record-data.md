---
keywords: Experience Platform;lar;tópicos populares;ingestão em fluxo;ingestão;dados de registro;dados de registro de fluxo;
solution: Experience Platform
title: Transmissão de dados de registro
topic: tutorial
type: Tutorial
description: Este tutorial o ajudará a começar a usar APIs de ingestão de streaming, parte das APIs do Adobe Experience Platform Data Ingestion Service.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 2%

---


# Transmitir dados de registro para o Adobe Experience Platform

Este tutorial o ajudará a começar a usar APIs de ingestão de streaming, parte das APIs do Adobe Experience Platform [!DNL Data Ingestion Service].

## Introdução

Este tutorial requer um conhecimento prático de vários serviços da Adobe Experience Platform. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado através do qual  [!DNL Platform] organiza os dados da experiência.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e de consumidor em tempo real, com base em dados agregados de várias fontes.
- [Guia](../../xdm/api/getting-started.md) do desenvolvedor do Registro do schema: Um guia abrangente que abrange cada um dos pontos finais disponíveis da  [!DNL Schema Registry] API e como fazer chamadas para eles. Isso inclui conhecer seu `{TENANT_ID}`, que aparece em chamadas em todo este tutorial, bem como saber como criar schemas, que é usado na criação de um conjunto de dados para ingestão.

Além disso, este tutorial requer que você já tenha criado uma conexão de streaming. Para obter mais informações sobre como criar uma conexão de streaming, leia o tutorial [criar uma conexão de streaming](./create-streaming-connection.md).

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs de ingestão de streaming.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Compor um schema com base na classe [!DNL XDM Individual Profile]

Para criar um conjunto de dados, primeiro será necessário criar um novo schema que implemente a classe [!DNL XDM Individual Profile]. Para obter mais informações sobre como criar schemas, leia o [Guia do desenvolvedor da API de Registro de Schemas](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `title` | O nome que você deseja usar para o seu schema. Esse nome deve ser exclusivo. |
| `description` | Uma descrição significativa do schema que você está criando. |
| `meta:immutableTags` | Neste exemplo, a tag `union` é usada para persistir seus dados em [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes do schema recém-criado.

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
    "imsOrg": "{IMS_ORG}",
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
| `{TENANT_ID}` | Essa ID é usada para garantir que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. Para obter mais informações sobre a ID do locatário, leia o [guia do Registro do schema](../../xdm/api/getting-started.md#know-your-tenant-id). |

Anote os atributos `$id` e `version`, pois ambos serão usados ao criar seu conjunto de dados.

## Definir um descritor de identidade primário para o schema

Em seguida, adicione um [descritor de identidade](../../xdm/api/descriptors.md) ao schema criado acima, usando o atributo de endereço de email de trabalho como o identificador principal. Isso resultará em duas alterações:

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
| `{SCHEMA_REF_ID}` | O `$id` que você recebeu anteriormente quando compôs o schema. Deve ser algo parecido com isto: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Códigos de Namespace de Identidade**
>
> Certifique-se de que os códigos sejam válidos - o exemplo acima usa &quot;email&quot;, que é uma namespace de identidade padrão. Outras namespaces de identidade padrão comumente usadas podem ser encontradas nas [Perguntas frequentes do serviço de identidade](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Se você quiser criar uma namespace personalizada, siga as etapas descritas em [visão geral da namespace de identidade](../../identity-service/home.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com informações sobre o descritor de identidade primário recém-criado para o schema.

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
    "imsOrg": "{IMS_ORG}"
}
```

## Criar um conjunto de dados para dados de registro

Depois de criar o schema, será necessário criar um conjunto de dados para assimilar os dados do registro.

>[!NOTE]
>
>Este conjunto de dados será ativado para **[!DNL Real-time Customer Profile]** e **[!DNL Identity Service]**.

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
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
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
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Ingressar dados de registro na conexão de streaming

Com o conjunto de dados e a conexão de streaming instalada, você pode assimilar registros JSON formatados em XDM para assimilar dados de registro em [!DNL Platform].

**Formato da API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{CONNECTION_ID}` | O valor `id` da conexão de streaming criada anteriormente. |
| `synchronousValidation` | Um parâmetro opcional de query destinado a fins de desenvolvimento. Se definido como `true`, ele pode ser usado para feedback imediato para determinar se a solicitação foi enviada com êxito. Por padrão, esse valor é definido como `false`. |

**Solicitação**

A inserção de dados de registro em uma conexão de streaming pode ser feita com ou sem o nome de origem.

A solicitação de exemplo abaixo ingere um registro com um nome de origem ausente na Plataforma. Se um registro não tiver o nome de origem, ele adicionará a ID de origem da definição de conexão de streaming.

>[!NOTE]
>
>A chamada de API a seguir **not** requer cabeçalhos de autenticação.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
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
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
| `{CONNECTION_ID}` | A ID da conexão de streaming criada anteriormente. |
| `xactionId` | Um identificador exclusivo gerou o lado do servidor para o registro que você acabou de enviar. Essa ID ajuda a Adobe a rastrear o ciclo de vida desse registro em vários sistemas e na depuração. |
| `receivedTimeMs` | Um carimbo de data e hora (época em milissegundos) que mostra a hora em que a solicitação foi recebida. |
| `synchronousValidation.status` | Como o parâmetro do query `synchronousValidation=true` foi adicionado, esse valor será exibido. Se a validação tiver êxito, o status será `pass`. |

## Recuperar os dados de registro recém-ingeridos

Para validar os registros ingeridos anteriormente, você pode usar [[!DNL Profile Access API]](../../profile/api/entities.md) para recuperar os dados do registro.

>[!NOTE]
>
>Se a ID da política de mesclagem não estiver definida e `schema.name` ou `relatedSchema.name` for `_xdm.context.profile`, [!DNL Profile Access] buscará **todas** identidades relacionadas.

**Formato da API**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `schema.name` | **Obrigatório.** O nome do schema que você está acessando. |
| `entityId` | A ID da entidade. Se fornecido, você também deve fornecer a namespace da entidade. |
| `entityIdNS` | A namespace da ID que você está tentando recuperar. |

**Solicitação**

Você pode revisar os dados de registro ingeridos anteriormente com a seguinte solicitação de GET.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes das entidades solicitadas. Como você pode ver, esse é o mesmo registro que foi ingerido com sucesso anteriormente.

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

Ao ler este documento, agora você entende como assimilar dados de registro em [!DNL Platform] usando conexões de transmissão. Você pode tentar fazer mais chamadas com valores diferentes e recuperar os valores atualizados. Além disso, você pode monitorar seus dados ingeridos com start por meio da interface do usuário [!DNL Platform]. Para obter mais informações, leia o guia [monitoramento da ingestão de dados](../quality/monitor-data-ingestion.md).

Para obter mais informações sobre a ingestão de streaming em geral, leia a [visão geral da ingestão de streaming](../streaming-ingestion/overview.md).


