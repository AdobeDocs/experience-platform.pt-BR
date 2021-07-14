---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, ativar conjunto de dados
title: Configurar um conjunto de dados para o Perfil e o serviço de identidade usando APIs
topic-legacy: tutorial
type: Tutorial
description: Este tutorial mostra como ativar um conjunto de dados para uso com o Perfil do cliente em tempo real e o Serviço de identidade usando APIs do Adobe Experience Platform.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---

# Configurar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service] usando APIs

Este tutorial aborda o processo de ativação de um conjunto de dados para uso em [!DNL Real-time Customer Profile] e [!DNL Identity Service], detalhado nas seguintes etapas:

1. Ative um conjunto de dados para usar em [!DNL Real-time Customer Profile], usando uma das duas opções:
   - [Criar um novo conjunto de dados](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar um conjunto de dados existente](#configure-an-existing-dataset)
1. [Assimilar dados no conjunto de dados](#ingest-data-into-the-dataset)
1. [Confirmar a assimilação de dados pelo Perfil do cliente em tempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar assimilação de dados pelo serviço de identidade](#confirm-data-ingest-by-identity-service)

## Introdução

Este tutorial requer uma compreensão funcional dos vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para [!DNL Profile]. Antes de iniciar este tutorial, reveja a documentação desses serviços [!DNL Platform] relacionados:

- [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Permite  [!DNL Real-time Customer Profile] por meio da ligação de identidades de diferentes fontes de dados que estão sendo assimiladas no  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Uma RESTful API que permite criar conjuntos de dados e configurá-los para  [!DNL Real-time Customer Profile] e  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da plataforma.

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional `Content-Type`. O valor correto desse cabeçalho é mostrado nas solicitações de amostra, quando necessário.

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho `x-sandbox-name` que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Criar um conjunto de dados habilitado para [!DNL Profile] e [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Você pode ativar um conjunto de dados para [!DNL Real-time Customer Profile] e [!DNL Identity Service] imediatamente após a criação ou em qualquer ponto após a criação do conjunto de dados. Se desejar ativar um conjunto de dados que já foi criado, siga as etapas para [configurar um conjunto de dados existente](#configure-an-existing-dataset) encontrado posteriormente neste documento. Para criar um novo conjunto de dados, você deve saber a ID de um esquema XDM existente que está ativada para o Perfil do cliente em tempo real. Para obter informações sobre como pesquisar ou criar um esquema habilitado para perfil, consulte o tutorial em [criar um esquema usando a API do Registro de esquema](../../xdm/tutorials/create-schema-api.md). A chamada a seguir para a API [!DNL Catalog] habilita um conjunto de dados para [!DNL Profile] e [!DNL Identity Service].

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir `unifiedProfile` e `unifiedIdentity` em `tags` no corpo da solicitação, o conjunto de dados será ativado imediatamente para [!DNL Profile] e [!DNL Identity Service], respectivamente. Os valores dessas tags devem ser uma matriz contendo a string `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Propriedade | Descrição |
|---|---|
| `schemaRef.id` | A ID do esquema habilitado para [!DNL Profile] no qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace dentro do [!DNL Schema Registry] que contém recursos pertencentes à sua Organização IMS. Consulte a seção [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) do guia do desenvolvedor [!DNL Schema Registry] para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz contendo a ID do conjunto de dados recém-criado no formato `"@/dataSets/{DATASET_ID}"`. Depois de criar e ativar com êxito um conjunto de dados, continue com as etapas para [carregar dados](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como habilitar um conjunto de dados criado anteriormente para [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Se você já criou um conjunto de dados habilitado para perfil, continue com as etapas para [assimilar dados](#ingest-data-into-the-dataset).

### Verificar se o conjunto de dados está ativado {#check-if-the-dataset-is-enabled}

Usando a API [!DNL Catalog], é possível inspecionar um conjunto de dados existente para determinar se ele está ativado para uso em [!DNL Real-time Customer Profile] e [!DNL Identity Service]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

**Formato da API**

```http
GET /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja inspecionar. |

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Na propriedade `tags`, você pode ver que `unifiedProfile` e `unifiedIdentity` estão presentes com o valor `enabled:true`. Portanto, [!DNL Real-time Customer Profile] e [!DNL Identity Service] são ativadas para esse conjunto de dados, respectivamente.

### Ativar o conjunto de dados {#enable-the-dataset}

Se o conjunto de dados existente não tiver sido ativado para [!DNL Profile] ou [!DNL Identity Service], é possível ativá-lo fazendo uma solicitação de PATCH usando a ID do conjunto de dados.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja atualizar. |

**Solicitação**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] }	
      ]'
```

O corpo da solicitação inclui um `path` para dois tipos de tags, `unifiedProfile` e `unifiedIdentity`. O `value` de cada é uma matriz que contém a cadeia de caracteres `enabled:true`.

****
RespostaUma solicitação de PATCH bem-sucedida retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. As tags `unifiedProfile` e `unifiedIdentity` foram adicionadas e o conjunto de dados é habilitado para uso pelos serviços de Perfil e identidade.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Assimilar dados no conjunto de dados {#ingest-data-into-the-dataset}

Ambos [!DNL Real-time Customer Profile] e [!DNL Identity Service] consomem dados XDM à medida que são assimilados em um conjunto de dados. Para obter instruções sobre como fazer upload de dados em um conjunto de dados, consulte o tutorial em [criar um conjunto de dados usando APIs](../../catalog/datasets/create.md). Ao planejar quais dados enviar para seu conjunto de dados habilitado para [!DNL Profile], considere as seguintes práticas recomendadas:

- Inclua todos os dados que deseja usar como critério de segmento do público-alvo.
- Inclua quantos identificadores você puder determinar dos dados do perfil para maximizar o gráfico de identidade. Isso permite que [!DNL Identity Service] identifique identidades em conjuntos de dados de forma mais eficaz.

## Confirmar assimilação de dados por [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Ao carregar dados em um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados conforme esperado. Usando a API de acesso [!DNL Real-time Customer Profile], é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se não conseguir recuperar nenhuma das entidades esperadas, o conjunto de dados pode não estar habilitado para [!DNL Real-time Customer Profile]. Depois de confirmar que seu conjunto de dados foi ativado, verifique se o formato e os identificadores de dados de origem são compatíveis com suas expectativas. Para obter instruções detalhadas sobre como usar a API [!DNL Real-time Customer Profile] para acessar os dados [!DNL Profile], siga o [guia do ponto de extremidade de entidades](../api/entities.md), também conhecido como &quot;[!DNL Profile Access] API&quot;.

## Confirmar assimilação de dados pelo serviço de identidade {#confirm-data-ingest-by-identity-service}

Cada fragmento de dados assimilado que contém mais de uma identidade cria um link no gráfico de identidade privada. Para obter mais informações sobre gráficos de identidade e dados de identidade de acesso, comece lendo a [Visão geral do Serviço de identidade](../../identity-service/home.md).
