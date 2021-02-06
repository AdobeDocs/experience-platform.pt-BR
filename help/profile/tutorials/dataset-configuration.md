---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;ativar conjunto de dados
title: Configurar um conjunto de dados para Perfil e serviço de identidade usando APIs
topic: tutorial
type: Tutorial
description: Este tutorial mostra como ativar um conjunto de dados para uso com o Perfil do cliente em tempo real e o Serviço de identidade usando as APIs da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 1%

---


# Configurar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service] usando APIs

Este tutorial aborda o processo de ativação de um conjunto de dados para uso em [!DNL Real-time Customer Profile] e [!DNL Identity Service], detalhado nas seguintes etapas:

1. Ative um conjunto de dados para uso em [!DNL Real-time Customer Profile], usando uma das duas opções:
   - [Criar um novo conjunto de dados](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar um conjunto de dados existente](#configure-an-existing-dataset)
1. [Inserir dados no conjunto de dados](#ingest-data-into-the-dataset)
1. [Confirmar a assimilação de dados pelo Perfil do cliente em tempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar a assimilação de dados pelo Serviço de Identidade](#confirm-data-ingest-by-identity-service)

## Introdução

Este tutorial requer um entendimento prático dos vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para [!DNL Profile]. Antes de iniciar este tutorial, reveja a documentação dos serviços relacionados [!DNL Platform]:

- [[!DNL Real-time Customer Profile]](../home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita  [!DNL Real-time Customer Profile] ao fazer a ponte entre identidades de fontes de dados diferentes que estão sendo assimiladas  [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Uma API RESTful que permite criar conjuntos de dados e configurá-los para  [!DNL Real-time Customer Profile] e  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para as APIs de plataforma.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá. Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## Criar um conjunto de dados habilitado para [!DNL Profile] e [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

Você pode ativar um conjunto de dados para [!DNL Real-time Customer Profile] e [!DNL Identity Service] imediatamente após a criação ou em qualquer momento após a criação do conjunto de dados. Se você deseja ativar um conjunto de dados que já foi criado, siga as etapas para [configurar um conjunto de dados existente](#configure-an-existing-dataset) encontrado posteriormente neste documento. Para criar um novo conjunto de dados, é necessário saber a ID de um schema XDM existente habilitado para o Perfil do cliente em tempo real. Para obter informações sobre como procurar ou criar um schema habilitado para Perfis, consulte o tutorial em [criar um schema usando a API do Registro do Schema](../../xdm/tutorials/create-schema-api.md). A chamada a seguir para a API [!DNL Catalog] ativa um conjunto de dados para [!DNL Profile] e [!DNL Identity Service].

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir `unifiedProfile` e `unifiedIdentity` em `tags` no corpo da solicitação, o conjunto de dados será imediatamente ativado para [!DNL Profile] e [!DNL Identity Service], respectivamente. Os valores dessas tags devem ser uma matriz que contenha a string `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
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
| `schemaRef.id` | A ID do schema habilitado para [!DNL Profile] no qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | A namespace dentro de [!DNL Schema Registry] que contém recursos pertencentes à sua Organização IMS. Consulte a seção [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) do [!DNL Schema Registry] guia do desenvolvedor para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz que contém a ID do conjunto de dados recém-criado na forma de `"@/dataSets/{DATASET_ID}"`. Depois de criar e ativar um conjunto de dados com êxito, siga para as etapas para [carregar dados](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como ativar um conjunto de dados criado anteriormente para [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Se você já tiver criado um conjunto de dados habilitado para Perfis, siga para as etapas para [assimilar dados](#ingest-data-into-the-dataset).

### Verifique se o conjunto de dados está ativado {#check-if-the-dataset-is-enabled}

Usando a API [!DNL Catalog], você pode inspecionar um conjunto de dados existente para determinar se ele está habilitado para uso em [!DNL Real-time Customer Profile] e [!DNL Identity Service]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

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
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
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

Na propriedade `tags`, você pode ver que `unifiedProfile` e `unifiedIdentity` estão presentes com o valor `enabled:true`. Portanto, [!DNL Real-time Customer Profile] e [!DNL Identity Service] estão ativados para este conjunto de dados, respectivamente.

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
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

O corpo da solicitação inclui uma propriedade `tags`, que contém duas subpropriedades: `"unifiedProfile"` e `"unifiedIdentity"`. Os valores dessas subpropriedades são arrays que contêm a string `"enabled:true"`.

****
RespostaUma solicitação de PATCH bem-sucedida retorna o Status HTTP 200 (OK) e uma matriz que contém a ID do conjunto de dados atualizado. Essa ID deve corresponder àquela enviada na solicitação de PATCH. As tags `"unifiedProfile"` e `"unifiedIdentity"` foram adicionadas e o conjunto de dados está habilitado para uso pelos serviços de Perfil e identidade.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Ingressar dados no conjunto de dados {#ingest-data-into-the-dataset}

Ambos [!DNL Real-time Customer Profile] e [!DNL Identity Service] consomem dados XDM à medida que são ingeridos em um conjunto de dados. Para obter instruções sobre como carregar dados em um conjunto de dados, consulte o tutorial em [criar um conjunto de dados usando APIs](../../catalog/datasets/create.md). Ao planejar quais dados serão enviados para seu conjunto de dados habilitado para [!DNL Profile], considere as seguintes práticas recomendadas:

- Inclua todos os dados que você deseja usar como critérios de segmento de audiência.
- Inclua quantos identificadores você puder determinar a partir dos dados do perfil para maximizar seu gráfico de identidade. Isso permite que [!DNL Identity Service] agrupe identidades em conjuntos de dados com mais eficiência.

## Confirmar assimilação de dados por [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez, ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados conforme esperado. Usando a API de acesso [!DNL Real-time Customer Profile], é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se você não conseguir recuperar nenhuma das entidades esperadas, seu conjunto de dados pode não estar habilitado para [!DNL Real-time Customer Profile]. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato e os identificadores dos dados de origem suportam suas expectativas. Para obter instruções detalhadas sobre como usar a API [!DNL Real-time Customer Profile] para acessar os dados [!DNL Profile], siga o [guia de endpoint das entidades](../api/entities.md), também conhecido como &quot;[!DNL Profile Access] API&quot;.

## Confirmar a assimilação de dados pelo Serviço de Identidade {#confirm-data-ingest-by-identity-service}

Cada fragmento de dados ingerido que contém mais de uma identidade cria um link no gráfico de identidade particular. Para obter mais informações sobre gráficos de identidade e dados de identidade de acesso, comece lendo a [visão geral do Serviço de Identidade](../../identity-service/home.md).