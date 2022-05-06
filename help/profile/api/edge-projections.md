---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API
title: Endpoints da API de projeção de borda
topic-legacy: guide
type: Documentation
description: O Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, disponibilizando os dados corretos prontamente e atualizando-os continuamente à medida que as mudanças acontecem. Isso é feito com o uso de bordas, um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis para os aplicativos.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# Endpoints de configurações e destinos de projeção de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente conforme as mudanças acontecem. O Adobe Experience Platform permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e a torna acessível para os aplicativos. Por exemplo, aplicativos Adobe como Adobe Target e Adobe Campaign usam bordas para fornecer experiências personalizadas ao cliente em tempo real. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo as informações específicas que serão disponibilizadas na borda. Este guia fornece instruções detalhadas para usar o [!DNL Real-time Customer Profile] API para trabalhar com projeções de borda, incluindo destinos e configurações.

## Introdução

O endpoint da API usado neste guia faz parte do [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, reveja o [guia de introdução](getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer [!DNL Experience Platform] API.

>[!NOTE]
>
>As solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem uma `Content-Type` cabeçalho. Mais de um `Content-Type` é usada neste documento. Preste especial atenção aos cabeçalhos nas chamadas de amostra para garantir que você esteja usando o método correto `Content-Type` para cada solicitação.

## Destinos de projeção

Uma projeção pode ser roteada para uma ou mais bordas especificando os locais onde os dados devem ser enviados. Cada destino de projeção criado tem uma ID exclusiva que é usada para criar a configuração de projeção.

### Listar todos os destinos

Você pode listar os destinos de borda que já foram criados para sua organização, fazendo uma solicitação do GET para a `/config/destinations` endpoint .

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A resposta inclui um `projectionDestinations` matriz com os detalhes de cada destino mostrados como um objeto individual dentro da matriz. Se nenhuma projeção tiver sido configurada, a variável `projectionDestinations` matriz retorna vazia.

>[!NOTE]
>
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
| `_links.self.href` | No nível superior, corresponde ao caminho usado para fazer a solicitação do GET. Em cada objeto de destino individual, esse caminho pode ser usado em uma solicitação GET para pesquisar diretamente os detalhes de um destino específico. |
| `id` | Em cada objeto de destino, a variável `"id"` mostra a ID exclusiva gerada pelo sistema somente leitura para o destino. Essa ID é usada ao fazer referência a um destino específico e ao criar configurações de projeção. |

Para obter mais informações sobre atributos de um destino individual, consulte a seção sobre [criação de um destino](#create-a-destination) o que se segue.

### Criar um destino {#create-a-destination}

Se o destino necessário ainda não existir, você poderá criar um novo destino de projeção fazendo uma solicitação de POST para a `/config/destinations` endpoint .

**Formato da API**

```http
POST /config/destinations
```

**Solicitação**

A solicitação a seguir cria um novo destino de borda.

>[!NOTE]
>
>A solicitação de POST para criar um destino requer um `Content-Type` conforme mostrado abaixo. Uso de um `Content-Type` resulta em um erro HTTP Status 415 (Unsupported Media Type).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Propriedade | Descrição |
|---|---|
| `type` **(Obrigatório)** | O tipo de destino a ser criado. O único valor aceito, &quot;EDGE&quot;, cria um destino de borda. |
| `dataCenters` **(Obrigatório)** | Um conjunto de strings que lista as bordas em direção às quais as projeções devem ser roteadas. Pode conter um ou mais dos seguintes valores: &quot;OR1&quot; - Estados Unidos ocidentais, &quot;VA5&quot; - Estados Unidos orientais, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Obrigatório)** | Especifica a expiração da projeção. Intervalo de valores aceito: 600 a 604800. Valor padrão: 3600. |
| `replicationPolicy` **(Obrigatório)** | Define o comportamento da replicação de dados do hub para as bordas.  Valores compatíveis: PROATIVO, REATIVO. Valor padrão: REATIVO. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do destino de borda recém-criado, incluindo a ID exclusiva gerada pelo sistema somente leitura (`id`).

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
| `self.href` | Esse caminho é usado para pesquisar (GET) diretamente o destino e também pode ser usado para atualizar (PUT) ou excluir (DELETE) o destino. |
| `id` | A ID exclusiva gerada pelo sistema e somente leitura para o destino. Essa ID é usada para fazer referência ao destino diretamente e ao criar configurações de projeção. |
| `version` | Este valor só de leitura mostra a versão atual do destino. Quando um destino é atualizado, o número da versão é incrementado automaticamente. |

### Exibir um destino

Se você souber a ID exclusiva de um destino de projeção, poderá executar uma solicitação de pesquisa para exibir seus detalhes. Isso é feito fazendo uma solicitação GET para o `/config/destinations` endpoint e incluindo a ID do destino no caminho da solicitação.

**Formato da API**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DESTINATION_ID}` | A ID exclusiva do destino da projeção que você deseja visualizar. |

**Solicitação**

A solicitação a seguir realiza uma pesquisa (GET) para visualizar o destino da ID fornecida no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

O objeto de resposta mostra os detalhes do destino de projeção. O `id` deve corresponder à ID do destino de projeção que foi fornecida na solicitação.

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

Um destino existente pode ser atualizado fazendo uma solicitação de PUT para a `/config/destinations` endpoint e incluindo a ID do destino a ser atualizada no caminho da solicitação. Essa operação basicamente está reescrevendo o destino, portanto, os mesmos atributos devem ser fornecidos no corpo da solicitação como são fornecidos ao criar um novo destino.

>[!CAUTION]
>
>A resposta da API à solicitação de atualização é imediata, no entanto, as alterações nas projeções são aplicadas de forma assíncrona. Em outras palavras, há uma diferença de tempo entre quando a atualização da definição do destino é feita e quando ela é aplicada.

**Formato da API**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DESTINATION_ID}` | A ID exclusiva do destino de projeção que você deseja atualizar. |

**Solicitação**

A solicitação a seguir atualiza o destino existente para incluir um segundo local (`dataCenters`).

>[!IMPORTANT]
>
>A solicitação de PUT requer um `Content-Type` conforme mostrado abaixo. Uso de um `Content-Type` resulta em um erro HTTP Status 415 (Unsupported Media Type).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `currentVersion` | A versão atual do destino existente. O valor da variável `version` ao executar uma solicitação de pesquisa para o destino. |

**Resposta**

A resposta inclui os detalhes atualizados para o destino, incluindo sua ID e o novo `version` do destino.

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

Se sua organização não exigir mais um destino de projeção, ele poderá ser excluído fazendo uma solicitação de DELETE para a `/config/destinations` endpoint e incluindo a ID do destino que você deseja excluir no caminho da solicitação.

>[!CAUTION]
>
>A resposta da API à solicitação de exclusão é imediata, no entanto, as alterações reais nos dados nas bordas ocorrem de forma assíncrona. Em outras palavras, os dados do perfil serão removidos de todas as bordas (a variável `dataCenters` especificado no destino da projeção), mas o processo levará tempo para ser concluído.

**Formato da API**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{DESTINATION_ID}` | A ID exclusiva do destino de projeção que você deseja excluir. |


**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

A solicitação de exclusão retorna o status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio. É possível confirmar que a exclusão foi bem-sucedida ao executar uma solicitação de pesquisa para o destino pela ID. A pesquisa deve retornar o status HTTP 404 (Não encontrado).

## Configurações de projeção

As configurações de projeção fornecem informações sobre quais dados devem estar disponíveis em cada borda. Em vez de projetar uma conclusão [!DNL Experience Data Model] (XDM) para a borda, uma projeção fornece apenas dados específicos, ou campos, do esquema. Sua organização pode definir mais de uma configuração de projeção para cada esquema XDM.

### Listar todas as configurações de projeção

Você pode listar todas as configurações de projeção que foram criadas para sua organização, fazendo uma solicitação de GET para a `/config/projections` endpoint . Você também pode adicionar parâmetros opcionais ao caminho da solicitação para acessar configurações de projeção para um esquema específico ou pesquisar uma projeção individual pelo nome.

**Formato da API**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parâmetro | Descrição |
|---|---|
| `{SCHEMA_NAME}` | O nome da classe schema associada à configuração de projeção que você deseja acessar. |
| `{PROJECTION_NAME}` | O nome da configuração de projeção que você deseja acessar. |

>[!NOTE]
>
>`schemaName` é necessário ao usar a variável `name` , como um nome de configuração de projeção é exclusivo somente no contexto de uma classe de esquema.

**Solicitação**

A solicitação a seguir lista todas as configurações de projeção associadas ao [!DNL Experience Data Model] classe schema, [!DNL XDM Individual Profile]. Para obter mais informações sobre o XDM e sua função no [!DNL Platform]Por favor, comece lendo o [Visão geral do sistema XDM](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de configurações de projeção dentro da raiz `_embedded` , contido no `projectionConfigs` matriz. Se nenhuma configuração de projeção tiver sido feita para sua organização, a variável `projectionConfigs` A matriz ficará vazia.

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
| `{SCHEMA_NAME}` | O nome da classe schema associada à configuração de projeção que você deseja acessar. |

**Solicitação**

>[!NOTE]
>
>A solicitação do POST para criar uma configuração requer um `Content-Type` conforme mostrado abaixo. Uso de um `Content-Type` resulta em um erro HTTP Status 415 (Unsupported Media Type).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Propriedade | Descrição |
|---|---|
| `selector` | Uma string contendo uma lista de propriedades no schema que devem ser replicadas nas bordas. As práticas recomendadas para trabalhar com seletores estão disponíveis na seção [Seletores](#selectors) seção deste documento. |
| `name` | Um nome descritivo para a nova configuração de projeção. |
| `destinationId` | O identificador para o destino da borda para o qual os dados serão projetados. |

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

## Seletores {#selectors}

Um seletor é uma lista separada por vírgulas de nomes de campos XDM. Em uma configuração de projeção, o seletor designa as propriedades a serem incluídas nas projeções. O formato do `selector` o valor do parâmetro é baseado livremente na sintaxe XPath. A sintaxe suportada é resumida abaixo, com exemplos adicionais fornecidos para referência.

### Sintaxe suportada

* Use vírgulas para selecionar vários campos. Não use espaços.
* Use a notação de pontos para selecionar campos aninhados.
   * Por exemplo, para selecionar um campo chamado `field` aninhado dentro de um campo chamado `foo`, use o seletor `foo.field`.
* Ao incluir um campo que contenha subcampos, todos os subcampos também são projetados por padrão. No entanto, é possível filtrar os subcampos retornados usando parênteses `"( )"`.
   * Por exemplo, `addresses(type,city.country)` retorna somente o tipo de endereço e o país em que a cidade do endereço está localizada para cada `addresses` elemento de matriz.
   * O exemplo acima é equivalente a `addresses.type,addresses.city.country`.

>[!NOTE]
>
>A notação de pontos e a notação de parênteses são suportadas para fazer referência a subcampos. No entanto, é uma prática recomendada usar a notação de pontos, pois é mais concisa e fornece uma melhor ilustração da hierarquia de campos.

* Cada campo em um seletor é especificado em relação à raiz da resposta.
   * Se os dados forem uma coleção de recursos, a projeção incluirá uma matriz de recursos.
   * Se os dados forem um único recurso, a projeção incluirá campos relativos a esse recurso.
   * Se o campo selecionado for (ou fizer parte de) uma matriz, a projeção incluirá a parte selecionada de todos os elementos na matriz.

### Exemplos do parâmetro do seletor

Os exemplos a seguir mostram exemplos `selector` parâmetros, seguidos pelos valores estruturados que representam.

**person.lastName**

Retorna o `lastName` subcampo do `person` no recurso solicitado.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**addresses**

Retorna todos os elementos no `addresses` , incluindo todos os campos em cada elemento, mas nenhum outro campo.

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

**person.lastName,addresses**

Retorna o `person.lastName` e todos os elementos no `addresses` matriz.

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

**addresses.city**

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
>
>Sempre que um campo aninhado é retornado, a projeção inclui os objetos pai delimitadores. Os campos pai não incluem nenhum outro campo filho, a menos que também sejam selecionados explicitamente.

**addresses(tipo, cidade)**

Retorna somente os valores da variável `type` e `city` campos para cada elemento na `addresses` matriz. Todos os outros subcampos contidos em cada `addresses` são filtrados.

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

Este guia mostrou as etapas envolvidas para configurar as projeções e os destinos, incluindo como formatar corretamente a variável `selector` parâmetro. Agora você pode criar novos destinos de projeção e configurações específicas às necessidades da sua organização.
