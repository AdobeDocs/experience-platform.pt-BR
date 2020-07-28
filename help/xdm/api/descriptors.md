---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Descritores
topic: developer guide
translation-type: tm+mt
source-git-commit: b021b6813af18e29f544dc55541f23dd7dd57d47
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 1%

---


# Descritores

Os Schemas definem uma visualização estática de entidades de dados, mas não fornecem detalhes específicos sobre como os dados baseados nesses schemas (conjuntos de dados, por exemplo) podem se relacionar entre si. O Adobe Experience Platform permite que você descreva esses relacionamentos e outros metadados interpretativos sobre um schema usando descritores.

Os descritores de Schema são metadados de nível de locatário, o que significa que são exclusivos à sua organização IMS e que todas as operações do descritor ocorrem no container do locatário.

Cada schema pode ter uma ou mais entidades de descritor de schema aplicadas a ele. Cada entidade do descritor de schema inclui um descritor `@type` e o `sourceSchema` qual ele se aplica. Depois de aplicados, esses descritores serão aplicados a todos os conjuntos de dados criados usando o schema.

Este documento fornece exemplos de chamadas de API para descritores, bem como uma lista completa de descritores disponíveis e os campos necessários para definir cada tipo.

>[!NOTE]
>
>Os descritores exigem cabeçalhos Accept exclusivos que substituem `xed` por `xdm`, mas que, de outra forma, pareçam muito semelhantes aos cabeçalhos Accept usados em outros locais do [!DNL Schema Registry]. Os cabeçalhos de Aceitação corretos foram incluídos nas chamadas de amostra abaixo, mas tenha cuidado extra para garantir que os cabeçalhos corretos estejam sendo usados.

## Descritores de Lista

Uma única solicitação de GET pode ser usada para retornar uma lista de todos os descritores que foram definidos pela sua organização.

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

O formato de resposta depende do cabeçalho Aceitar enviado na solicitação. Observe que o `/descriptors` ponto de extremidade usa cabeçalhos Aceitar que são diferentes de todos os outros pontos de extremidade na [!DNL Schema Registry] API.

Os cabeçalhos Aceitar descritor substituem `xed` por `xdm`e oferta uma `link` opção exclusiva aos descritores.

| Aceitar | Descrição |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Retorna uma matriz de IDs de descritor |
| `application/vnd.adobe.xdm-link+json` | Retorna uma matriz de caminhos da API do descritor |
| `application/vnd.adobe.xdm+json` | Retorna uma matriz de objetos de descritor expandidos |

**Resposta**

A resposta inclui uma matriz para cada tipo de descritor que tenha descritores definidos. Em outras palavras, se não houver descritores de um determinado `@type` tipo definido, o registro não retornará uma matriz vazia para esse tipo de descritor.

Ao usar o cabeçalho `link` Aceitar, cada descritor é mostrado como um item de matriz no formato `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## Procurar um descritor

Se desejar visualização nos detalhes de um descritor específico, você pode procurar (GET) um descritor individual usando seu `@id`.

**Formato da API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` descritor que você deseja pesquisar. |

**Solicitação**

Os descritores não têm controle de versão, portanto, nenhum cabeçalho Accept é necessário na solicitação de pesquisa.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do descritor, incluindo seus `@type` e `sourceSchema`, bem como informações adicionais que variam dependendo do tipo de descritor. O descritor retornado `@id` deve corresponder ao `@id` fornecido na solicitação.

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

## Criar descritor

O [!DNL Schema Registry] permite definir vários tipos diferentes de descritor. Cada tipo de descritor requer que seus próprios campos específicos sejam enviados na solicitação de POST. Uma lista completa de descritores e os campos necessários para defini-los estão disponíveis na seção do apêndice sobre a [definição de descritores](#defining-descriptors).

**Formato da API**

```http
POST /tenant/descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um schema de amostra. Isso instrui [!DNL Experience Platform] o uso do endereço de email como um identificador para ajudar a unir informações sobre o indivíduo.

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

## Descritor de atualização

Você pode atualizar um descritor fazendo uma solicitação de PUT que faça referência ao `@id` descritor que deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` descritor que você deseja atualizar. |

**Solicitação**

Essa solicitação basicamente _regrava_ o descritor, de modo que o corpo da solicitação deve incluir todos os campos necessários para definir um descritor desse tipo. Em outras palavras, a carga da solicitação para atualizar (PUT) um descritor é a mesma carga para criar (POST) um descritor do mesmo tipo.

Neste exemplo, o descritor de identidade está sendo atualizado para fazer referência a um `xdm:sourceProperty` (&quot;celular&quot;) diferente e alterar o `xdm:namespace` para &quot;Telefone&quot;.

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

Detalhes sobre as propriedades `xdm:namespace` e `xdm:property`como acessá-las estão disponíveis na seção do apêndice sobre a [definição de descritores](#defining-descriptors).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e o `@id` do descritor atualizado (que deve corresponder ao `@id` enviado na solicitação).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

A execução de uma solicitação de pesquisa (GET) para visualização do descritor mostrará que os campos foram atualizados para refletir as alterações enviadas na solicitação de PUT.

## Excluir descritor

Ocasionalmente, talvez seja necessário remover um descritor definido do [!DNL Schema Registry]. Isso é feito fazendo uma solicitação DELETE referenciando o nome `@id` do descritor que você deseja remover.

**Formato da API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DESCRIPTOR_ID}` | O `@id` descritor que deseja excluir. |

**Solicitação**

Não é necessário aceitar cabeçalhos ao excluir descritores.

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

Para confirmar que o descritor foi excluído, é possível executar uma solicitação de pesquisa em relação ao descritor `@id`. A resposta retorna o status HTTP 404 (Não encontrado) porque o descritor foi removido do [!DNL Schema Registry].

## Apêndice

A seção a seguir fornece informações adicionais sobre como trabalhar com descritores na [!DNL Schema Registry] API.

### Definição de descritores

As seções a seguir fornecem uma visão geral dos tipos de descritor disponíveis, incluindo os campos obrigatórios para definir um descritor de cada tipo.

#### Descritor de identidade

Um descritor de identidade sinaliza que &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; é um [!DNL Identity] campo como descrito pelo Serviço [de identidade do](../../identity-service/home.md)Adobe Experience Platform.

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
| `xdm:sourceSchema` | O `$id` URI do schema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | O `id` valor ou `code` da namespace de identidade. Uma lista de namespaces pode ser encontrada usando o [!DNL Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | Ou `xdm:id` ou `xdm:code`, dependendo do `xdm:namespace` usado. |
| `xdm:isPrimary` | Um valor booliano opcional. Quando verdadeiro, indica o campo como a identidade primária. Os Schemas podem conter apenas uma identidade primária. |

#### Descritor de nome amigável

Descritores de nome amigáveis permitem que um usuário modifique os valores `title`, `description`e `meta:enum` os campos de schema da biblioteca principal. Especialmente útil ao trabalhar com &quot;eVars&quot; e outros campos &quot;genéricos&quot; que você deseja rotular como contendo informações específicas à sua organização. A interface do usuário pode usá-los para mostrar um nome mais amigável ou apenas para mostrar campos com um nome amigável.

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
| `xdm:sourceSchema` | O `$id` URI do schema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | O caminho para a propriedade específica que será a identidade. O caminho deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, use &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | O novo título que você deseja exibir para este campo, escrito em Caixa alta/baixa. |
| `xdm:description` | Uma descrição opcional pode ser adicionada junto com o título. |
| `meta:enum` | Se o campo indicado por `xdm:sourceProperty` for um campo de string, `meta:enum` determinará a lista dos valores sugeridos para o campo na [!DNL Experience Platform] interface do usuário. É importante observar que `meta:enum` não declara uma lista discriminada ou fornece nenhuma validação de dados para o campo XDM.<br><br>Isso deve ser usado somente para os campos principais XDM definidos pelo Adobe. Se a propriedade de origem for um campo personalizado definido pela sua organização, edite a propriedade do campo `meta:enum` diretamente por meio de uma solicitação [de](./update-resource.md)PATCH. |

#### Descritor de relação

Descritores de relacionamento descrevem uma relação entre dois schemas diferentes, marcados nas propriedades descritas em `sourceProperty` e `destinationProperty`. Consulte o tutorial sobre como [definir uma relação entre dois schemas](../tutorials/relationship-api.md) para obter mais informações.

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
| `xdm:sourceSchema` | O `$id` URI do schema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no schema de origem onde o relacionamento está sendo definido. Deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | O `$id` URI do schema de destino com o qual este descritor está definindo uma relação. |
| `xdm:destinationVersion` | A versão principal do schema de destino. |
| `xdm:destinationProperty` | Caminho opcional para um campo de público alvo dentro do schema de destino. Se essa propriedade for omitida, o campo público alvo será inferido por quaisquer campos que contenham um descritor de identidade de referência correspondente (consulte abaixo). |


#### Descritor de identidade de referência

Os descritores de identidade de referência fornecem um contexto de referência para a identidade primária de um campo de schema, permitindo que ele seja referenciado por campos em outros schemas. Os campos já devem ser rotulados com um descritor de identidade antes que um descritor de referência possa ser aplicado a eles.

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
| `xdm:sourceSchema` | O `$id` URI do schema no qual o descritor está sendo definido. |
| `xdm:sourceVersion` | A versão principal do schema de origem. |
| `xdm:sourceProperty` | Caminho para o campo no schema de origem onde o descritor está sendo definido. Deve começar com &quot;/&quot; e não terminar com um. Não inclua &quot;propriedades&quot; no caminho (por exemplo, &quot;/personalEmail/address&quot; em vez de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | O código de namespace de identidade para a propriedade source. |