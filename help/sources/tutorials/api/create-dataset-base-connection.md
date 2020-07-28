---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar uma conexão básica de conjunto de dados de Experience Platform usando a API de Serviço de Fluxo
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---


# Criar uma conexão básica de [!DNL Experience Platform] conjunto de dados usando a [!DNL Flow Service] API

[!DNL Flow Service] é usada para coletar e centralizar dados do cliente de várias fontes diferentes no Adobe Experience Platform. O serviço fornece uma interface de usuário e uma RESTful API a partir da qual todas as fontes compatíveis são conectáveis.

Para conectar dados de uma fonte de terceiros a [!DNL Platform], é necessário estabelecer primeiro uma conexão de base de conjunto de dados.

Este tutorial usa a [!DNL Flow Service] API para guiá-lo pelas etapas para criar uma conexão básica de conjunto de dados.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Guia](../../../xdm/api/getting-started.md)do desenvolvedor do Registro do Schema: Inclui informações importantes que você precisa saber para executar com êxito chamadas para a API do Registro do Schema. Isso inclui seu `{TENANT_ID}`, o conceito de &quot;container&quot; e os cabeçalhos necessários para fazer solicitações (com atenção especial ao cabeçalho Accept e seus possíveis valores).
* [Serviço](../../../catalog/home.md)de catálogo: Catálogo é o sistema de registro para localização e linhagem de dados dentro [!DNL Experience Platform].
* [Ingestão](../../../ingestion/batch-ingestion/overview.md)em lote: A API de ingestão em lote permite que você ingira dados em Experience Platform como arquivos em lote.
* [Caixas de proteção](../../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao Data Lake usando a [!DNL Flow Service] API.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Flow Service], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Pesquisar especificações de conexão

A primeira etapa na criação de uma conexão base de conjunto de dados é recuperar um conjunto de especificações de conexão de dentro [!DNL Flow Service].

**Formato da API**

Cada fonte disponível tem seu próprio conjunto exclusivo de especificações de conexão para descrever propriedades do conector, como requisitos de autenticação. Você pode procurar especificações de conexão para uma conexão básica de conjunto de dados executando uma solicitação de GET e usando parâmetros de query.

Enviar uma solicitação de GET sem parâmetros de query retornará especificações de conexão para todas as fontes disponíveis. Você pode incluir o query `property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"` para obter informações sobre a conexão básica do conjunto de dados.

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**Solicitação**

A solicitação a seguir recupera as especificações de conexão para uma conexão base de conjunto de dados.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna as especificações de conexão e o identificador exclusivo (`id`) necessário para criar uma conexão básica.

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

## Criar uma conexão básica de conjunto de dados

Uma conexão básica especifica uma fonte e contém suas credenciais para essa fonte. Somente uma conexão base de conjunto de dados é necessária, pois pode ser usada para criar vários conectores de origem para trazer dados diferentes.

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

Uma resposta bem-sucedida retorna detalhes da conexão básica recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para criar uma conexão de público alvo e assimilar dados de um conector de origem de terceiros.

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão básica de conjunto de dados usando a [!DNL Flow Service] API e obteve o valor de ID exclusivo da conexão. Você pode usar essa conexão básica para criar uma conexão de público alvo. Os seguintes tutoriais percorrem as etapas de criação de uma conexão de público alvo, dependendo da categoria do conector de origem que você está usando:

* [armazenamento em nuvem](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [Sucesso do cliente](./collect/customer-success.md)
* [Banco de dados](./collect/database-nosql.md)