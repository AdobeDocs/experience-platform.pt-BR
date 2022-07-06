---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema, descritor, descritores, descritores, identidade, identidade, nome amigável, nome amigável, alternatedisplayinfo, referência, referência, relação, relacionamento
solution: Experience Platform
title: Endpoint da API de descritores
description: O endpoint /descriptors na API do Registro de Schema permite gerenciar programaticamente os descritores XDM no aplicativo de experiência.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 65a6eca9450b3a3e19805917fb777881c08817a0
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 4%

---

# Ponto de extremidade de descritores

Os esquemas definem uma visualização estática das entidades de dados, mas não fornecem detalhes específicos sobre como os dados baseados nesses esquemas (conjuntos de dados, por exemplo) podem se relacionar entre si. O Adobe Experience Platform permite descrever esses relacionamentos e outros metadados interpretativos sobre um esquema usando descritores.

Os descritores de esquema são metadados no nível do locatário, o que significa que são exclusivos de sua Organização IMS e todas as operações do descritor ocorrem no contêiner do locatário.

Cada esquema pode ter uma ou mais entidades descritoras de esquema aplicadas a ele. Cada entidade do descritor de esquema inclui um descritor `@type` e `sourceSchema` a que se aplica. Depois de aplicados, esses descritores serão aplicados a todos os conjuntos de dados criados usando o schema .

O `/descriptors` endpoint no [!DNL Schema Registry] A API permite gerenciar descritores de forma programática no aplicativo de experiência.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de descritores {#list}

Você pode listar todos os descritores que foram definidos pela organização fazendo uma solicitação de GET para `/tenant/descriptors`.

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

O formato de resposta depende do `Accept` cabeçalho enviado na solicitação. Observe que a variável `/descriptors` usos do ponto de extremidade `Accept` cabeçalhos que são diferentes de todos os outros endpoints no [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>Descritores exigem `Accept` cabeçalhos que substituem `xed` com `xdm`e também oferecer uma `link` que é exclusiva aos descritores. A `Accept` os cabeçalhos foram incluídos nas chamadas de exemplos abaixo, mas tenha cuidado extra para garantir que os cabeçalhos corretos estejam sendo usados ao trabalhar com descritores.

| `Accept` header | Descrição |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Retorna uma matriz de IDs de descritor |
| `application/vnd.adobe.xdm-link+json` | Retorna uma matriz de caminhos da API do descritor |
| `application/vnd.adobe.xdm+json` | Retorna uma matriz de objetos descritores expandidos |
| `application/vnd.adobe.xdm-v2+json` | Essa `Accept` deve ser usado para utilizar recursos de paginação. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

A resposta inclui uma matriz para cada tipo de descritor que tenha descritores definidos. Em outras palavras, se não houver descritores de um determinado `@type` definido, o registro não retornará uma matriz vazia para esse tipo de descritor.

Ao usar a variável `link` `Accept` cada descritor é exibido como um item de matriz no formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Se quiser visualizar os detalhes de um descritor específico, procure (GET) um descritor individual usando seu `@id`.

**Formato da API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera um descritor por seu `@id` valor. Os descritores não têm controle de versão, portanto, não há `Accept` é necessário ter o cabeçalho na solicitação de pesquisa.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor, incluindo seu `@type` e `sourceSchema`, bem como informações adicionais que variam de acordo com o tipo de descritor. O retorno `@id` deve corresponder ao descritor `@id` fornecido no pedido.

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

Você pode criar um novo descritor fazendo uma solicitação de POST para a variável `/tenant/descriptors` endpoint .

>[!IMPORTANT]
>
>O [!DNL Schema Registry] permite definir vários tipos diferentes de descritor. Cada tipo de descritor requer que seus próprios campos específicos sejam enviados no corpo da solicitação. Consulte a [apêndice](#defining-descriptors) para obter uma lista completa de descritores e os campos necessários para defini-los.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um schema de exemplo. Isso diz [!DNL Experience Platform] para usar o endereço de email como um identificador para ajudar a unir informações sobre o indivíduo.

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

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes do descritor recém-criado, incluindo seu `@id`. O `@id` é um campo somente leitura atribuído pelo [!DNL Schema Registry] e usado para referenciar o descritor na API.

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

Você pode atualizar um descritor incluindo seu `@id` no caminho de uma solicitação de PUT.

**Formato da API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

Essa solicitação basicamente reescreve o descritor, de modo que o corpo da solicitação deve incluir todos os campos necessários para definir um descritor desse tipo. Em outras palavras, a carga da solicitação para atualizar (PUT) um descritor é igual à carga para [criar (POST) um descritor](#create) do mesmo tipo.

>[!IMPORTANT]
>
>Assim como na criação de descritores usando solicitações de POST, cada tipo de descritor requer que seus próprios campos específicos sejam enviados em cargas de solicitação de PUT. Consulte a [apêndice](#defining-descriptors) para obter uma lista completa de descritores e os campos necessários para defini-los.

O exemplo a seguir atualiza um descritor de identidade para fazer referência a um `xdm:sourceProperty` (`mobile phone`) e alterar o `xdm:namespace` para `Phone`.

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

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e a variável `@id` do descritor atualizado (que deve corresponder à variável `@id` enviado na solicitação).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Executar um [solicitação de pesquisa (GET)](#lookup) para visualizar o descritor, mostrará que os campos foram atualizados para refletir as alterações enviadas na solicitação do PUT.

## Excluir um descritor {#delete}

Ocasionalmente, talvez seja necessário remover um descritor definido no [!DNL Schema Registry]. Isso é feito fazendo uma solicitação de DELETE que faça referência à variável `@id` do descritor que deseja remover.

**Formato da API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que deseja excluir. |

{style=&quot;table-layout:auto&quot;}

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

Para confirmar que o descritor foi excluído, é possível executar um [solicitação de pesquisa](#lookup) contra o descritor `@id`. A resposta retorna o status HTTP 404 (Not Found) porque o descritor foi removido do [!DNL Schema Registry].

## Apêndice

A seção a seguir fornece informações adicionais sobre como trabalhar com descritores na variável [!DNL Schema Registry] API.

### Definição de descritores {#defining-descriptors}

As seções a seguir fornecem uma visão geral dos tipos de descritor disponíveis, incluindo os campos obrigatórios para definir um descritor de cada tipo.

#### Descritor de identidade

Um descritor de identidade sinaliza que &quot;[!UICONTROL sourceProperty]&quot; do &quot;[!UICONTROL sourceSchema]&quot; é um [!DNL Identity] como descrito por [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md).

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
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de identidade, esse valor deve ser definido como `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | O `$id` URI do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;) |
| `xdm:namespace` | O `id` ou `code` valor do namespace de identidade. Uma lista de namespaces pode ser encontrada usando o [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | Ou `xdm:id` ou `xdm:code`, dependendo do `xdm:namespace` usado. |
| `xdm:isPrimary` | Um valor booleano opcional. Quando verdadeiro, indica o campo como a identidade primária. Os esquemas podem conter apenas uma identidade primária. |

{style=&quot;table-layout:auto&quot;}

#### Descritor de nome amigável {#friendly-name}

Descritores de nome amigáveis permitem que um usuário modifique o `title`, `description`e `meta:enum` valores dos campos de esquema da biblioteca principal. Especialmente útil ao trabalhar com &quot;eVars&quot; e outros campos &quot;genéricos&quot; que você deseja rotular como contendo informações específicas para sua organização. A interface do usuário pode usá-los para mostrar um nome mais amigável ou apenas para mostrar campos que têm um nome amigável.

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
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de nome amigável, esse valor deve ser definido como `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | O `$id` URI do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;) |
| `xdm:title` | O novo título que deseja exibir para esse campo, escrito em Caso de título. |
| `xdm:description` | Uma descrição opcional pode ser adicionada junto com o título. |
| `meta:enum` | Se o campo indicado por `xdm:sourceProperty` é um campo de string, `meta:enum` determina a lista de valores sugeridos para o campo no [!DNL Experience Platform] IU. É importante notar que `meta:enum` não declara uma enumeração ou fornece nenhuma validação de dados para o campo XDM.<br><br>Isso só deve ser usado para campos XDM principais definidos pelo Adobe. Se a propriedade de origem for um campo personalizado definido pela organização, em vez disso, edite o campo `meta:enum` diretamente por meio de uma solicitação PATCH para o recurso pai do campo. |

{style=&quot;table-layout:auto&quot;}

#### Descritor de relacionamento

Descritores de relacionamento descrevem uma relação entre dois esquemas diferentes, com base nas propriedades descritas em `sourceProperty` e `destinationProperty`. Veja o tutorial em [definição de uma relação entre dois schemas](../tutorials/relationship-api.md) para obter mais informações.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de relacionamento, esse valor deve ser definido como `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | O `$id` URI do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no schema de origem onde o relacionamento está sendo definido. Deve começar com um &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | O `$id` URI do esquema de destino com o qual este descritor está definindo uma relação. |
| `xdm:destinationVersion` | A versão principal do schema de destino. |
| `xdm:destinationProperty` | Caminho opcional para um campo de destino dentro do esquema de destino. Se essa propriedade for omitida, o campo de destino será inferido por qualquer campo que contenha um descritor de identidade de referência correspondente (veja abaixo). |

{style=&quot;table-layout:auto&quot;}

#### Descritor de identidade de referência

Os descritores de identidade de referência fornecem um contexto de referência para a identidade primária de um campo de esquema, permitindo que ele seja referenciado por campos em outros schemas. O schema de destino já deve ter um campo de identidade primário definido antes que possa ser referenciado por outros schemas por meio deste descritor.

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
| `@type` | O tipo de descritor que está sendo definido. Para um descritor de identidade de referência, esse valor deve ser definido como `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | O `$id` URI do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no schema de origem que será usado para fazer referência ao schema de destino. Deve começar com um &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, `/personalEmail/address` em vez de `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | O código do namespace de identidade para a propriedade de origem. |

{style=&quot;table-layout:auto&quot;}

#### Descritor de campo obsoleto

Você pode [descontinuar um campo em um recurso XDM personalizado](../tutorials/field-deprecation.md#custom) adicionando uma `meta:status` conjunto de atributos para `deprecated` para o campo em questão. No entanto, se você quiser descontinuar os campos fornecidos pelos recursos padrão do XDM em seus esquemas, poderá atribuir um descritor de campo obsoleto ao schema em questão para obter o mesmo efeito. Usar o [correto `Accept` header](../tutorials/field-deprecation.md#verify-deprecation), é possível exibir quais campos padrão estão obsoletos para um esquema ao pesquisá-lo na API.

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
| `@type` | O tipo de descritor. Para um descritor de descontinuação de campo, esse valor deve ser definido como `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | O URI `$id` do esquema ao qual você está aplicando o descritor. |
| `xdm:sourceVersion` | A versão do esquema à qual você está aplicando o descritor. Deve ser definido como `1`. |
| `xdm:sourceProperty` | O caminho para a propriedade no esquema ao qual você está aplicando o descritor. Se quiser aplicar o descritor a várias propriedades, é possível fornecer uma lista de caminhos na forma de uma matriz (por exemplo, `["/firstName", "/lastName"]`). |

{style=&quot;table-layout:auto&quot;}
