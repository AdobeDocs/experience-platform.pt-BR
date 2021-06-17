---
keywords: Experience Platform, home, tópicos populares, guia do desenvolvedor do sandbox
solution: Experience Platform
title: Endpoint da API de gerenciamento de sandbox
topic-legacy: developer guide
description: O endpoint /sandboxes na API do Sandbox permite gerenciar sandboxes de forma programática no Adobe Experience Platform.
source-git-commit: 1ec141fa5a13bb4ca6a4ec57f597f38802a92b3f
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 2%

---

# Ponto de extremidade de gerenciamento de sandbox

As sandboxes no Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar seu ambiente de produção. O endpoint `/sandboxes` na API [!DNL Sandbox] permite gerenciar programaticamente as sandboxes na plataforma.

## Introdução

O endpoint da API usado neste guia faz parte da [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de sandboxes {#list}

Você pode listar todas as sandboxes pertencentes à sua Organização IMS (ativa ou não), fazendo uma solicitação do GET para o endpoint `/sandboxes`.

**Formato da API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Parâmetros de consulta opcionais para filtrar os resultados por. Consulte a seção em [parâmetros de consulta](./appendix.md#query) para obter mais informações. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de sandboxes pertencentes à sua organização, incluindo detalhes como `name`, `title`, `state` e `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sandbox. Essa propriedade é usada para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da sandbox. |
| `state` | O estado de processamento atual da sandbox. O estado de uma sandbox pode ser qualquer um dos seguintes: <br/><ul><li>`creating`: A sandbox foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>`active`: A sandbox é criada e ativa.</li><li>`failed`: Devido a um erro, a sandbox não pôde ser provisionada pelo sistema e está desativada.</li><li>`deleted`: A sandbox foi desativada manualmente.</li></ul> |
| `type` | O tipo de sandbox. Os tipos de sandbox atuais suportados incluem `development` e `production`. |
| `isDefault` | Uma propriedade booleana que indica se essa sandbox é a sandbox de produção padrão da organização. |
| `eTag` | Um identificador para uma versão específica da sandbox. Usado para controle de versão e eficiência de armazenamento em cache, esse valor é atualizado sempre que uma alteração é feita na sandbox. |

## Procurar uma sandbox {#lookup}

Você pode pesquisar uma sandbox individual fazendo uma solicitação do GET que inclui a propriedade `name` da sandbox no caminho da solicitação.

**Formato da API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja procurar. |

**Solicitação**

A solicitação a seguir recupera uma sandbox chamada &quot;dev-2&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox, incluindo `name`, `title`, `state` e `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome da sandbox. Essa propriedade é usada para fins de pesquisa em chamadas de API. |
| `title` | O nome de exibição da sandbox. |
| `state` | O estado de processamento atual da sandbox. O estado de uma sandbox pode ser qualquer um dos seguintes: <ul><li>**criação**: A sandbox foi criada, mas ainda está sendo provisionada pelo sistema.</li><li>**ativo**: A sandbox é criada e ativa.</li><li>**falhou**: Devido a um erro, a sandbox não pôde ser provisionada pelo sistema e está desativada.</li><li>**suprimido**: A sandbox foi desativada manualmente.</li></ul> |
| `type` | O tipo de sandbox. Os tipos atuais de sandbox compatíveis incluem: `development` e `production`. |
| `isDefault` | Uma propriedade booleana que indica se essa sandbox é a sandbox padrão da organização. Normalmente, essa é a sandbox de produção. |
| `eTag` | Um identificador para uma versão específica da sandbox. Usado para controle de versão e eficiência de armazenamento em cache, esse valor é atualizado sempre que uma alteração é feita na sandbox. |

## Criar uma sandbox {#create}

Você pode criar uma nova sandbox de desenvolvimento ou produção, fazendo uma solicitação POST para o endpoint `/sandboxes`.

### Criar uma sandbox de desenvolvimento

Para criar uma sandbox de desenvolvimento, você deve fornecer um atributo `type` com um valor `development` na carga da solicitação.

**Formato da API**

```http
POST /sandboxes
```

**Solicitação**

A solicitação a seguir cria uma nova sandbox de desenvolvimento chamada &quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O identificador que será usado para acessar a sandbox em solicitações futuras. Esse valor deve ser exclusivo, e a prática recomendada é torná-lo o mais descritivo possível. Esse valor não pode conter espaços ou caracteres especiais. |
| `title` | Um nome legível usado para fins de exibição na interface do usuário da plataforma. |
| `type` | O tipo de sandbox a ser criado. Para uma sandbox de não produção, esse valor deve ser `development`. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox recém-criada, mostrando que seu `state` está &quot;criando&quot;.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>As sandboxes levam aproximadamente 30 segundos para serem provisionadas pelo sistema, depois elas `state` se tornarão &quot;ativas&quot; ou &quot;com falha&quot;.

### Criar uma sandbox de produção

Para criar uma sandbox de produção, você deve fornecer um atributo `type` com um valor `production` na carga da solicitação.

**Formato da API**

```http
POST /sandboxes
```

**Solicitação**

A solicitação a seguir cria uma nova sandbox de produção chamada &quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O identificador que será usado para acessar a sandbox em solicitações futuras. Esse valor deve ser exclusivo, e a prática recomendada é torná-lo o mais descritivo possível. Esse valor não pode conter espaços ou caracteres especiais. |
| `title` | Um nome legível usado para fins de exibição na interface do usuário da plataforma. |
| `type` | O tipo de sandbox a ser criado. Para uma sandbox de produção, esse valor deve ser `production`. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox recém-criada, mostrando que seu `state` está &quot;criando&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>As sandboxes levam aproximadamente 30 segundos para serem provisionadas pelo sistema, depois elas `state` se tornarão &quot;ativas&quot; ou &quot;com falha&quot;.

## Atualizar uma sandbox {#put}

Você pode atualizar um ou mais campos em uma sandbox fazendo uma solicitação de PATCH que inclui o sandbox `name` no caminho da solicitação e a propriedade a ser atualizada no payload da solicitação.

>[!NOTE]
>
>Atualmente, somente a propriedade `title` de uma sandbox pode ser atualizada.

**Formato da API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza a propriedade `title` da sandbox chamada &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) com os detalhes da sandbox recém-atualizada.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Redefinir uma sandbox {#reset}

As sandboxes têm um recurso de &quot;redefinição de fábrica&quot; que exclui todos os recursos não padrão de uma sandbox. Você pode redefinir uma sandbox fazendo uma solicitação de PUT que inclui o `name` da sandbox no caminho da solicitação.

**Formato da API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja redefinir. |
| `validationOnly` | Um parâmetro opcional que permite fazer uma verificação prévia na operação de redefinição da sandbox sem fazer a solicitação real. Defina esse parâmetro como `validationOnly=true` para verificar se a sandbox que você está prestes a redefinir contém qualquer Adobe Analytics, Adobe Audience Manager ou segmento que compartilha dados. |

**Solicitação**

A solicitação a seguir redefine uma sandbox chamada &quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `action` | Esse parâmetro deve ser fornecido na carga da solicitação com um valor de &quot;redefinir&quot; para redefinir a sandbox. |

**Resposta**

>[!NOTE]
>
>Depois que uma sandbox é redefinida, leva aproximadamente 30 segundos para ser provisionada pelo sistema.

Uma resposta bem-sucedida retorna os detalhes da sandbox atualizada, mostrando que seu `state` é uma &quot;redefinição&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

A sandbox de produção padrão e qualquer sandbox de produção criada pelo usuário não podem ser redefinidas se o gráfico de identidade hospedado nela também estiver sendo usado pelo Adobe Analytics para o recurso [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) ou se o gráfico de identidade hospedado nele também estiver sendo usado pelo Adobe Audience Manager para o recurso [Destinos baseados em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).

Veja a seguir uma lista de possíveis exceções que podem impedir a redefinição de uma sandbox:

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

Você pode continuar a redefinir uma sandbox de produção que é usada para o compartilhamento de segmentos bidirecionais com [!DNL Audience Manager] ou [!DNL Audience Core Service] adicionando o parâmetro `ignoreWarnings` à solicitação.

**Formato da API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | A propriedade `name` da sandbox que você deseja redefinir. |
| `ignoreWarnings` | Um parâmetro opcional que permite ignorar a verificação de validação e forçar a redefinição de uma sandbox de produção usada para o compartilhamento de segmentos bidirecionais com [!DNL Audience Manager] ou [!DNL Audience Core Service]. Esse parâmetro não pode ser aplicado a uma sandbox de produção padrão. |

**Solicitação**

A solicitação a seguir redefine uma sandbox de produção chamada &quot;acme&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da sandbox atualizada, mostrando que seu `state` é uma &quot;redefinição&quot;.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Excluir uma sandbox {#delete}

>[!IMPORTANT]
>
>A sandbox de produção padrão não pode ser excluída.

Você pode excluir uma sandbox fazendo uma solicitação de DELETE que inclui o `name` da sandbox no caminho da solicitação.

>[!NOTE]
>
>Fazer essa chamada de API atualiza a propriedade `status` da sandbox para &quot;deletada&quot; e a desativa. As solicitações do GET ainda podem recuperar os detalhes da sandbox depois que ela for excluída.

**Formato da API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Parâmetro | Descrição |
| --- | --- |
| `{SANDBOX_NAME}` | O `name` da sandbox que você deseja excluir. |
| `validationOnly` | Um parâmetro opcional que permite fazer uma verificação prévia na operação de exclusão da sandbox sem fazer a solicitação real. Defina esse parâmetro como `validationOnly=true` para verificar se a sandbox que você está prestes a redefinir contém qualquer Adobe Analytics, Adobe Audience Manager ou segmento que compartilha dados. |
| `ignoreWarnings` | Um parâmetro opcional que permite ignorar a verificação de validação e forçar a exclusão de uma sandbox de produção criada pelo usuário, usada para o compartilhamento de segmentos bidirecionais com [!DNL Audience Manager] ou [!DNL Audience Core Service]. Esse parâmetro não pode ser aplicado a uma sandbox de produção padrão. |

**Solicitação**

A solicitação a seguir exclui uma sandbox de produção chamada &quot;acme&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes atualizados da sandbox, mostrando que seu `state` é &quot;excluído&quot;.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
