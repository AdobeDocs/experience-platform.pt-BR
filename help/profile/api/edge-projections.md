---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do desenvolvedor da API do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: 5aad9fa71051a58fe1c4678553f47077d81d23fc

---


# Destinos de borda e projeções

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. A plataforma Adobe Experience permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Por exemplo, os aplicativos da Adobe, como o Público alvo da Adobe e o Adobe Campaign, usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda. Este guia fornece instruções detalhadas sobre como usar a API de Perfil do cliente em tempo real para trabalhar com projeções de borda, incluindo destinos e configurações.

## Introdução

Os pontos de extremidade da API usados neste guia fazem parte da API do Perfil do cliente em tempo real. Antes de continuar, leia o guia [do desenvolvedor do Perfil do cliente em tempo](getting-started.md)real. Em particular, a seção [de](getting-started.md#getting-started) introdução do guia do desenvolvedor do Perfil inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para quaisquer APIs da plataforma de experiência.

## Destinos de projeção

Uma projeção pode ser roteada para uma ou mais bordas especificando os locais onde os dados devem ser enviados. Cada destino de projeção criado tem uma ID exclusiva que é usada para criar a configuração de projeção.

### Lista de todos os destinos

Você pode lista os destinos de borda que já foram criados para sua organização, fazendo uma solicitação GET para o `/config/destinations` endpoint.

**Formato da API**

```http
GET /config/destinations
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui uma `projectionDestinations` matriz com os detalhes de cada destino mostrados como um objeto individual dentro da matriz. Se nenhuma projeção tiver sido configurada, o `projectionDestinations` storage retornará vazio.

>[!NOTE]
>Essa resposta foi encurtada por espaço e mostra apenas dois destinos.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Propriedade | Descrição |
|---|---|
| `_links.self.href` | No nível superior, corresponde ao caminho usado para fazer a solicitação GET. Em cada objeto de destino individual, esse caminho pode ser usado em uma solicitação GET para pesquisar os detalhes de um destino específico diretamente. |
| `id` | Em cada objeto de destino, o `"id"` mostra a ID exclusiva gerada pelo sistema e somente leitura para o destino. Essa ID é usada ao fazer referência a um destino específico e ao criar configurações de projeção. |

Para obter mais informações sobre os atributos de um destino individual, consulte a seção sobre como [criar um destino](#create-a-destination) a seguir.

### Criar um destino {#create-a-destination}

Se o destino desejado ainda não existir, você poderá criar um novo destino de projeção, fazendo uma solicitação POST ao `/config/destinations` ponto final.

**Formato da API**

```http
POST /config/destinations
```

**Solicitação**

A solicitação a seguir cria um novo destino de borda.

>[!NOTE]
>A solicitação POST para criar um destino requer um `Content-Type` cabeçalho específico, como mostrado abaixo. O uso de um `Content-Type` cabeçalho incorreto resulta em um erro HTTP Status 415 (Tipo de mídia não suportado).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

|Propriedade|Descrição||`type` **(Obrigatório)** |O tipo de destino a criar. O único valor aceito, &quot;EDGE&quot;, cria um destino de borda.||`dataCenters` **(Obrigatório)** |Uma matriz de string que lista as bordas em direção às projeções a serem roteadas. Pode conter um ou mais dos seguintes valores: &quot;OR1&quot; - Estados Unidos ocidentais, &quot;VA5&quot; - Estados Unidos orientais, &quot;NLD1&quot; - EMEA.||`ttl` **(Obrigatório)** |Especifica a expiração da projeção. Intervalo de valores aceitos: 600 a 604800. Valor padrão: 3600.||`replicationPolicy` **(Obrigatório)** |Define o comportamento da replicação de dados do hub para as bordas.  Valores suportados: PROATIVO, REATIVO. Valor padrão: REATIVO.|

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do destino de borda recém-criado, incluindo a ID exclusiva gerada pelo sistema (somente leitura) (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Propriedade | Descrição |
|---|---|
| `self.href` | Este caminho é usado para pesquisar (GET) o destino diretamente e também pode ser usado para atualizar (PUT) ou excluir (DELETE) o destino. |
| `id` | A ID exclusiva somente leitura gerada pelo sistema para o destino. Essa ID é usada para fazer referência ao destino diretamente e ao criar configurações de projeção. |
| `version` | Esse valor somente leitura mostra a versão atual do destino. Quando um destino é atualizado, o número da versão é incrementado automaticamente. |

### Visualização de um destino

Se você souber a ID exclusiva de um destino de projeção, poderá executar uma solicitação de pesquisa para visualização de seus detalhes. Isso é feito fazendo uma solicitação GET ao ponto de `/config/destinations` extremidade e incluindo a ID do destino no caminho da solicitação.

**Formato da API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DESTINATION_ID}` | A ID exclusiva do destino da projeção que você deseja visualização. |

**Solicitação**

A solicitação a seguir realiza uma pesquisa (GET) para visualização do destino da ID fornecida no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto response mostra os detalhes do destino da projeção. O `id` atributo deve corresponder à ID do destino de projeção fornecido na solicitação.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Atualizar um destino

Um destino existente pode ser atualizado fazendo uma solicitação PUT para o `/config/destinations` ponto de extremidade e incluindo a ID do destino a ser atualizado no caminho da solicitação. Essa operação é essencialmente a _regravação_ do destino, portanto, os mesmos atributos devem ser fornecidos no corpo da solicitação como são fornecidos ao criar um novo destino.

>[!CAUTION]
>A resposta da API à solicitação de atualização é imediata, no entanto, as alterações nas projeções são aplicadas de forma assíncrona. Em outras palavras, há uma diferença de tempo entre quando a atualização da definição de destino é feita e quando é aplicada.

**Formato da API**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DESTINATION_ID}` | A ID exclusiva do destino de projeção que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza o destino existente para incluir um segundo local (`dataCenters`).

>[!IMPORTANT]
>A solicitação PUT requer um `Content-Type` cabeçalho específico, como mostrado abaixo. O uso de um `Content-Type` cabeçalho incorreto resulta em um erro HTTP Status 415 (Tipo de mídia não suportado).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Propriedade | Descrição |
|---|---|
| `currentVersion` | A versão atual do destino existente. O valor do `version` atributo ao executar uma solicitação de pesquisa para o destino. |

**Resposta**

A resposta inclui os detalhes atualizados para o destino, incluindo sua ID e a nova `version` do destino.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Excluir um destino

Se sua organização não exigir mais um destino de projeção, ela poderá ser excluída fazendo uma solicitação DELETE para o `/config/destinations` ponto final e incluindo a ID do destino que você deseja excluir no caminho da solicitação.

>[!CAUTION]
>A resposta da API à solicitação de exclusão é imediata, no entanto, as alterações reais nos dados nas bordas ocorrem de forma assíncrona. Em outras palavras, os dados do perfil serão removidos de todas as bordas (o `dataCenters` especificado no destino da projeção), mas o processo levará tempo para ser concluído.

**Formato da API**

```
DELETE /config/destinations/{DESTINATION_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DESTINATION_ID}` | A ID exclusiva do destino da projeção que você deseja excluir. |


**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A solicitação de exclusão retorna o status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio. Você pode confirmar que a exclusão foi bem-sucedida ao executar uma solicitação de pesquisa para o destino por sua ID. A pesquisa deve retornar o status HTTP 404 (Não encontrado).

## Configurações de projeção

As configurações de projeção fornecem informações sobre quais dados devem estar disponíveis em cada borda. Em vez de projetar um schema completo do Experience Data Model (XDM) para a borda, uma projeção fornece apenas dados específicos ou campos do schema. Sua organização pode definir mais de uma configuração de projeção para cada schema XDM.

### Lista de todas as configurações de projeção

Você pode lista todas as configurações de projeção que foram criadas para sua organização, fazendo uma solicitação GET ao `/config/projections` endpoint. Você também pode adicionar parâmetros opcionais ao caminho de solicitação para acessar configurações de projeção para um schema específico ou pesquisar uma projeção individual pelo nome.

**Formato da API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parâmetro | Descrição |
|---|---|
| `{SCHEMA_NAME}` | O nome da classe de schema associada à configuração de projeção que você deseja acessar. |
| `{PROJECTION_NAME}` | O nome da configuração de projeção que você deseja acessar. |

>[!NOTE]
>`schemaName` é necessário ao usar o `name` parâmetro, já que o nome da configuração de projeção é único somente no contexto de uma classe de schema.

**Solicitação**

A solicitação a seguir lista todas as configurações de projeção associadas à classe de schema do Experience Data Model, Perfil Individual XDM. Para obter mais informações sobre o XDM e sua função na Plataforma, comece lendo a visão geral [do Sistema](../../xdm/home.md)XDM.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de configurações de projeção dentro do `_embedded` atributo raiz, contido na `projectionConfigs` matriz. Se nenhuma configuração de projeção tiver sido feita para sua organização, o `projectionConfigs` storage estará vazio.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Criar uma configuração de projeção

Você pode criar (POST) uma nova configuração de projeção que ditará quais campos XDM serão disponibilizados nas bordas.

**Formato da API**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parâmetro | Descrição |
|---|---|
| `{SCHEMA_NAME}` | O nome da classe de schema associada à configuração de projeção que você deseja acessar. |

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Propriedade | Descrição |
|---|---|
| `selector` | Uma string contendo uma lista de propriedades dentro do schema que devem ser replicadas para as bordas. As práticas recomendadas para trabalhar com seletores estão disponíveis na seção [Seletores](#selectors) deste documento. |
| `name` | Um nome descritivo para a nova configuração de projeção. |
| `destinationId` | O identificador do destino da borda para o qual os dados serão projetados. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da configuração de projeção recém-criada.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Selectors {#selectors}

Um seletor é uma lista separada por vírgulas de nomes de campos XDM. Numa configuração de projeção, o seletor designa as propriedades a serem incluídas nas projeções. O formato do valor do `selector` parâmetro é livremente baseado na sintaxe XPath. A sintaxe suportada é resumida abaixo, com exemplos adicionais fornecidos para referência.

### Sintaxe suportada

* Use vírgulas para selecionar vários campos. Não use espaços.
* Use a notação de pontos para selecionar campos aninhados.
   * Por exemplo, para selecionar um campo com o nome `field` aninhado dentro de um campo com o nome `foo`, use o seletor `foo.field`.
* Ao incluir um campo que contenha subcampos, todos os subcampos também são projetados por padrão. Entretanto, é possível filtrar os subcampos retornados usando parênteses `"( )"`.
   * Por exemplo, `addresses(type,city.country)` retorna somente o tipo de endereço e o país em que a cidade do endereço está localizada para cada elemento de `addresses` matriz.
   * O exemplo acima equivale a `addresses.type,addresses.city.country`.

>[!NOTE]
>A notação de pontos e a notação entre parênteses são suportadas para fazer referência a subcampos. No entanto, a prática recomendada é usar a notação de pontos porque é mais concisa e fornece uma melhor ilustração da hierarquia de campos.

* Cada campo em um seletor é especificado em relação à raiz da resposta.
   * Se os dados forem uma coleção de recursos, a projeção incluirá uma gama de recursos.
   * Se os dados forem um único recurso, a projeção incluirá campos relativos a esse recurso.
   * Se o campo selecionado for (ou fizer parte de) um storage, a projeção incluirá a parte selecionada de todos os elementos no storage.

### Exemplos do parâmetro do seletor

Os exemplos a seguir mostram `selector` parâmetros de amostra, seguidos pelos valores estruturados que representam.

**people.lastName**

Retorna o `lastName` subcampo do `person` objeto no recurso solicitado.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**endereços**

Retorna todos os elementos na `addresses` matriz, incluindo todos os campos em cada elemento, mas nenhum outro campo.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**people.lastName,address**

Retorna o `person.lastName` campo e todos os elementos na `addresses` matriz.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**address.city**

Retorna somente o campo cidade para todos os elementos na matriz de endereços.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>Sempre que um campo aninhado é retornado, a projeção inclui os objetos pai circundantes. Os campos pai não incluem quaisquer outros campos filho, a menos que também sejam selecionados explicitamente.

**endereços(tipo,cidade)**

Retorna somente os valores dos campos `type` e `city` para cada elemento na `addresses` matriz. Todos os outros subcampos contidos em cada `addresses` elemento são filtrados.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Próximas etapas

Este guia mostra as etapas envolvidas para configurar projeções de borda e destinos, incluindo como formatar corretamente o `selector` parâmetro. Agora você pode criar novos destinos de borda e projeções específicas às necessidades de sua organização. Para descobrir ações adicionais disponíveis por meio da API do Perfil, consulte o guia [do desenvolvedor da API do Perfil do cliente em tempo](getting-started.md)real.