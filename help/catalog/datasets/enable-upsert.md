---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;habilitar conjunto de dados
title: Ativar um conjunto de dados para atualizações de perfil usando APIs
type: Tutorial
description: Este tutorial mostra como usar APIs do Adobe Experience Platform para ativar um conjunto de dados com recursos de "substituição" a fim de fazer atualizações nos dados do Perfil do cliente em tempo real.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 7%

---

# Ativar um conjunto de dados para atualizações de perfil usando APIs

Este tutorial aborda o processo de habilitação de um conjunto de dados com recursos de &quot;substituição&quot; para fazer atualizações nos dados do Perfil do cliente em tempo real. Isso inclui etapas para criar um novo conjunto de dados e configurar um conjunto de dados existente.

>[!NOTE]
>
>O fluxo de trabalho descrito neste tutorial funciona somente para assimilação em lote. Para obter substituições de assimilação por transmissão, consulte o manual em [envio de atualizações de linhas parciais para o Perfil do cliente em tempo real usando o Preparo de dados](../../data-prep/upserts.md).

## Introdução

Este tutorial requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para perfis. Antes de iniciar este tutorial, reveja a documentação desses serviços [!DNL Experience Platform] relacionados:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Catalog Service]](../../catalog/home.md): uma API RESTful que permite criar conjuntos de dados e configurá-los para [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
- [Assimilação em lote](../../ingestion/batch-ingestion/overview.md): a API de assimilação em lote permite assimilar dados na Experience Platform como arquivos em lote.

As seções a seguir fornecem as informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs do Experience Platform.

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho `Content-Type` adicional. O valor correto desse cabeçalho é mostrado nas solicitações de exemplo, quando necessário.

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para APIs [!DNL Experience Platform] exigem um cabeçalho `x-sandbox-name` que especifique o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Criar um conjunto de dados habilitado para atualizações de perfil

Ao criar um novo conjunto de dados, você pode habilitá-lo para o Perfil e habilitar os recursos de atualização no momento da criação.

>[!NOTE]
>
>Para criar um novo conjunto de dados habilitado para perfil, você deve saber a ID de um esquema XDM existente que está habilitado para o Perfil. Para obter informações sobre como pesquisar ou criar um esquema habilitado para perfil, consulte o tutorial sobre [criação de um esquema usando a API do Registro de Esquema](../../xdm/tutorials/create-schema-api.md).

Para criar um conjunto de dados habilitado para Perfil e atualizações, use uma solicitação POST para o ponto de extremidade `/dataSets`.

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir `unifiedIdentity` e `unifiedProfile` em `tags` no corpo da solicitação, o conjunto de dados será habilitado para [!DNL Profile] após a criação. Na matriz `unifiedProfile`, adicionar `isUpsert:true` adicionará a capacidade do conjunto de dados de oferecer suporte a atualizações.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schemaRef.id` | A ID do esquema habilitado para [!DNL Profile] no qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace no [!DNL Schema Registry] que contém recursos que pertencem à sua organização. Consulte a seção [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) do guia do desenvolvedor do [!DNL Schema Registry] para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz contendo a ID do conjunto de dados recém-criado na forma de `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como configurar um conjunto de dados habilitado para perfil existente para a funcionalidade de atualização (substituição).

>[!NOTE]
>
>Para configurar um conjunto de dados habilitado para perfil existente para substituição, primeiro você deve desabilitar o conjunto de dados para Perfil e depois reabilitá-lo junto com a tag `isUpsert`. Se o conjunto de dados existente não estiver habilitado para o Perfil, você poderá prosseguir diretamente para as etapas para [habilitar o conjunto de dados para Perfil e substituir](#enable-the-dataset). Se não tiver certeza, as etapas a seguir mostram como verificar se o conjunto de dados já está habilitado.

### Verifique se o conjunto de dados está ativado para o Perfil

Usando a API [!DNL Catalog], você pode inspecionar um conjunto de dados existente para determinar se ele está habilitado para uso em [!DNL Real-Time Customer Profile]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

**Formato da API**

```http
GET /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja inspecionar. |

**Solicitação**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Na propriedade `tags`, você pode ver que `unifiedProfile` está presente com o valor `enabled:true`. Portanto, [!DNL Real-Time Customer Profile] está habilitado para este conjunto de dados.

### Desativar o conjunto de dados para o Perfil

Para configurar um conjunto de dados habilitado para atualizações, primeiro você deve desabilitar as marcas `unifiedProfile` e `unifiedIdentity` e depois reabilitá-las junto com a marca `isUpsert`. Isso é feito usando duas solicitações do PATCH, uma para desativar e outra para reativar.

>[!WARNING]
>
>Os dados assimilados no conjunto de dados enquanto ele estiver desativado não serão assimilados no armazenamento de Perfil. Você deve evitar assimilar dados no conjunto de dados até que ele seja reativado para o Perfil.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados que você deseja atualizar. |

**Solicitação**

O primeiro corpo de solicitação PATCH inclui um `path` para `unifiedProfile` e um `path` para `unifiedIdentity`, definindo o `value` para `enabled:false` para ambos os caminhos para desabilitar as marcas.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Resposta**

Uma solicitação bem-sucedida do PATCH retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. As marcas `unifiedProfile` e `unifiedIdentity` foram desabilitadas.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Ativar o conjunto de dados para Perfil e substituição {#enable-the-dataset}

Um conjunto de dados existente pode ser ativado para Atualizações de perfil e atributo usando uma única solicitação do PATCH.

>[!IMPORTANT]
>
>Ao habilitar seu conjunto de dados para o Perfil, verifique se o esquema ao qual o conjunto de dados está associado tem **também** perfil habilitado. Se o esquema não for habilitado para perfil, o conjunto de dados **não** será exibido como habilitado para perfil na interface do Experience Platform.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja atualizar. |

**Solicitação**

O corpo da solicitação inclui uma configuração de `path` a `unifiedProfile` de `value` para incluir as marcas `enabled` e `isUpsert`, ambas definidas como `true`, e uma configuração de `path` a `unifiedIdentity` de `value` para incluir a marca `enabled` definida como `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Resposta**

Uma solicitação bem-sucedida do PATCH retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. As marcas `unifiedProfile` e `unifiedIdentity` foram habilitadas e configuradas para atualizações de atributo.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Próximas etapas

O perfil e o conjunto de dados habilitado para substituição agora podem ser usados por fluxos de trabalho de assimilação em lote para fazer atualizações nos dados do perfil. Para saber mais sobre assimilação de dados na Adobe Experience Platform, comece lendo a [visão geral da assimilação de dados](../../ingestion/home.md).
