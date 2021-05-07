---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema;
solution: Experience Platform
title: Introdução à API do Registro de Schema
description: Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Registro de Schema.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# Introdução à API [!DNL Schema Registry]

A API [!DNL Schema Registry] permite criar e gerenciar vários recursos do Experience Data Model (XDM). Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Schema Registry].

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../schema/composition.md) do schema: Saiba mais sobre os componentes básicos dos esquemas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O XDM usa a formatação Esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Portanto, é altamente recomendável revisar a [documentação oficial do Esquema JSON](https://json-schema.org/) para obter uma melhor compreensão dessa tecnologia subjacente.

## Lendo exemplos de chamadas de API

A documentação da API [!DNL Schema Registry] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo aqueles pertencentes a [!DNL Schema Registry], são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação da sandbox](../../sandboxes/home.md).

Todas as solicitações de pesquisa (GET) para o [!DNL Schema Registry] exigem um cabeçalho `Accept` adicional, cujo valor determina o formato das informações retornadas pela API. Consulte a seção [Accept header](#accept) abaixo para obter mais detalhes.

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Conhece seu TENANT_ID {#know-your-tenant_id}

Em todos os guias da API, você verá referências a um `TENANT_ID`. Essa ID é usada para garantir que os recursos criados sejam namespacados corretamente e estejam contidos na Organização IMS. Caso não saiba sua ID, é possível acessá-la executando a seguinte solicitação do GET:

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna informações sobre o uso do [!DNL Schema Registry] por parte de sua organização. Isso inclui um atributo `tenantId`, cujo valor é seu `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "fieldgroups": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "fieldgroups",
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
      "meta:resourceType": "fieldgroups",
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

## Entenda o `CONTAINER_ID` {#container}

As chamadas à API [!DNL Schema Registry] exigem o uso de um `CONTAINER_ID`. Há dois contêineres para fazer chamadas de API: o contêiner `global` e o contêiner `tenant`.

### Contêiner global

O contêiner `global` contém todos os Adobe padrão e [!DNL Experience Platform] classes fornecidas pelo parceiro, grupos de campos de esquema, tipos de dados e esquemas. Você só pode executar solicitações de lista e pesquisa (GET) em relação ao contêiner `global`.

Um exemplo de chamada que usa o contêiner `global` seria semelhante ao seguinte:

```http
GET /global/classes
```

### Contêiner de locatário

Para não ser confundido com seu `TENANT_ID` exclusivo, o contêiner `tenant` contém todas as classes, grupos de campos, tipos de dados, esquemas e descritores definidos por uma Organização IMS. Elas são exclusivas de cada organização, o que significa que não são visíveis ou gerenciáveis por outras Orgs do IMS. Você pode executar todas as operações CRUD (GET, POST, PUT, PATCH, DELETE) em relação aos recursos que você cria no contêiner `tenant`.

Um exemplo de chamada que usa o contêiner `tenant` seria semelhante ao seguinte:

```http
POST /tenant/fieldgroups
```

Ao criar uma classe, grupo de campos, esquema ou tipo de dados no contêiner `tenant`, ele é salvo no [!DNL Schema Registry] e recebe um URI `$id` que inclui seu `TENANT_ID`. Esse `$id` é usado em toda a API para fazer referência a recursos específicos. Exemplos de valores `$id` são fornecidos na próxima seção.

## Identificação do recurso {#resource-identification}

Os recursos XDM são identificados com um atributo `$id` no formato de um URI, como os seguintes exemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para tornar o URI mais compatível com REST, os schemas também têm uma codificação de notação de pontos do URI em uma propriedade chamada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

As chamadas para a API [!DNL Schema Registry] oferecerão suporte ao URI `$id` codificado por URL ou `meta:altId` (formato de notação de pontos). A prática recomendada é usar o URI `$id` codificado por URL ao fazer uma chamada REST para a API, da seguinte maneira:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceitar cabeçalho {#accept}

Ao executar operações de lista e pesquisa (GET) na API [!DNL Schema Registry], um cabeçalho `Accept` é necessário para determinar o formato dos dados retornados pela API. Ao pesquisar recursos específicos, um número de versão também deve ser incluído no cabeçalho `Accept`.

A tabela a seguir lista valores de cabeçalho compatíveis `Accept`, incluindo aqueles com números de versão, juntamente com descrições do que a API retornará quando forem usadas.

| Accept | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retorna somente uma lista de IDs. Isso é usado mais frequentemente para listar recursos. |
| `application/vnd.adobe.xed+json` | Retorna uma lista de esquema JSON completo com `$ref` original e `allOf` incluído. Isso é usado para retornar uma lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM bruto com `$ref` e `allOf`. Possui títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` e  `allOf` resolvidos. Possui títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM bruto com `$ref` e `allOf`. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` e  `allOf` resolvidos. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` e  `allOf` resolvidos. Os descritores são incluídos. |

>[!NOTE]
>
>Atualmente, a plataforma suporta apenas uma versão principal para cada esquema (`1`). Portanto, o valor de `version` deve sempre ser `1` ao executar solicitações de pesquisa para retornar a versão secundária mais recente do esquema. Consulte a subseção abaixo para obter mais informações sobre o controle de versão do schema.

### Controle de versão do esquema {#versioning}

As versões do esquema são referenciadas por cabeçalhos `Accept` na API do Registro de Schema e nas propriedades `schemaRef.contentType` nas cargas downstream da API do serviço da plataforma.

Atualmente, a Platform suporta apenas uma única versão principal (`1`) para cada esquema. De acordo com as [regras de evolução do schema](../schema/composition.md#evolution), cada atualização em um schema deve ser não destrutiva, o que significa que novas versões secundárias de um schema (`1.2`, `1.3`, etc.) são sempre compatíveis com versões secundárias anteriores. Portanto, ao especificar `version=1`, o Registro de Schema sempre retorna a **versão principal** mais recente `1` de um schema , o que significa que as versões secundárias anteriores não são retornadas.

>[!NOTE]
>
>O requisito não destrutivo da evolução do schema é empregado somente após o schema ter sido referenciado por um conjunto de dados e um dos seguintes casos ser verdadeiro:
>
>* Os dados foram assimilados no conjunto de dados.
>* O conjunto de dados foi ativado para uso no Perfil do cliente em tempo real (mesmo se nenhum dado tiver sido assimilado).

>
>
Se o esquema não tiver sido associado a um conjunto de dados que atende a um dos critérios acima, qualquer alteração poderá ser feita nele. No entanto, em todos os casos, o componente `version` ainda permanece em `1`.

## Restrições de campo e práticas recomendadas do XDM

Os campos de um schema são listados em seu objeto `properties`. Cada campo é um objeto contendo atributos para descrever e restringir os dados que o campo pode conter.

Mais informações sobre a definição de tipos de campo na API podem ser encontradas no [field restrguide](../schema/field-constraints.md) deste guia, incluindo amostras de código e restrições opcionais para os tipos de dados mais usados.

O campo de amostra a seguir ilustra um campo XDM formatado corretamente, com mais detalhes sobre as restrições de nomenclatura e práticas recomendadas fornecidas abaixo. Essas práticas também podem ser aplicadas ao definir outros recursos que contenham atributos semelhantes.

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

* O nome de um objeto de campo pode conter caracteres alfanuméricos, traço ou sublinhados, mas **pode não** começar com um sublinhado.
   * **Correto:** `fieldName`,  `field_name2`,  `Field-Name`,  `field-name_3`
   * **Incorreto:** `_fieldName`
* camelCase é preferível para o nome do objeto de campo. Exemplo: `fieldName`
* O campo deve incluir um `title`, gravado no Caso de título. Exemplo: `Field Name`
* O campo requer um `type`.
   * A definição de certos tipos pode exigir um `format` opcional.
   * Quando uma formatação específica de dados é necessária, `examples` pode ser adicionado como uma matriz.
   * O tipo de campo também pode ser definido usando qualquer tipo de dados no registro. Consulte a seção sobre [criar um tipo de dados](./data-types.md#create) no guia de ponto de extremidade de tipos de dados para obter mais informações.
* O `description` explica o campo e as informações pertinentes sobre os dados do campo. Ele deve ser escrito em frases completas com linguagem clara para que qualquer pessoa que acessar o esquema possa entender a intenção do campo.

Consulte o documento em [restrições de campo](../schema/field-constraints.md) para obter mais informações sobre como definir diferentes tipos de campo na API.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Schema Registry], selecione um dos guias de ponto de extremidade disponíveis.
