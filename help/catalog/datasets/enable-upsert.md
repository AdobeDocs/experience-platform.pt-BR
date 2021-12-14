---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, ativar conjunto de dados
title: Ativar um conjunto de dados para atualizações de perfil usando APIs
type: Tutorial
description: Este tutorial mostra como usar APIs do Adobe Experience Platform para ativar um conjunto de dados com recursos de "atualização" para fazer atualizações nos dados de Perfil do cliente em tempo real.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# Ativar um conjunto de dados para atualizações de perfil usando APIs

Este tutorial aborda o processo de ativação de um conjunto de dados com recursos de &quot;atualização&quot; para fazer atualizações nos dados de Perfil do cliente em tempo real. Isso inclui etapas para criar um novo conjunto de dados e configurar um conjunto de dados existente.

## Introdução

Este tutorial requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para perfil. Antes de iniciar este tutorial, reveja a documentação desses serviços da plataforma DNL relacionados:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Catalog Service]](../../catalog/home.md): Uma RESTful API que permite criar conjuntos de dados e configurá-los para [!DNL Real-time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.
- [Assimilação em lote](../../ingestion/batch-ingestion/overview.md)

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

## Criar um conjunto de dados habilitado para atualizações de perfil

Ao criar um novo conjunto de dados, você pode habilitar esse conjunto de dados para Perfil e habilitar recursos de atualização no momento da criação.

>[!NOTE]
>
>Para criar um novo conjunto de dados habilitado para perfil, você deve saber a ID de um esquema XDM existente que está ativado para o perfil. Para obter informações sobre como pesquisar ou criar um esquema ativado por perfil, consulte o tutorial em [criação de um esquema usando a API do Registro de esquema](../../xdm/tutorials/create-schema-api.md).

Para criar um conjunto de dados habilitado para Perfil e atualizações, use uma solicitação de POST para `/dataSets` endpoint .

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir `unifiedProfile` under `tags` no corpo da solicitação, o conjunto de dados será ativado para [!DNL Profile] após a criação. No `unifiedProfile` array, adição `isUpsert:true` O adicionará a capacidade do conjunto de dados de suportar atualizações.

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
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| Propriedade | Descrição |
|---|---|
| `schemaRef.id` | A ID do [!DNL Profile]-enabled schema no qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace no [!DNL Schema Registry] que contém recursos pertencentes à organização IMS. Consulte a [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) da seção [!DNL Schema Registry] guia do desenvolvedor para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz contendo a ID do conjunto de dados recém-criado no formato de `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como configurar um conjunto de dados existente habilitado para perfil para a funcionalidade de atualização (&quot;upsert&quot;).

>[!NOTE]
>
>Para configurar um conjunto de dados habilitado para perfil para &quot;upsert&quot;, primeiro desative o conjunto de dados para Perfil e depois reative-o junto com o `isUpsert` . Se o conjunto de dados existente não estiver ativado para o Perfil, você pode prosseguir diretamente para as etapas para [habilitar o conjunto de dados para Perfil e Redefinir](#enable-the-dataset). Se não tiver certeza, as etapas a seguir mostram como verificar se o conjunto de dados já está ativado.

### Verifique se o conjunto de dados está ativado para o Perfil

Usar o [!DNL Catalog] Você pode inspecionar um conjunto de dados existente para determinar se ele está ativado para uso em [!DNL Real-time Customer Profile]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

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
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
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
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
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

Em `tags` você pode ver que `unifiedProfile` está presente com o valor `enabled:true`. Por conseguinte, [!DNL Real-time Customer Profile] está ativado para este conjunto de dados.

### Desativar o conjunto de dados para o Perfil

Para configurar um conjunto de dados habilitado para perfil para atualizações, primeiro você deve desativar o `unifiedProfile` e, em seguida, reative-a ao lado da `isUpsert` . Isso é feito usando duas solicitações PATCH, uma para desativar e outra para reativar.

>[!WARNING]
>
>Os dados assimilados no conjunto de dados enquanto ele está desativado não serão assimilados na Loja de perfis. É recomendável evitar a assimilação de dados no conjunto de dados até que ele tenha sido reativado para o Perfil.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja atualizar. |

**Solicitação**

O primeiro corpo da solicitação de PATCH inclui um `path` para `unifiedProfile` definir a variável `value` para `enabled:false` para desativar a tag.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

**Resposta**
Uma solicitação bem-sucedida do PATCH retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. O `unifiedProfile` agora foi desativada.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Ativar o conjunto de dados para Perfil e Revigorar {#enable-the-dataset}

Um conjunto de dados existente pode ser ativado para atualizações de Perfil e atributo usando uma única solicitação de PATCH.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja atualizar. |

**Solicitação**

O corpo da solicitação inclui um `path` para `unifiedProfile` definir a variável `value` para incluir a `enabled` e `isUpsert` tags, ambas definidas como `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

**Resposta**
Uma solicitação bem-sucedida do PATCH retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. O `unifiedProfile` agora foi ativada e configurada para atualizações de atributos.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Próximas etapas

Seu perfil e conjunto de dados habilitado para atualização agora podem ser usados por fluxos de trabalho de assimilação em lote e streaming para fazer atualizações nos dados do perfil. Para saber mais sobre como assimilar dados no Adobe Experience Platform, comece lendo o [visão geral da assimilação de dados](../../ingestion/home.md).
