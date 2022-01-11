---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, ativar conjunto de dados
title: Ativar um conjunto de dados para o Perfil e o serviço de identidade usando APIs
type: Tutorial
description: Este tutorial mostra como ativar um conjunto de dados para uso com o Perfil do cliente em tempo real e o Serviço de identidade usando APIs do Adobe Experience Platform.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: d463dabbb9dc099394081b803df619129c0cb416
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Ativar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service] uso de APIs

Este tutorial aborda o processo de ativação de um conjunto de dados para uso no [!DNL Real-time Customer Profile] e [!DNL Identity Service], divididas nas seguintes etapas:

1. Habilitar um conjunto de dados para uso em [!DNL Real-time Customer Profile], usando uma das duas opções:
   - [Criar um novo conjunto de dados](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar um conjunto de dados existente](#configure-an-existing-dataset)
1. [Assimilar dados no conjunto de dados](#ingest-data-into-the-dataset)
1. [Confirmar a assimilação de dados pelo Perfil do cliente em tempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar assimilação de dados pelo serviço de identidade](#confirm-data-ingest-by-identity-service)

## Introdução

Este tutorial requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para perfil. Antes de iniciar este tutorial, revise a documentação referente a esses [!DNL Platform] serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilitar [!DNL Real-time Customer Profile] ao ligar identidades de fontes de dados diferentes que estão sendo assimiladas em [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): Uma RESTful API que permite criar conjuntos de dados e configurá-los para [!DNL Real-time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da plataforma.

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem uma carga adicional `Content-Type` cabeçalho. O valor correto desse cabeçalho é mostrado nas solicitações de amostra, quando necessário.

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um `x-sandbox-name` cabeçalho que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Criar um conjunto de dados habilitado para Perfil e identidade {#create-a-dataset-enabled-for-profile-and-identity}

Você pode ativar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade imediatamente após a criação ou em qualquer ponto após a criação do conjunto de dados. Se desejar ativar um conjunto de dados que já foi criado, siga as etapas para [configuração de um conjunto de dados existente](#configure-an-existing-dataset) encontrado mais tarde neste documento.

>[!NOTE]
>
>Para criar um novo conjunto de dados habilitado para perfil, você deve saber a ID de um esquema XDM existente que está ativado para o perfil. Para obter informações sobre como pesquisar ou criar um esquema ativado por perfil, consulte o tutorial em [criação de um esquema usando a API do Registro de esquema](../../xdm/tutorials/create-schema-api.md).

Para criar um conjunto de dados habilitado para o Perfil, você pode usar uma solicitação de POST para a função `/dataSets` endpoint .

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir `unifiedProfile` e `unifiedIdentity` under `tags` no corpo da solicitação, o conjunto de dados será ativado imediatamente para [!DNL Profile] e [!DNL Identity Service], respectivamente. Os valores dessas tags devem ser uma matriz contendo a string `"enabled:true"`.

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
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| Propriedade | Descrição |
|---|---|
| `schemaRef.id` | A ID do [!DNL Profile]-enabled schema no qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace no [!DNL Schema Registry] que contém recursos pertencentes à organização IMS. Consulte a [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) da seção [!DNL Schema Registry] guia do desenvolvedor para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz contendo a ID do conjunto de dados recém-criado no formato de `"@/dataSets/{DATASET_ID}"`. Depois de criar e ativar com êxito um conjunto de dados, continue com as etapas para [upload de dados](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como ativar um conjunto de dados criado anteriormente para [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Se você já criou um conjunto de dados habilitado para perfil, continue com as etapas para [assimilação de dados](#ingest-data-into-the-dataset).

### Verificar se o conjunto de dados está ativado {#check-if-the-dataset-is-enabled}

Usar o [!DNL Catalog] Você pode inspecionar um conjunto de dados existente para determinar se ele está ativado para uso em [!DNL Real-time Customer Profile] e [!DNL Identity Service]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

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

Em `tags` você pode ver que `unifiedProfile` e `unifiedIdentity` estão presentes com o valor `enabled:true`. Por conseguinte, [!DNL Real-time Customer Profile] e [!DNL Identity Service] são ativadas para esse conjunto de dados, respectivamente.

### Ativar o conjunto de dados {#enable-the-dataset}

Se o conjunto de dados existente não tiver sido ativado para [!DNL Profile] ou [!DNL Identity Service], é possível ativá-lo fazendo uma solicitação do PATCH usando a ID do conjunto de dados.

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

O corpo da solicitação inclui um `path` para dois tipos de tags, `unifiedProfile` e `unifiedIdentity`. O `value` de cada uma são arrays que contêm a string `enabled:true`.

**Resposta**
Uma solicitação bem-sucedida do PATCH retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. O `unifiedProfile` e `unifiedIdentity` As tags foram adicionadas e o conjunto de dados é ativado para uso pelos serviços de Perfil e identidade.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Assimilar dados no conjunto de dados {#ingest-data-into-the-dataset}

Ambos [!DNL Real-time Customer Profile] e [!DNL Identity Service] consumir dados XDM conforme são assimilados em um conjunto de dados. Para obter instruções sobre como fazer upload de dados em um conjunto de dados, consulte o tutorial em [criação de um conjunto de dados usando APIs](../../catalog/datasets/create.md). Ao planejar quais dados enviar para a [!DNL Profile]conjunto de dados habilitado para o , considere as seguintes práticas recomendadas:

- Inclua todos os dados que deseja usar como critérios de segmentação.
- Inclua quantos identificadores você puder determinar dos dados do perfil para maximizar o gráfico de identidade. Isso permite [!DNL Identity Service] para unir identidades em conjuntos de dados de forma mais eficaz.

## Confirmar a assimilação de dados por [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Ao carregar dados em um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que eles tenham sido carregados conforme esperado. Usar o [!DNL Real-time Customer Profile] Para acessar a API, é possível recuperar dados em lote à medida que eles são carregados em um conjunto de dados. Se não conseguir recuperar nenhuma das entidades esperadas, o conjunto de dados talvez não esteja habilitado para [!DNL Real-time Customer Profile]. Depois de confirmar que seu conjunto de dados foi ativado, verifique se o formato e os identificadores de dados de origem são compatíveis com suas expectativas. Para obter instruções detalhadas sobre como usar o [!DNL Real-time Customer Profile] API para acessar [!DNL Profile] consulte os [guia do endpoint de entidades](../../profile/api/entities.md), também conhecido como &quot;[!DNL Profile Access]&quot; API.

## Confirmar assimilação de dados pelo serviço de identidade {#confirm-data-ingest-by-identity-service}

Cada fragmento de dados assimilado que contém mais de uma identidade cria um link no gráfico de identidade privada. Para obter mais informações sobre gráficos de identidade e dados de identidade de acesso, comece lendo o [Visão geral do Serviço de identidade](../../identity-service/home.md).
