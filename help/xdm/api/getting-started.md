---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Introdução à API do Registro de Schemas
description: Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Registro do Schema.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Introdução à API [!DNL Schema Registry]

A API [!DNL Schema Registry] permite que você crie e gerencie vários recursos do Modelo de Dados de Experiência (XDM). Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API [!DNL Schema Registry].

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

O XDM usa a formatação do Schema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Portanto, é altamente recomendável que você reveja a [documentação oficial do Schema JSON](https://json-schema.org/) para obter uma melhor compreensão dessa tecnologia subjacente.

## Lendo chamadas de exemplo da API

A documentação da API [!DNL Schema Registry] fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](../../tutorials/authentication.md). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes a [!DNL Schema Registry], são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações de pesquisa (GET) para [!DNL Schema Registry] exigem um cabeçalho `Accept` adicional, cujo valor determina o formato das informações retornadas pela API. Consulte a seção [Aceitar cabeçalho](#accept) abaixo para obter mais detalhes.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Conheça sua TENANT_ID {#know-your-tenant_id}

Em todos os guias da API, você verá referências a `TENANT_ID`. Essa ID é usada para garantir que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. Se você não souber sua ID, poderá acessá-la executando a seguinte solicitação de GET:

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
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

## Entenda o `CONTAINER_ID` {#container}

As chamadas para a API [!DNL Schema Registry] exigem o uso de um `CONTAINER_ID`. Há dois container contra os quais as chamadas de API podem ser feitas: o container `global` e o container `tenant`.

### Container global

O container `global` contém todos os Adobe padrão e [!DNL Experience Platform] os parceiros forneciam classes, mixins, tipos de dados e schemas. Você só pode executar solicitações de lista e pesquisa (GET) contra o container `global`.

Um exemplo de uma chamada que usa o container `global` seria semelhante ao seguinte:

```http
GET /global/classes
```

### Container de inquilino

Para não ser confundido com seu `TENANT_ID` exclusivo, o container `tenant` contém todas as classes, misturas, tipos de dados, schemas e descritores definidos por uma Organização IMS. Elas são exclusivas de cada organização, o que significa que não são visíveis ou gerenciáveis por outras Organizações IMS. Você pode executar todas as operações CRUD (GET, POST, PUT, PATCH, DELETE) em relação aos recursos criados no container `tenant`.

Um exemplo de uma chamada que usa o container `tenant` seria semelhante ao seguinte:

```http
POST /tenant/mixins
```

Quando você cria uma classe, combinação, schema ou tipo de dados no container `tenant`, ela é salva no [!DNL Schema Registry] e recebe um URI `$id` que inclui seu `TENANT_ID`. Esse `$id` é usado em toda a API para fazer referência a recursos específicos. Exemplos de valores `$id` são fornecidos na próxima seção.

## Identificação do recurso {#resource-identification}

Os recursos XDM são identificados com um atributo `$id` na forma de um URI, como os seguintes exemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para tornar o URI mais compatível com REST, os schemas também têm uma codificação de notação de pontos do URI em uma propriedade chamada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

As chamadas para a API [!DNL Schema Registry] oferecerão suporte ao URI `$id` codificado pelo URL ou ao `meta:altId` (formato de notação de pontos). A prática recomendada é usar o URI `$id` codificado por URL ao fazer uma chamada REST para a API, como segue:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceitar cabeçalho {#accept}

Ao executar operações de lista e pesquisa (GET) na API [!DNL Schema Registry], um cabeçalho `Accept` é necessário para determinar o formato dos dados retornados pela API. Ao procurar recursos específicos, um número de versão também deve ser incluído no cabeçalho `Accept`.

A tabela a seguir lista valores de cabeçalho compatíveis `Accept`, incluindo aqueles com números de versão, juntamente com descrições do que a API retornará quando for usada.

| Aceitar | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retorna apenas uma lista de IDs. Isso é usado com mais frequência para a listagem de recursos. |
| `application/vnd.adobe.xed+json` | Retorna uma lista de schema JSON completo com `$ref` e `allOf` originais incluídos. Isto é usado para devolver uma lista de recursos completos. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | XDM bruto com `$ref` e `allOf`. Tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e  `allOf` resolvido. Tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | XDM bruto com `$ref` e `allOf`. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e  `allOf` resolvido. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e  `allOf` resolvido. Os descritores estão incluídos. |

>[!NOTE]
>
>Se apenas for fornecida a versão principal (por exemplo, 1, 2, 3), o registro retornará a versão secundária mais recente (por exemplo, .1, .2, .3) automaticamente.

## Restrições de campo XDM e práticas recomendadas

Os campos de um schema são listados em seu objeto `properties`. Cada campo é um objeto, contendo atributos para descrever e restringir os dados que o campo pode conter.

Para obter mais informações sobre a definição de tipos de campos na API, consulte [Appendix](appendix.md) deste guia, incluindo amostras de código e restrições opcionais para os tipos de dados mais usados.

O campo de amostra a seguir ilustra um campo XDM formatado corretamente, com mais detalhes sobre restrições de nomenclatura e práticas recomendadas fornecidas abaixo. Essas práticas também podem ser aplicadas na definição de outros recursos que contenham atributos semelhantes.

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

* O nome de um objeto de campo pode conter caracteres alfanuméricos, traço ou sublinhado, mas **não pode** start com um sublinhado.
   * **Correto:** `fieldName`,  `field_name2`,  `Field-Name`,  `field-name_3`
   * **Incorreto:** `_fieldName`
* camelCase é o preferido para o nome do objeto field. Exemplo: `fieldName`
* O campo deve incluir um `title`, gravado em Caso de título. Exemplo: `Field Name`
* O campo requer um `type`.
   * A definição de certos tipos pode exigir um `format` opcional.
   * Quando uma formatação específica de dados é necessária, `examples` pode ser adicionado como uma matriz.
   * O tipo de campo também pode ser definido usando qualquer tipo de dados no registro. Consulte a seção sobre [como criar um tipo de dados](./data-types.md#create) no guia de ponto de extremidade de tipos de dados para obter mais informações.
* O `description` explica o campo e as informações pertinentes sobre os dados do campo. Deve ser escrito em frases completas, com linguagem clara, para que qualquer pessoa que acesse o schema possa entender a intenção do campo.

Consulte o documento em [restrições de campo](../schema/field-constraints.md) para obter mais informações sobre como definir tipos de campos diferentes na API.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Schema Registry], selecione um dos guias de ponto de extremidade disponíveis.
