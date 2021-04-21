---
keywords: Experience Platform, home, tópicos populares, serviço de fluxo de conexão do conjunto de dados, serviço de fluxo, conexão de serviço de fluxo
solution: Experience Platform
title: Criar uma conexão básica do conjunto de dados do Adobe Experience Platform usando a API do Serviço de fluxo
topic-legacy: overview
type: Tutorial
description: Saiba como usar a API do Serviço de fluxo para criar uma conexão básica do conjunto de dados com o Adobe Experience Platform.
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# Crie uma conexão base do conjunto de dados [!DNL Experience Platform] usando a API [!DNL Flow Service]

[!DNL Flow Service] O é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API da qual todas as fontes compatíveis são conectáveis.

Para conectar dados de uma fonte de terceiros a [!DNL Platform], primeiro deve ser estabelecida uma conexão base do conjunto de dados.

Este tutorial usa a API [!DNL Flow Service] para orientá-lo pelas etapas para criar uma conexão base do conjunto de dados.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../xdm/home.md) do Experience Data Model (XDM): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Guia](../../../xdm/api/getting-started.md) do desenvolvedor do Registro de Schema: Inclui informações importantes que você precisa saber para executar com sucesso chamadas para a API do Registro de Esquema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;contêineres&quot; e os cabeçalhos necessários para fazer solicitações (com especial atenção ao cabeçalho Accept e seus possíveis valores).
* [Serviço](../../../catalog/home.md) de catálogo: Catálogo é o sistema de registro para localização e linhagem de dados no  [!DNL Experience Platform].
* [Ingestão](../../../ingestion/batch-ingestion/overview.md) em lote: A API de assimilação em lote permite assimilar dados no Experience Platform como arquivos em lote.
* [Sandboxes](../../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao Data Lake usando a API [!DNL Flow Service].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Flow Service], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* `Content-Type: application/json`

## Pesquisar especificações de conexão

A primeira etapa na criação de uma conexão base do conjunto de dados é recuperar um conjunto de especificações de conexão de dentro de [!DNL Flow Service].

**Formato da API**

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. Você pode pesquisar especificações de conexão para uma conexão base do conjunto de dados executando uma solicitação do GET e usando parâmetros de consulta.

Enviar uma solicitação de GET sem parâmetros de consulta retornará especificações de conexão para todas as fontes disponíveis. Você pode incluir a consulta `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` para obter informações para a conexão base do conjunto de dados.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão de uma conexão base do conjunto de dados.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão e o identificador exclusivo (`id`) necessário para criar uma conexão base.

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## Criar uma conexão base do conjunto de dados

Uma conexão base especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão base do conjunto de dados é necessária, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| Propriedade | Descrição |
| ------------- | --------------- |
| `connectionSpec.id` | A especificação de conexão `id` recuperada na etapa anterior. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão base recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para criar uma conexão de destino e assimilar dados de um conector de origem de terceiros.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão básica do conjunto de dados usando a API [!DNL Flow Service] e obteve o valor de ID exclusivo da conexão. Você pode usar essa conexão base para criar uma conexão de destino. Os seguintes tutoriais percorrem as etapas da criação de uma conexão de destino, dependendo da categoria do conector de origem que você está usando:

* [armazenamento na nuvem](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Sucesso do cliente](./collect/customer-success.md)
* [Banco de dados](./collect/database-nosql.md)
