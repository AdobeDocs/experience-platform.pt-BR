---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;habilitar conjunto de dados
title: Ativar um conjunto de dados para o Perfil e o Serviço de identidade usando APIs
type: Tutorial
description: Este tutorial mostra como ativar um conjunto de dados para uso com o Perfil do cliente em tempo real e o Serviço de identidade usando as APIs do Adobe Experience Platform.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: b80d8349fc54a955ebb3362d67a482d752871420
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 6%

---

# Ativar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service] uso de APIs

Este tutorial aborda o processo de habilitação de um conjunto de dados para uso no [!DNL Real-Time Customer Profile] e [!DNL Identity Service], divididos nas seguintes etapas:

1. Ativar um conjunto de dados para uso no [!DNL Real-Time Customer Profile], usando uma das duas opções:
   - [Criar um novo conjunto de dados](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar um conjunto de dados existente](#configure-an-existing-dataset)
1. [Assimilar dados no conjunto de dados](#ingest-data-into-the-dataset)
1. [Confirmar assimilação de dados pelo Perfil do cliente em tempo real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar assimilação de dados pelo Serviço de identidade](#confirm-data-ingest-by-identity-service)

## Introdução

Este tutorial requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para perfis. Antes de iniciar este tutorial, revise a documentação desses [!DNL Platform] serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] unindo identidades de diferentes fontes de dados assimiladas na [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): uma API RESTful que permite criar conjuntos de dados e configurá-los para [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem as informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da plataforma.

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem uma `Content-Type` cabeçalho. O valor correto desse cabeçalho é mostrado nas solicitações de exemplo, quando necessário.

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem uma `x-sandbox-name` cabeçalho que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Criar um conjunto de dados habilitado para Perfil e Identidade {#create-a-dataset-enabled-for-profile-and-identity}

Você pode ativar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade imediatamente após a criação ou em qualquer momento após a criação do conjunto de dados. Se quiser ativar um conjunto de dados que já foi criado, siga as etapas para [configurar um conjunto de dados existente](#configure-an-existing-dataset) encontrado mais adiante neste documento.

>[!NOTE]
>
>Para criar um novo conjunto de dados habilitado para perfil, você deve saber a ID de um esquema XDM existente que está habilitado para o Perfil. Para obter informações sobre como pesquisar ou criar um esquema habilitado para perfil, consulte o tutorial em [criação de um esquema usando a API do registro de esquema](../../xdm/tutorials/create-schema-api.md).

Para criar um conjunto de dados habilitado para o Perfil, você pode usar uma solicitação POST para `/dataSets` terminal.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
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
| `schemaRef.id` | A ID do [!DNL Profile]Esquema habilitado para o qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace dentro do [!DNL Schema Registry] que contém recursos pertencentes à sua organização. Consulte a [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) seção do [!DNL Schema Registry] guia do desenvolvedor para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz que contém a ID do conjunto de dados recém-criado na forma de `"@/dataSets/{DATASET_ID}"`. Depois de criar e habilitar um conjunto de dados com sucesso, prossiga para as etapas para [upload de dados](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como ativar um conjunto de dados criado anteriormente para o [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. Se você já criou um conjunto de dados habilitado para o perfil, prossiga para as etapas para [assimilação de dados](#ingest-data-into-the-dataset).

### Verificar se o conjunto de dados está habilitado {#check-if-the-dataset-is-enabled}

Usar o [!DNL Catalog] , você pode inspecionar um conjunto de dados existente para determinar se ele está ativado para uso no [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

No `tags` propriedade, você pode ver que `unifiedProfile` e `unifiedIdentity` ambos estão presentes com o valor `enabled:true`. Por conseguinte, [!DNL Real-Time Customer Profile] e [!DNL Identity Service] são habilitados para este conjunto de dados, respectivamente.

### Ativar o conjunto de dados {#enable-the-dataset}

Se o conjunto de dados existente não tiver sido habilitado para [!DNL Profile] ou [!DNL Identity Service], você pode ativá-lo fazendo uma solicitação PATCH usando a ID do conjunto de dados.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

O corpo da solicitação inclui uma `path` para dois tipos de tags, `unifiedProfile` e `unifiedIdentity`. A variável `value` de cada são matrizes que contêm a sequência `enabled:true`.

**Resposta**

Uma solicitação PATCH bem-sucedida retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A variável `unifiedProfile` e `unifiedIdentity` As tags foram adicionadas e o conjunto de dados está habilitado para uso pelos serviços de Perfil e Identidade.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Assimilar dados no conjunto de dados {#ingest-data-into-the-dataset}

Ambos [!DNL Real-Time Customer Profile] e [!DNL Identity Service] consumir dados XDM enquanto estão sendo assimilados em um conjunto de dados. Para obter instruções sobre como fazer upload de dados em um conjunto de dados, consulte o tutorial sobre [criação de um conjunto de dados usando APIs](../../catalog/datasets/create.md). Ao planejar quais dados enviar para o seu [!DNL Profile]conjunto de dados habilitado para, considere as seguintes práticas recomendadas:

- Inclua todos os dados que deseja usar como critérios de segmentação.
- Inclua quantos identificadores você puder verificar a partir dos dados do perfil para maximizar seu gráfico de identidade. Isso permite [!DNL Identity Service] para compilar identidades em conjuntos de dados com mais eficiência.

## Confirmar assimilação de dados por [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que tenham sido carregados conforme esperado. Usar o [!DNL Real-Time Customer Profile] Acessar a API, é possível recuperar dados em lote à medida que são carregados em um conjunto de dados. Se não conseguir recuperar nenhuma das entidades esperadas, o conjunto de dados pode não estar habilitado para [!DNL Real-Time Customer Profile]. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato de dados de origem e os identificadores atendem às suas expectativas. Para obter instruções detalhadas sobre como usar a variável [!DNL Real-Time Customer Profile] API para acessar o [!DNL Profile] consulte os [manual de endpoint de entidades](../../profile/api/entities.md), também conhecido como &quot;[!DNL Profile Access]&quot;API.

## Confirmar assimilação de dados pelo Serviço de identidade {#confirm-data-ingest-by-identity-service}

Cada fragmento de dados assimilado que contém mais de uma identidade cria um link em seu gráfico de identidade privado. Para obter mais informações sobre gráficos de identidade e acessar dados de identidade, comece lendo o [Visão geral do serviço de identidade](../../identity-service/home.md).
