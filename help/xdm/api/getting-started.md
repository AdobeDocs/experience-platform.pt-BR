---
keywords: Experience Platform;início;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquema;Registro de esquema;
solution: Experience Platform
title: Introdução à API do Registro de esquema
description: Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Registro de esquema.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: eb1cf204e95591082b27dc97cd3c709a23b20b08
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 5%

---

# Introdução à API [!DNL Schema Registry]

A API [!DNL Schema Registry] permite criar e gerenciar vários recursos do Experience Data Model (XDM). Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Schema Registry].

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O XDM usa a formatação do esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Portanto, é altamente recomendável que você consulte a [documentação oficial do Esquema JSON](https://json-schema.org/) para obter uma melhor compreensão dessa tecnologia subjacente.

## Leitura de chamadas de API de amostra

A documentação da API [!DNL Schema Registry] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Schema Registry], estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação da sandbox](../../sandboxes/home.md).

Todas as solicitações de pesquisa (GET) para [!DNL Schema Registry] exigem um cabeçalho `Accept` adicional, cujo valor determina o formato das informações retornadas pela API. Consulte a seção [Aceitar cabeçalho](#accept) abaixo para obter mais detalhes.

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Conhecer seu TENANT_ID {#know-your-tenant_id}

Nos guias de API você verá referências a um `TENANT_ID`. Essa ID é usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na organização. Caso não saiba a ID, é possível acessá-la executando a seguinte solicitação do GET:

**Formato da API**

```http
GET /stats
```

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna informações sobre o uso do [!DNL Schema Registry] por sua organização. Isso inclui um atributo `tenantId`, cujo valor é seu `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Entender o `CONTAINER_ID` {#container}

As chamadas à API [!DNL Schema Registry] exigem o uso de um `CONTAINER_ID`. Há dois contêineres para os quais as chamadas de API podem ser feitas: o contêiner `global` e o contêiner `tenant`.

### Contêiner global

O contêiner `global` contém todas as classes, grupos de campos de esquema, tipos de dados e esquemas fornecidos pelo Adobe padrão e pelo parceiro [!DNL Experience Platform]. Você só pode executar solicitações de lista e pesquisa (GET) no contêiner `global`.

Um exemplo de uma chamada que usa o contêiner `global` seria semelhante ao seguinte:

```http
GET /global/classes
```

### Contêiner do inquilino

Para não ser confundido com seu `TENANT_ID` exclusivo, o contêiner `tenant` contém todas as classes, grupos de campos, tipos de dados, esquemas e descritores definidos por uma organização. Elas são exclusivas de cada organização, o que significa que não são visíveis nem gerenciáveis por outras organizações. Você pode executar todas as operações CRUD (GET, POST, PUT, PATCH, DELETE) em relação aos recursos criados no contêiner `tenant`.

Um exemplo de uma chamada que usa o contêiner `tenant` seria semelhante ao seguinte:

```http
POST /tenant/fieldgroups
```

Ao criar uma classe, grupo de campos, esquema ou tipo de dados no contêiner `tenant`, ele é salvo em [!DNL Schema Registry] e é atribuído um URI `$id` que inclui seu `TENANT_ID`. Este `$id` é usado em toda a API para referenciar recursos específicos. Exemplos de valores `$id` são fornecidos na próxima seção.

## Identificação do recurso {#resource-identification}

Os recursos XDM são identificados com um atributo `$id` no formato de um URI, como os seguintes exemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para tornar o URI mais amigável, os esquemas também têm uma codificação de notação de pontos do URI em uma propriedade chamada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

As chamadas para a API [!DNL Schema Registry] oferecerão suporte ao URI `$id` codificado em URL ou ao `meta:altId` (formato de notação de ponto). A prática recomendada é usar o URI `$id` codificado em URL ao fazer uma chamada REST para a API, da seguinte maneira:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceitar cabeçalho {#accept}

Ao executar operações de lista e pesquisa (GET) na API [!DNL Schema Registry], é necessário um cabeçalho `Accept` para determinar o formato dos dados retornados pela API. Quando você procura recursos específicos, um número de versão também deve ser incluído no cabeçalho `Accept`.

A tabela a seguir lista valores de cabeçalho `Accept` compatíveis, incluindo aqueles com números de versão, juntamente com descrições do que a API retornará quando forem usados.

| Aceitar | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retorna somente uma lista de IDs. Isso é usado com mais frequência para listar recursos. |
| `application/vnd.adobe.xed+json` | Retorna uma lista de esquemas JSON completos com `$ref` e `allOf` originais incluídos. Isso é usado para retornar uma lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM bruto com `$ref` e `allOf`. Tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos e `allOf` resolvidos. Tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM bruto com `$ref` e `allOf`. Nenhum título ou descrição. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` atributos e `allOf` resolvidos. Nenhum título ou descrição. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` atributos e `allOf` resolvidos. Os descritores estão incluídos. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` resolvidos, têm títulos e descrições. Campos obsoletos são indicados com um atributo `meta:status` de `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>No momento, a plataforma oferece suporte a apenas uma versão principal para cada esquema (`1`). Portanto, o valor de `version` deve ser sempre `1` ao executar solicitações de pesquisa para retornar a versão secundária mais recente do esquema. Consulte a subseção abaixo para obter mais informações sobre o controle de versão do schema.

### Controle de versão do esquema {#versioning}

As versões de esquema são referenciadas por `Accept` cabeçalhos na API do Registro de Esquema e em `schemaRef.contentType` propriedades nas cargas da API do serviço de plataforma downstream.

Atualmente, a Platform só oferece suporte a uma única versão principal (`1`) para cada esquema. De acordo com as [regras de evolução do esquema](../schema/composition.md#evolution), cada atualização de um esquema deve ser não destrutiva, o que significa que novas versões secundárias de um esquema (`1.2`, `1.3` etc.) são sempre compatíveis com versões anteriores secundárias. Portanto, ao especificar `version=1`, o Registro de Esquemas sempre retorna a **última** versão principal `1` de um esquema, o que significa que as versões secundárias anteriores não são retornadas.

>[!NOTE]
>
>O requisito não destrutivo para a evolução do esquema só é aplicado depois que o esquema é referenciado por um conjunto de dados e um dos seguintes casos é verdadeiro:
>
>* Os dados foram assimilados no conjunto de dados.
>* O conjunto de dados foi ativado para uso no Perfil do cliente em tempo real (mesmo se nenhum dado tiver sido assimilado).
>
>Se o esquema não tiver sido associado a um conjunto de dados que atenda a um dos critérios acima, qualquer alteração poderá ser feita nele. No entanto, em todos os casos, o componente `version` ainda permanece em `1`.

## Restrições de campo XDM e práticas recomendadas

Os campos de um esquema são listados em seu objeto `properties`. Cada campo é um objeto que contém atributos para descrever e restringir os dados que o campo pode conter. Consulte o manual sobre [definição de campos personalizados na API](../tutorials/custom-fields-api.md) para obter amostras de código e restrições opcionais para os tipos de dados mais usados.

O campo de amostra a seguir ilustra um campo XDM formatado corretamente, com mais detalhes sobre restrições de nomenclatura e práticas recomendadas fornecidas abaixo. Essas práticas também podem ser aplicadas ao definir outros recursos que contenham atributos semelhantes.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* O nome de um objeto de campo pode conter caracteres alfanuméricos, traços ou sublinhados, mas **não** pode começar com um sublinhado.
   * **Correto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorreto:** `_fieldName`
* Os nomes de campos não diferenciam maiúsculas de minúsculas e devem ter nomes diferentes no mesmo nível no esquema.
* camelCase é preferido para o nome do objeto de campo. Exemplo: `fieldName`
* O campo deve incluir um `title`, escrito em letra maiúscula ou minúscula. Exemplo: `Field Name`
* O campo requer `type`.
   * A definição de determinados tipos pode exigir um `format` opcional.
   * Quando uma formatação específica de dados é necessária, `examples` pode ser adicionado como uma matriz.
   * O tipo de campo também pode ser definido usando qualquer tipo de dados no registro. Consulte a seção sobre [criação de um tipo de dados](./data-types.md#create) no manual de ponto de extremidade de tipos de dados para obter mais informações.
* O `description` explica o campo e as informações pertinentes aos dados do campo. Ele deve ser escrito em frases completas com linguagem clara para que qualquer pessoa que acesse o schema possa entender a intenção do campo.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Schema Registry], selecione um dos manuais de ponto de extremidade disponíveis.
