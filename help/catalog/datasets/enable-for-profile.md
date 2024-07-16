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

# Habilitar um conjunto de dados para [!DNL Profile] e [!DNL Identity Service] usando APIs

Este tutorial aborda o processo de habilitação de um conjunto de dados para uso em [!DNL Real-Time Customer Profile] e [!DNL Identity Service], detalhado nas seguintes etapas:

1. Habilite um conjunto de dados para uso em [!DNL Real-Time Customer Profile], usando uma das duas opções:
   - [Criar um novo conjunto de dados](#create-a-dataset-enabled-for-profile-and-identity)
   - [Configurar um conjunto de dados existente](#configure-an-existing-dataset)
1. [Assimilar dados no conjunto de dados](#ingest-data-into-the-dataset)
1. [Confirmar assimilação de dados pelo Perfil de Cliente em Tempo Real](#confirm-data-ingest-by-real-time-customer-profile)
1. [Confirmar assimilação de dados pelo Serviço de Identidade](#confirm-data-ingest-by-identity-service)

## Introdução

Este tutorial requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para perfis. Antes de iniciar este tutorial, reveja a documentação desses serviços [!DNL Platform] relacionados:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] unindo identidades de diferentes fontes de dados que estão sendo assimiladas em [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): uma API RESTful que permite criar conjuntos de dados e configurá-los para [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem as informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da plataforma.

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho `Content-Type` adicional. O valor correto desse cabeçalho é mostrado nas solicitações de exemplo, quando necessário.

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para APIs [!DNL Platform] exigem um cabeçalho `x-sandbox-name` que especifique o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Criar um conjunto de dados habilitado para Perfil e Identidade {#create-a-dataset-enabled-for-profile-and-identity}

Você pode ativar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade imediatamente após a criação ou em qualquer momento após a criação do conjunto de dados. Se você quiser habilitar um conjunto de dados que já foi criado, siga as etapas para [configurar um conjunto de dados existente](#configure-an-existing-dataset) localizado posteriormente neste documento.

>[!NOTE]
>
>Para criar um novo conjunto de dados habilitado para perfil, você deve saber a ID de um esquema XDM existente que está habilitado para o Perfil. Para obter informações sobre como pesquisar ou criar um esquema habilitado para perfil, consulte o tutorial sobre [criação de um esquema usando a API do Registro de Esquema](../../xdm/tutorials/create-schema-api.md).

Para criar um conjunto de dados habilitado para o Perfil, você pode usar uma solicitação POST para o ponto de extremidade `/dataSets`.

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir `unifiedProfile` e `unifiedIdentity` em `tags` no corpo da solicitação, o conjunto de dados será habilitado imediatamente para [!DNL Profile] e [!DNL Identity Service], respectivamente. Os valores dessas marcas devem ser uma matriz contendo a cadeia de caracteres `"enabled:true"`.

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
| `schemaRef.id` | A ID do esquema habilitado para [!DNL Profile] no qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace no [!DNL Schema Registry] que contém recursos que pertencem à sua organização. Consulte a seção [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) do guia do desenvolvedor do [!DNL Schema Registry] para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz contendo a ID do conjunto de dados recém-criado na forma de `"@/dataSets/{DATASET_ID}"`. Depois de criar e habilitar com êxito um conjunto de dados, prossiga para as etapas para [carregar dados](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como habilitar um conjunto de dados criado anteriormente para [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. Se você já criou um conjunto de dados habilitado para perfil, prossiga para as etapas para [assimilar dados](#ingest-data-into-the-dataset).

### Verificar se o conjunto de dados está habilitado {#check-if-the-dataset-is-enabled}

Usando a API [!DNL Catalog], você pode inspecionar um conjunto de dados existente para determinar se ele está habilitado para uso em [!DNL Real-Time Customer Profile] e [!DNL Identity Service]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

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

Na propriedade `tags`, você pode ver que `unifiedProfile` e `unifiedIdentity` estão ambos presentes com o valor `enabled:true`. Portanto, [!DNL Real-Time Customer Profile] e [!DNL Identity Service] estão habilitados para este conjunto de dados, respectivamente.

### Ativar o conjunto de dados {#enable-the-dataset}

Se o conjunto de dados existente não tiver sido habilitado para [!DNL Profile] ou [!DNL Identity Service], você poderá habilitá-lo fazendo uma solicitação PATCH usando a ID do conjunto de dados.

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

O corpo da solicitação inclui de `path` a dois tipos de marcas, `unifiedProfile` e `unifiedIdentity`. Os `value` de cada um são matrizes que contêm a cadeia de caracteres `enabled:true`.

**Resposta**

Uma solicitação PATCH bem-sucedida retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. As marcas `unifiedProfile` e `unifiedIdentity` foram adicionadas e o conjunto de dados está habilitado para uso pelos serviços de Perfil e Identidade.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Assimilar dados no conjunto de dados {#ingest-data-into-the-dataset}

[!DNL Real-Time Customer Profile] e [!DNL Identity Service] consomem dados XDM enquanto estão sendo assimilados em um conjunto de dados. Para obter instruções sobre como carregar dados em um conjunto de dados, consulte o tutorial sobre [criação de um conjunto de dados usando APIs](../../catalog/datasets/create.md). Ao planejar quais dados enviar para seu conjunto de dados habilitado para [!DNL Profile], considere as seguintes práticas recomendadas:

- Inclua todos os dados que deseja usar como critérios de segmentação.
- Inclua quantos identificadores você puder verificar a partir dos dados do perfil para maximizar seu gráfico de identidade. Isso permite que o [!DNL Identity Service] compile identidades em conjuntos de dados com mais eficiência.

## Confirmar assimilação de dados por [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

Ao fazer upload de dados para um novo conjunto de dados pela primeira vez ou como parte de um processo que envolve um novo ETL ou fonte de dados, é recomendável verificar cuidadosamente os dados para garantir que tenham sido carregados conforme esperado. Usando a API de Acesso [!DNL Real-Time Customer Profile], você pode recuperar dados em lote conforme eles são carregados em um conjunto de dados. Se você não conseguir recuperar nenhuma das entidades esperadas, seu conjunto de dados pode não estar habilitado para [!DNL Real-Time Customer Profile]. Depois de confirmar que o conjunto de dados foi ativado, verifique se o formato de dados de origem e os identificadores atendem às suas expectativas. Para obter instruções detalhadas sobre como usar a API [!DNL Real-Time Customer Profile] para acessar dados do [!DNL Profile], consulte o [manual de ponto de extremidade de entidades](../../profile/api/entities.md), também conhecido como API &quot;[!DNL Profile Access]&quot;.

## Confirmar assimilação de dados pelo Serviço de identidade {#confirm-data-ingest-by-identity-service}

Cada fragmento de dados assimilado que contém mais de uma identidade cria um link em seu gráfico de identidade privado. Para obter mais informações sobre gráficos de identidade e acessar dados de identidade, comece lendo a [visão geral do Serviço de identidade](../../identity-service/home.md).
