---
keywords: Experience Platform;home;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquemas;Registro de esquemas;descritor;Descritor;descritores;Descritores;identidade;identidade;nome amigável;nome amigável;alternatedisplayinfo;referência;referência;relacionamento;Relação
solution: Experience Platform
title: Endpoint da API de descritores
description: O ponto de extremidade /descriptors na API do registro de esquema permite gerenciar programaticamente os descritores XDM no aplicativo de experiência.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 02a22362b9ecbfc5fd7fcf17dc167309a0ea45d5
workflow-type: tm+mt
source-wordcount: '2888'
ht-degree: 1%

---

# Ponto de extremidade de descritores

Os esquemas definem a estrutura das entidades de dados, mas não especificam como os conjuntos de dados criados a partir desses esquemas se relacionam entre si. No Adobe Experience Platform, você pode usar descritores para descrever esses relacionamentos e adicionar metadados interpretativos a um esquema.

Os descritores são objetos de metadados em nível de locatário aplicados a esquemas no Adobe Experience Platform. Eles definem relações estruturais, chaves e campos comportamentais (como carimbos de data e hora ou controle de versão) que influenciam como os dados são validados, unidos ou interpretados downstream.

Um esquema pode ter um ou mais descritores. Cada descritor define um `@type` e o `sourceSchema` ao qual ele se aplica. O descritor se aplica automaticamente a todos os conjuntos de dados criados a partir desse esquema.

No Adobe Experience Platform, um descritor são metadados que adicionam regras comportamentais ou significado estrutural a um esquema.
Há vários tipos de descritores, incluindo:

- [Descritor de identidade](#identity-descriptor) - marca um campo como uma identidade
- [Descritor de chave primária](#primary-key-descriptor) - impõe exclusividade
- [Descritor de relacionamento](#relationship-descriptor) - define uma associação de chave estrangeira
- [Descritor de informações de exibição alternativo](#friendly-name) - permite renomear um campo na interface
- Descritores de [Versão](#version-descriptor) e [carimbo de data/hora](#timestamp-descriptor) - rastrear a ordenação de eventos e a detecção de alterações

O ponto de extremidade `/descriptors` na API [!DNL Schema Registry] permite gerenciar de forma programática os descritores no aplicativo de experiência.

## Introdução

O ponto de extremidade usado neste guia faz parte da [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

Além dos descritores padrão, o [!DNL Schema Registry] dá suporte a tipos de descritores para esquemas baseados em modelo, como **chave primária**, **versão** e **carimbo de data/hora**. Eles impõem exclusividade, controlam versão e definem campos de série temporal no nível do esquema. Se você não estiver familiarizado com esquemas baseados em modelo, revise a [visão geral do Data Mirror](../data-mirror/overview.md) e a [referência técnica de esquemas baseados em modelo](../schema/model-based.md) antes de continuar.

>[!IMPORTANT]
>
>Consulte o [Apêndice](#defining-descriptors) para obter detalhes sobre todos os tipos de descritor.

## Recuperar uma lista de descritores {#list}

Você pode listar todos os descritores que foram definidos pela sua organização fazendo uma solicitação GET para `/tenant/descriptors`.

**Formato da API**

```http
GET /tenant/descriptors
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

O formato da resposta depende do cabeçalho `Accept` enviado na solicitação. Observe que o ponto de extremidade `/descriptors` usa `Accept` cabeçalhos que são diferentes de todos os outros pontos de extremidade na API [!DNL Schema Registry].

>[!IMPORTANT]
>
>Os descritores exigem cabeçalhos `Accept` exclusivos que substituem `xed` por `xdm` e também oferecem uma opção `link` exclusiva aos descritores. Os cabeçalhos `Accept` adequados foram incluídos nas chamadas de exemplo abaixo, mas tenha cuidado extra para garantir que os cabeçalhos corretos estejam sendo usados ao trabalhar com descritores.

| Cabeçalho `Accept` | Descrição |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Retorna uma matriz de IDs de descritor |
| `application/vnd.adobe.xdm-link+json` | Retorna uma matriz de caminhos de API do descritor |
| `application/vnd.adobe.xdm+json` | Retorna uma matriz de objetos de descritor expandidos |
| `application/vnd.adobe.xdm-v2+json` | Este cabeçalho `Accept` deve ser usado para usar recursos de paginação. |

{style="table-layout:auto"}

**Resposta**

A resposta inclui uma matriz para cada tipo de descritor que tem descritores definidos. Em outras palavras, se não houver descritores de um determinado `@type` definido, o registro não retornará uma matriz vazia para esse tipo de descritor.

Ao usar o cabeçalho `link` `Accept`, cada descritor é mostrado como um item de matriz no formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Pesquisar um descritor {#lookup}

Para exibir os detalhes de um descritor específico, envie uma solicitação GET usando seu `@id`.

**Formato da API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que você deseja pesquisar. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir recupera um descritor por seu valor `@id`. Os descritores não têm controle de versão, portanto, nenhum cabeçalho `Accept` é necessário na solicitação de pesquisa.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor, incluindo seus `@type` e `sourceSchema`, bem como informações adicionais que variam dependendo do tipo de descritor. O `@id` retornado deve corresponder ao descritor `@id` fornecido na solicitação.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Criar um descritor {#create}

Você pode criar um novo descritor fazendo uma solicitação POST para o ponto de extremidade `/tenant/descriptors`.

>[!IMPORTANT]
>
>O [!DNL Schema Registry] permite definir vários tipos de descritores diferentes. Cada tipo de descritor exige que seus próprios campos específicos sejam enviados no corpo da solicitação. Consulte o [apêndice](#defining-descriptors) para obter uma lista completa de descritores e os campos necessários para defini-los.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um esquema de amostra. Isso instrui [!DNL Experience Platform] a usar o endereço de email como um identificador para ajudar a compilar as informações sobre o indivíduo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes do descritor recém-criado, incluindo seu `@id`. `@id` é um campo somente leitura atribuído por [!DNL Schema Registry] e usado para fazer referência ao descritor na API.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Atualizar um descritor {#put}

Você pode atualizar um descritor incluindo seu `@id` no caminho de uma solicitação PUT.

**Formato da API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que você deseja atualizar. |

{style="table-layout:auto"}

**Solicitação**

Essa solicitação reescreve essencialmente o descritor, de modo que o corpo da solicitação deve incluir todos os campos necessários para definir um descritor desse tipo. Em outras palavras, a carga da solicitação para atualizar (PUT) um descritor é a mesma que a carga para [criar (POST) um descritor](#create) do mesmo tipo.

>[!IMPORTANT]
>
>Assim como na criação de descritores usando solicitações POST, cada tipo de descritor requer que seus próprios campos específicos sejam enviados em cargas de solicitação PUT. Consulte o [apêndice](#defining-descriptors) para obter uma lista completa de descritores e os campos necessários para defini-los.

O exemplo a seguir atualiza um descritor de identidade para fazer referência a um `xdm:sourceProperty` (`mobile phone`) diferente e alterar o `xdm:namespace` para `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e o `@id` do descritor atualizado (que deve corresponder ao `@id` enviado na solicitação).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Executar uma [solicitação de pesquisa (GET)](#lookup) para exibir o descritor mostra que os campos foram atualizados para refletir as alterações enviadas na solicitação PUT.

## Excluir um descritor {#delete}

Ocasionalmente, talvez seja necessário remover um descritor definido de [!DNL Schema Registry]. Isso é feito fazendo uma solicitação DELETE referenciando o `@id` do descritor que você deseja remover.

**Formato da API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que você deseja excluir. |

{style="table-layout:auto"}

**Solicitação**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Para confirmar se o descritor foi excluído, você pode executar uma [solicitação de pesquisa](#lookup) em relação ao descritor `@id`. A resposta retorna o status HTTP 404 (Não Encontrado) porque o descritor foi removido de [!DNL Schema Registry].

## Apêndice {#appendix}

A seção a seguir fornece informações adicionais sobre como trabalhar com descritores na API [!DNL Schema Registry].

### Definição de descritores {#defining-descriptors}

>[!NOTE]
>
>O número máximo de descritores que podem ser aplicados à sandbox de uma organização é 4000.

As seções a seguir fornecem uma visão geral dos tipos de descritores disponíveis, incluindo os campos obrigatórios para definir um descritor de cada tipo.

>[!IMPORTANT]
>
>Não é possível rotular o objeto de namespace do locatário, pois o sistema aplicaria esse rótulo a cada campo personalizado nessa sandbox. Em vez disso, você deve especificar o nó de folha sob esse objeto que você precisa rotular.

#### Descritor de identidade {#identity-descriptor}

Um descritor de identidade indica que &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; é um campo [!DNL Identity], conforme descrito pelo [Serviço de Identidade da Experience Platform](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de identidade, este valor deve ser definido como `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | O URI `$id` do esquema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do esquema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | O valor `id` ou `code` do namespace de identidade. Uma lista de namespaces pode ser encontrada usando o [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | `xdm:id` ou `xdm:code`, dependendo do `xdm:namespace` usado. |
| `xdm:isPrimary` | Um valor booleano opcional. Quando verdadeiro, indica o campo como a identidade principal. Os esquemas podem conter apenas uma identidade principal. |

{style="table-layout:auto"}

#### Descritor de nome amigável {#friendly-name}

Descritores de nome amigável permitem que um usuário modifique os valores `title`, `description` e `meta:enum` dos campos de esquema da biblioteca principal. Especialmente úteis ao trabalhar com &quot;eVars&quot; e outros campos &quot;genéricos&quot; que você deseja rotular como contendo informações específicas da organização. A interface pode usá-los para mostrar um nome mais amigável ou para mostrar apenas campos que tenham um nome amigável.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de nome amigável, esse valor deve ser definido como `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | O URI `$id` do esquema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do esquema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica cujos detalhes você deseja modificar. O caminho deve começar com uma barra (`/`) e não terminar com uma. Não inclua `properties` no caminho (por exemplo, use `/personalEmail/address` em vez de `/properties/personalEmail/properties/address`). |
| `xdm:title` | O novo título que você deseja exibir para este campo, escrito em Primeira letra maiúscula. |
| `xdm:description` | Uma descrição opcional pode ser adicionada junto com o título. |
| `meta:enum` | Se o campo indicado por `xdm:sourceProperty` for um campo de cadeia de caracteres, `meta:enum` poderá ser usado para adicionar os valores sugeridos para o campo na interface de segmentação. É importante observar que `meta:enum` não declara uma enumeração nem fornece validação de dados para o campo XDM.<br><br>Isso só deve ser usado para campos XDM principais definidos pelo Adobe. Se a propriedade de origem for um campo personalizado definido por sua organização, você deverá editar a propriedade `meta:enum` do campo diretamente por meio de uma solicitação PATCH para o recurso principal do campo. |
| `meta:excludeMetaEnum` | Se o campo indicado por `xdm:sourceProperty` for um campo de cadeia de caracteres que tenha valores sugeridos existentes fornecidos em um campo `meta:enum`, você poderá incluir esse objeto em um descritor de nome amigável para excluir alguns ou todos esses valores da segmentação. A chave e o valor de cada entrada devem corresponder àqueles incluídos na `meta:enum` original do campo para que a entrada seja excluída. |

{style="table-layout:auto"}

#### Descritor de relacionamento {#relationship-descriptor}

Os descritores de relacionamento descrevem uma relação entre dois esquemas diferentes, digitados nas propriedades descritas em `xdm:sourceProperty` e `xdm:destinationProperty`. Consulte o tutorial em [definindo uma relação entre dois esquemas](../tutorials/relationship-api.md) para obter mais informações.

Use estas propriedades para declarar como um campo de origem (chave estrangeira) se relaciona a um campo de destino ([chave primária](#primary-key-descriptor) ou chave candidata).

>[!TIP]
>
>Uma **chave estrangeira** é um campo no esquema de origem (definido por `xdm:sourceProperty`) que faz referência a um campo de chave em outro esquema. Uma **chave candidata** é qualquer campo (ou conjunto de campos) no esquema de destino que identifica exclusivamente um registro e pode ser usada em vez da chave primária.

A API oferece suporte a dois padrões:

- `xdm:descriptorOneToOne`: relação padrão 1:1.
- `xdm:descriptorRelationship`: padrão geral para novos esquemas de trabalho e baseados em modelo (suporta cardinalidade, nomeação e alvos de chave não primária).

##### Relação um para um (esquemas padrão)

Use isso ao manter integrações de esquema padrão existentes que já dependem de `xdm:descriptorOneToOne`.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

A tabela a seguir descreve os campos necessários para definir um descritor de relacionamento um para um.

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de relacionamento, esse valor deve ser definido como `xdm:descriptorOneToOne`, a menos que você tenha acesso ao Real-Time CDP B2B edition. Com o B2B edition você tem a opção de usar `xdm:descriptorOneToOne` ou [`xdm:descriptorRelationship`](#b2b-relationship-descriptor). |
| `xdm:sourceSchema` | O URI `$id` do esquema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do esquema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no esquema de origem em que a relação está sendo definida. Deve começar com &quot;/&quot; e não terminar com &quot;/&quot;. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | O URI `$id` do esquema de referência com o qual este descritor está definindo uma relação. |
| `xdm:destinationVersion` | A versão principal do esquema de referência. |
| `xdm:destinationProperty` | (Opcional) Caminho para um campo de destino no esquema de referência. Se essa propriedade for omitida, o campo de destino será inferido por quaisquer campos que contenham um descritor de identidade de referência correspondente (veja abaixo). |

##### Relação geral (esquemas baseados em modelo e recomendados para novos projetos)

Use esse descritor para todas as novas implementações e para esquemas baseados em modelo. Ela permite definir a cardinalidade da relação (como um para um ou muitos para um), especificar nomes de relação e vincular a um campo de destino que não seja a chave primária (chave não primária).

Os exemplos a seguir mostram como definir um descritor de relacionamento geral.

**Exemplo mínimo:**

Este exemplo mínimo inclui apenas os campos necessários para definir uma relação muitos para um entre dois schemas.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**Exemplo com todos os campos opcionais:**

Este exemplo inclui todos os campos opcionais, como nomes de relacionamento, títulos de exibição e um campo de destino de chave não primária explícito.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### Escolha de um descritor de relacionamento

Use as diretrizes a seguir para decidir qual descritor de relacionamento aplicar:

| Situação | Descritor a ser usado |
| --------------------------------------------------------------------- | ----------------------------------------- |
| Novos esquemas baseados em trabalho ou modelo | `xdm:descriptorRelationship` |
| Mapeamento 1:1 existente em esquemas padrão | Continue usando o `xdm:descriptorOneToOne` a menos que precise de recursos com suporte apenas do `xdm:descriptorRelationship`. |
| É necessária uma cardinalidade de muitos para um ou opcional (`1:1`, `1:0`, `M:1`, `M:0`) | `xdm:descriptorRelationship` |
| São necessários nomes ou títulos de relacionamento para legibilidade da interface do usuário/downstream | `xdm:descriptorRelationship` |
| É necessário um destino que não seja uma identidade | `xdm:descriptorRelationship` |

>[!NOTE]
>
>Para descritores `xdm:descriptorOneToOne` existentes em esquemas padrão, continue usando-os a menos que precise de recursos como destinos de identidade não primários, nomenclatura personalizada ou opções de cardinalidade expandidas.

##### Comparação de recursos

A tabela a seguir compara os recursos dos dois tipos de descritor:

| Recurso | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| Cardinalidade | 1:1 | 1:1, 1:0, M:1, M:0 (informativo) |
| Destino | Campo de identidade/explícito | Chave primária por padrão, ou chave não primária via `xdm:destinationProperty` |
| Nomeação de campos | Incompatível | `xdm:sourceToDestinationName`, `xdm:destinationToSourceName` e títulos |
| Ajuste relacional | Limitado | Padrão principal para esquemas baseados em modelo |

##### Restrições e validação

Siga estes requisitos e recomendações ao definir um descritor de relacionamento geral:

- Para esquemas baseados em modelo, coloque o campo de origem (chave estrangeira) no nível raiz. Essa é uma limitação técnica atual para assimilação, não apenas uma recomendação de práticas recomendadas.
- Verifique se os tipos de dados dos campos de origem e destino são compatíveis (numérico, data, booleano, string).
- Lembre-se de que a cardinalidade é informativa; o armazenamento não a impõe. Especifique a cardinalidade no formato `<source>:<destination>`. Os valores aceitos são: `1:1`, `1:0`, `M:1` ou `M:0`.

#### Descritor de chave primária {#primary-key-descriptor}

O descritor de chave primária (`xdm:descriptorPrimaryKey`) impõe restrições de exclusividade e não nulas em um ou mais campos em um esquema.

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| Propriedade | Descrição |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | Deve ser `xdm:descriptorPrimaryKey`. |
| `xdm:sourceSchema` | `$id` URI do esquema. |
| `xdm:sourceProperty` | Ponteiro(s) JSON para o(s) campo(s) de chave primária. Use uma matriz para chaves compostas. Para esquemas de série temporal, a chave composta deve incluir o campo de carimbo de data e hora para garantir exclusividade em registros de evento. |

#### Descritor de versão {#version-descriptor}

>[!NOTE]
>
>No Editor de Esquema da Interface do Usuário, o descritor de versão aparece como &quot;[ !UICOTRNOL Identificador de versão]&quot;.

O descritor de versão (`xdm:descriptorVersion`) designa um campo para detectar e evitar conflitos de eventos de alteração fora de ordem.

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| Propriedade | Descrição |
| -------------------- | ------------------------------------------------------------- |
| `@type` | Deve ser `xdm:descriptorVersion`. |
| `xdm:sourceSchema` | `$id` URI do esquema. |
| `xdm:sourceProperty` | Ponteiro JSON para o campo de versão. Deve ser marcado como `required`. |

#### Descritor de carimbo de data e hora {#timestamp-descriptor}

>[!NOTE]
>
>No Editor de Esquema de Interface do Usuário, o descritor de carimbo de data/hora aparece como &quot;[ !UICOTRNOL Identificador de carimbo de data/hora]&quot;.

O descritor de carimbo de data/hora (`xdm:descriptorTimestamp`) designa um campo de data/hora como carimbo de data/hora para esquemas com `"meta:behaviorType": "time-series"`.

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| Propriedade | Descrição |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | Deve ser `xdm:descriptorTimestamp`. |
| `xdm:sourceSchema` | `$id` URI do esquema. |
| `xdm:sourceProperty` | Ponteiro JSON para o campo de carimbo de data e hora. Deve ser marcado como `required` e ser do tipo `date-time`. |

##### Descritor de relacionamento B2B {#B2B-relationship-descriptor}

O Real-Time CDP B2B edition apresenta uma maneira alternativa de definir relações entre esquemas, o que permite relações muitos para um. Esta nova relação deve ter o tipo `@type: xdm:descriptorRelationship` e a carga deve incluir mais campos do que a relação `@type: xdm:descriptorOneToOne`. Consulte o tutorial sobre [definição de uma relação de esquema para o B2B edition](../tutorials/relationship-b2b.md) para obter mais informações.

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para nós com os campos a seguir, o valor deve ser definido como `xdm:descriptorRelationship`. Para obter informações sobre tipos adicionais, consulte a seção [descritores de relacionamento](#relationship-descriptor). |
| `xdm:sourceSchema` | O URI `$id` do esquema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do esquema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no esquema de origem em que a relação está sendo definida. Deve começar com &quot;/&quot; e não terminar com &quot;/&quot;. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | O URI `$id` do esquema de referência com o qual este descritor está definindo uma relação. |
| `xdm:destinationVersion` | A versão principal do esquema de referência. |
| `xdm:destinationProperty` | (Opcional) Caminho para um campo de destino no esquema de referência. Isso deve resolver para a ID primária do esquema ou para outro campo com um tipo de dados compatível com `xdm:sourceProperty`. Se omitida, a relação pode não funcionar conforme esperado. |
| `xdm:destinationNamespace` | O namespace da ID primária do esquema de referência. |
| `xdm:destinationToSourceTitle` | O nome de exibição do relacionamento entre o esquema de referência e o esquema de origem. |
| `xdm:sourceToDestinationTitle` | O nome de exibição do relacionamento do esquema de origem com o esquema de referência. |
| `xdm:cardinality` | A relação de ligação entre os esquemas. Este valor deve ser definido como `M:1`, referindo-se a uma relação muitos para um. |

{style="table-layout:auto"}

#### Descritor de identidade de referência

Os descritores de identidade de referência fornecem um contexto de referência para a identidade principal de um campo de esquema, permitindo que ele seja referenciado por campos em outros esquemas. O esquema de referência já deve ter um campo de identidade primário definido para que possa ser referenciado por outros esquemas por meio desse descritor.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de identidade de referência, este valor deve ser definido como `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | O URI `$id` do esquema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do esquema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no esquema de origem que será usado para fazer referência ao esquema de referência. Deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, `/personalEmail/address` em vez de `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | O código de namespace de identidade da propriedade de origem. |

{style="table-layout:auto"}

#### Descritor de campo obsoleto

Você pode [descontinuar um campo em um recurso XDM personalizado](../tutorials/field-deprecation-api.md#custom) adicionando um atributo `meta:status` definido como `deprecated` ao campo em questão. No entanto, se você quiser descontinuar os campos fornecidos pelos recursos XDM padrão em seus esquemas, poderá atribuir um descritor de campo descontinuado ao esquema em questão para obter o mesmo efeito. Usando o [cabeçalho `Accept` correto](../tutorials/field-deprecation-api.md#verify-deprecation), você pode visualizar quais campos padrão foram descontinuados para um esquema ao pesquisá-lo na API.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor. Para um descritor de substituição de campo, este valor deve ser definido como `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | O URI `$id` do esquema ao qual você está aplicando o descritor. |
| `xdm:sourceVersion` | A versão do esquema ao qual você está aplicando o descritor. Deve ser definido como `1`. |
| `xdm:sourceProperty` | O caminho para a propriedade no esquema ao qual você está aplicando o descritor. Se quiser aplicar o descritor a várias propriedades, você pode fornecer uma lista de caminhos na forma de uma matriz (por exemplo, `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
