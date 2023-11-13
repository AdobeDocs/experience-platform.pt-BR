---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;habilitar conjunto de dados
title: Ativar um conjunto de dados para atualizações de perfil usando APIs
type: Tutorial
description: Este tutorial mostra como usar APIs do Adobe Experience Platform para ativar um conjunto de dados com recursos de "substituição" a fim de fazer atualizações nos dados do Perfil do cliente em tempo real.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 6985ebf8705130636abdc50b5c3f50299a60f2aa
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 11%

---

# Ativar um conjunto de dados para atualizações de perfil usando APIs

Este tutorial aborda o processo de habilitação de um conjunto de dados com recursos de &quot;substituição&quot; para fazer atualizações nos dados do Perfil do cliente em tempo real. Isso inclui etapas para criar um novo conjunto de dados e configurar um conjunto de dados existente.

>[!NOTE]
>
>O fluxo de trabalho descrito neste tutorial funciona somente para assimilação em lote. Para obter os upserts de assimilação por transmissão, consulte o manual no [envio de atualizações de linhas parciais ao Perfil de cliente em tempo real usando o Preparo de dados](../../data-prep/upserts.md).

## Introdução

Este tutorial requer uma compreensão funcional de vários serviços da Adobe Experience Platform envolvidos no gerenciamento de conjuntos de dados habilitados para perfis. Antes de iniciar este tutorial, revise a documentação desses [!DNL Platform] serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Catalog Service]](../../catalog/home.md): uma API RESTful que permite criar conjuntos de dados e configurá-los para [!DNL Real-Time Customer Profile] e [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a [!DNL Platform] organiza os dados de experiência do cliente.
- [Assimilação em lote](../../ingestion/batch-ingestion/overview.md): a API de assimilação em lote permite assimilar dados no Experience Platform como arquivos em lote.

As seções a seguir fornecem as informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs da plataforma.

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no manual de solução de problemas da [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs da [!DNL Platform], primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem uma `Content-Type` cabeçalho. O valor correto desse cabeçalho é mostrado nas solicitações de exemplo, quando necessário.

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem uma `x-sandbox-name` cabeçalho que especifica o nome da sandbox em que a operação ocorrerá. Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

## Criar um conjunto de dados habilitado para atualizações de perfil

Ao criar um novo conjunto de dados, você pode habilitá-lo para o Perfil e habilitar os recursos de atualização no momento da criação.

>[!NOTE]
>
>Para criar um novo conjunto de dados habilitado para perfil, você deve saber a ID de um esquema XDM existente que está habilitado para o Perfil. Para obter informações sobre como pesquisar ou criar um esquema habilitado para perfil, consulte o tutorial em [criação de um esquema usando a API do registro de esquema](../../xdm/tutorials/create-schema-api.md).

Para criar um conjunto de dados habilitado para Perfil e atualizações, use uma solicitação POST para `/dataSets` terminal.

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

Ao incluir a `unifiedIdentity` e a variável `unifiedProfile` em `tags` no corpo da solicitação, o conjunto de dados será ativado para [!DNL Profile] após a criação. No prazo de `unifiedProfile` matriz, adicionando `isUpsert:true` O adicionará a capacidade do conjunto de dados de oferecer suporte a atualizações.

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
| `schemaRef.id` | A ID do [!DNL Profile]Esquema habilitado para o qual o conjunto de dados será baseado. |
| `{TENANT_ID}` | O namespace dentro do [!DNL Schema Registry] que contém recursos pertencentes à sua organização. Consulte a [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) seção do [!DNL Schema Registry] guia do desenvolvedor para obter mais informações. |

**Resposta**

Uma resposta bem-sucedida mostra uma matriz que contém a ID do conjunto de dados recém-criado na forma de `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurar um conjunto de dados existente {#configure-an-existing-dataset}

As etapas a seguir abordam como configurar um conjunto de dados habilitado para perfil existente para a funcionalidade de atualização (substituição).

>[!NOTE]
>
>Para configurar um conjunto de dados habilitado para perfil existente para substituição, primeiro você deve desabilitar o conjunto de dados para o Perfil e depois reabilitá-lo junto com o `isUpsert` tag. Se o conjunto de dados existente não estiver ativado para o Perfil, você poderá prosseguir diretamente para as etapas para [ativar o conjunto de dados para Perfil e substituição](#enable-the-dataset). Se não tiver certeza, as etapas a seguir mostram como verificar se o conjunto de dados já está habilitado.

### Verifique se o conjunto de dados está ativado para o Perfil

Usar o [!DNL Catalog] , você pode inspecionar um conjunto de dados existente para determinar se ele está ativado para uso no [!DNL Real-Time Customer Profile]. A chamada a seguir recupera os detalhes de um conjunto de dados por ID.

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
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

No `tags` propriedade, você pode ver que `unifiedProfile` está presente com o valor `enabled:true`. Por conseguinte, [!DNL Real-Time Customer Profile] está habilitado para este conjunto de dados.

### Desativar o conjunto de dados para o Perfil

Para configurar um conjunto de dados habilitado para perfil para atualizações, primeiro você deve desabilitar o `unifiedProfile` e `unifiedIdentity` tags e, em seguida, reative-as junto com o `isUpsert` tag. Isso é feito usando duas solicitações PATCH, uma para desativar e outra para reativar.

>[!WARNING]
>
>Os dados assimilados no conjunto de dados enquanto ele estiver desativado não serão assimilados no Armazenamento de perfis. Você deve evitar assimilar dados no conjunto de dados até que ele seja reativado para o Perfil.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID do conjunto de dados que você deseja atualizar. |

**Solicitação**

O corpo da primeira solicitação de PATCH inclui uma `path` para `unifiedProfile` e uma `path` para `unifiedIdentity`, definindo o `value` para `enabled:false` em ambos os caminhos para desativar as tags.

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

Uma solicitação PATCH bem-sucedida retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A variável `unifiedProfile` e `unifiedIdentity` as tags foram desativadas.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Ativar o conjunto de dados para Perfil e substituição {#enable-the-dataset}

Um conjunto de dados existente pode ser ativado para Atualizações de perfil e atributo usando uma única solicitação de PATCH.

>[!IMPORTANT]
>
>Ao ativar o conjunto de dados para o Perfil, verifique se o esquema ao qual o conjunto de dados está associado está **também** Habilitado para perfil. Se o esquema não estiver habilitado para perfil, o conjunto de dados **não** são exibidos como Ativados para perfil na interface do usuário da plataforma.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{DATASET_ID}` | A ID de um conjunto de dados que você deseja atualizar. |

**Solicitação**

O corpo da solicitação inclui uma `path` para `unifiedProfile` definição de `value` para incluir o `enabled` e `isUpsert` tags, ambas definidas como `true`, e uma `path` para `unifiedIdentity` definição de `value` para incluir o `enabled` tag definida como `true`.

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

Uma solicitação PATCH bem-sucedida retorna o Status HTTP 200 (OK) e uma matriz contendo a ID do conjunto de dados atualizado. Essa ID deve corresponder à enviada na solicitação PATCH. A variável `unifiedProfile` tag e `unifiedIdentity` As tags de foram habilitadas e configuradas para atualizações de atributo.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Próximas etapas

O perfil e o conjunto de dados habilitado para substituição agora podem ser usados por fluxos de trabalho de assimilação em lote para fazer atualizações nos dados do perfil. Para saber mais sobre como assimilar dados na Adobe Experience Platform, comece lendo o [visão geral da assimilação de dados](../../ingestion/home.md).
