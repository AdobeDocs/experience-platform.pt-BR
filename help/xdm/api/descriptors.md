---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema, descritor, descritores, descritores, identidade, identidade, nome amigável, nome amigável, alternatedisplayinfo, referência, referência, relação, relacionamento
solution: Experience Platform
title: Endpoint da API de descritores
description: O endpoint /descriptors na API do Registro de Schema permite gerenciar programaticamente os descritores XDM no aplicativo de experiência.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: f269a7b1584a6e4a0e1820a0c587a647c0c8f7b5
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 4%

---

# Ponto de extremidade de descritores

Os esquemas definem uma visualização estática das entidades de dados, mas não fornecem detalhes específicos sobre como os dados baseados nesses esquemas (conjuntos de dados, por exemplo) podem se relacionar entre si. O Adobe Experience Platform permite descrever esses relacionamentos e outros metadados interpretativos sobre um esquema usando descritores.

Os descritores de esquema são metadados no nível do locatário, o que significa que são exclusivos de sua Organização IMS e todas as operações do descritor ocorrem no contêiner do locatário.

Cada esquema pode ter uma ou mais entidades descritoras de esquema aplicadas a ele. Cada entidade descritora de esquema inclui um descritor `@type` e o `sourceSchema` ao qual se aplica. Depois de aplicados, esses descritores serão aplicados a todos os conjuntos de dados criados usando o schema .

O endpoint `/descriptors` na API [!DNL Schema Registry] permite gerenciar descritores de forma programática no aplicativo de experiência.

## Introdução

O endpoint usado neste manual faz parte da [[!DNL Schema Registry] API do ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

## Recuperar uma lista de descritores {#list}

Você pode listar todos os descritores que foram definidos pela organização, fazendo uma solicitação de GET para `/tenant/descriptors`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

O formato de resposta depende do cabeçalho `Accept` enviado na solicitação. Observe que o ponto de extremidade `/descriptors` usa cabeçalhos `Accept` diferentes de todos os outros pontos de extremidade na API [!DNL Schema Registry].

>[!IMPORTANT]
>
>Os descritores exigem cabeçalhos `Accept` exclusivos que substituem `xed` por `xdm` e também oferecem uma opção `link` exclusiva aos descritores. Os cabeçalhos `Accept` adequados foram incluídos nas chamadas de exemplo abaixo, mas tenha cuidado extra para garantir que os cabeçalhos corretos estejam sendo usados ao trabalhar com descritores.

| `Accept` header | Descrição |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Retorna uma matriz de IDs de descritor |
| `application/vnd.adobe.xdm-link+json` | Retorna uma matriz de caminhos da API do descritor |
| `application/vnd.adobe.xdm+json` | Retorna uma matriz de objetos descritores expandidos |
| `application/vnd.adobe.xdm-v2+json` | Esse cabeçalho `Accept` deve ser usado para utilizar recursos de paginação. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

A resposta inclui uma matriz para cada tipo de descritor que tenha descritores definidos. Em outras palavras, se não houver descritores de um determinado `@type` definido, o registro não retornará uma matriz vazia para esse tipo de descritor.

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

Se quiser visualizar os detalhes de um descritor específico, procure (GET) um descritor individual usando seu `@id`.

**Formato da API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que você deseja pesquisar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera um descritor pelo valor `@id`. Os descritores não têm controle de versão, portanto, nenhum cabeçalho `Accept` é necessário na solicitação de pesquisa.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor, incluindo `@type` e `sourceSchema`, bem como informações adicionais que variam dependendo do tipo de descritor. O `@id` retornado deve corresponder ao descritor `@id` fornecido na solicitação.

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
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Criar um descritor {#create}

Você pode criar um novo descritor fazendo uma solicitação de POST ao ponto de extremidade `/tenant/descriptors`.

>[!IMPORTANT]
>
>O [!DNL Schema Registry] permite definir vários tipos diferentes de descritor. Cada tipo de descritor requer que seus próprios campos específicos sejam enviados no corpo da solicitação. Consulte o [apêndice](#defining-descriptors) para obter uma lista completa de descritores e os campos necessários para defini-los.

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um schema de exemplo. Isso instrui [!DNL Experience Platform] a usar o endereço de email como um identificador para ajudar a unir informações sobre o indivíduo.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Você pode atualizar um descritor ao incluir seu `@id` no caminho de uma solicitação de PUT.

**Formato da API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que você deseja atualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

Essa solicitação basicamente reescreve o descritor, de modo que o corpo da solicitação deve incluir todos os campos necessários para definir um descritor desse tipo. Em outras palavras, a carga da solicitação para atualizar (PUT) um descritor é igual à carga para [criar (POST) um descritor](#create) do mesmo tipo.

>[!IMPORTANT]
>
>Assim como na criação de descritores usando solicitações de POST, cada tipo de descritor requer que seus próprios campos específicos sejam enviados em cargas de solicitação de PUT. Consulte o [apêndice](#defining-descriptors) para obter uma lista completa de descritores e os campos necessários para defini-los.

O exemplo a seguir atualiza um descritor de identidade para fazer referência a um `xdm:sourceProperty` diferente (`mobile phone`) e altera o `xdm:namespace` para `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Executar uma solicitação de [pesquisa (GET)](#lookup) para visualizar o descritor mostrará que os campos foram atualizados para refletir as alterações enviadas na solicitação do PUT.

## Excluir um descritor {#delete}

Ocasionalmente, talvez seja necessário remover um descritor definido no [!DNL Schema Registry]. Isso é feito fazendo uma solicitação DELETE referenciando o `@id` do descritor que você deseja remover.

**Formato da API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` do descritor que você deseja excluir. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo) e um corpo em branco.

Para confirmar que o descritor foi excluído, é possível executar um [solicitação de pesquisa](#lookup) no descritor `@id`. A resposta retorna o status HTTP 404 (Not Found) porque o descritor foi removido do [!DNL Schema Registry].

## Apêndice

A seção a seguir fornece informações adicionais sobre como trabalhar com descritores na API [!DNL Schema Registry].

### Definição de descritores {#defining-descriptors}

As seções a seguir fornecem uma visão geral dos tipos de descritor disponíveis, incluindo os campos obrigatórios para definir um descritor de cada tipo.

#### Descritor de identidade

Um descritor de identidade sinaliza que &quot;[!UICONTROL sourceProperty]&quot; do &quot;[!UICONTROL sourceSchema]&quot; é um campo [!DNL Identity] conforme descrito por [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | O tipo de descritor que está sendo definido. |
| `xdm:sourceSchema` | O URI `$id` do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;) |
| `xdm:namespace` | O valor `id` ou `code` do namespace de identidade. Uma lista de namespaces pode ser encontrada usando o [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | `xdm:id` ou `xdm:code`, dependendo do `xdm:namespace` usado. |
| `xdm:isPrimary` | Um valor booleano opcional. Quando verdadeiro, indica o campo como a identidade primária. Os esquemas podem conter apenas uma identidade primária. |

{style=&quot;table-layout:auto&quot;}

#### Descritor de nome amigável

Descritores de nome amigáveis permitem que um usuário modifique os valores `title`, `description` e `meta:enum` dos campos de esquema da biblioteca principal. Especialmente útil ao trabalhar com &quot;eVars&quot; e outros campos &quot;genéricos&quot; que você deseja rotular como contendo informações específicas para sua organização. A interface do usuário pode usá-los para mostrar um nome mais amigável ou apenas para mostrar campos que têm um nome amigável.

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
| `@type` | O tipo de descritor que está sendo definido. |
| `xdm:sourceSchema` | O URI `$id` do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;) |
| `xdm:title` | O novo título que deseja exibir para esse campo, escrito em Caso de título. |
| `xdm:description` | Uma descrição opcional pode ser adicionada junto com o título. |
| `meta:enum` | Se o campo indicado por `xdm:sourceProperty` for um campo de string, `meta:enum` determinará a lista de valores sugeridos para o campo na interface [!DNL Experience Platform]. É importante observar que `meta:enum` não declara uma enumeração ou fornece qualquer validação de dados para o campo XDM.<br><br>Isso só deve ser usado para campos XDM principais definidos pelo Adobe. Se a propriedade de origem for um campo personalizado definido pela organização, em vez disso, edite a propriedade `meta:enum` do campo diretamente por meio de uma solicitação PATCH para o recurso pai do campo. |

{style=&quot;table-layout:auto&quot;}

#### Descritor de relacionamento

Descritores de relacionamento descrevem uma relação entre dois esquemas diferentes, com base nas propriedades descritas em `sourceProperty` e `destinationProperty`. Consulte o tutorial em [definindo uma relação entre dois schemas](../tutorials/relationship-api.md) para obter mais informações.

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
| `@type` | O tipo de descritor que está sendo definido. |
| `xdm:sourceSchema` | O URI `$id` do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no schema de origem onde o relacionamento está sendo definido. Deve começar com um &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | O URI `$id` do esquema de destino com o qual este descritor está definindo uma relação. |
| `xdm:destinationVersion` | A versão principal do schema de destino. |
| `xdm:destinationProperty` | Caminho opcional para um campo de destino dentro do esquema de destino. Se essa propriedade for omitida, o campo de destino será inferido por qualquer campo que contenha um descritor de identidade de referência correspondente (veja abaixo). |

{style=&quot;table-layout:auto&quot;}


#### Descritor de identidade de referência

Os descritores de identidade de referência fornecem um contexto de referência para a identidade primária de um campo de esquema, permitindo que ele seja referenciado por campos em outros schemas. Os campos já devem ser rotulados com um descritor de identidade antes que um descritor de referência possa ser aplicado a eles.

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
| `@type` | O tipo de descritor que está sendo definido. |
| `xdm:sourceSchema` | O URI `$id` do esquema em que o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no schema de origem onde o descritor está sendo definido. Deve começar com um &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/pessoalEmail/address&quot; em vez de &quot;/properties/pessoalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | O código do namespace de identidade para a propriedade de origem. |
