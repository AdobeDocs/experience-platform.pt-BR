---
keywords: Experience Platform;início;tópicos populares;api;API;XDM;sistema XDM;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;modelo de dados;registro de esquema;Registro de esquema;
solution: Experience Platform
title: Introdução à API do Registro de esquema
description: Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Registro de esquema.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# Introdução ao [!DNL Schema Registry] API

A variável [!DNL Schema Registry] A API permite criar e gerenciar vários recursos do Experience Data Model (XDM). Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [!DNL Schema Registry] API.

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O XDM usa a formatação do esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Portanto, é altamente recomendável que você analise a [Documentação oficial do esquema JSON](https://json-schema.org/) para compreender melhor essa tecnologia subjacente.

## Leitura de chamadas de API de amostra

A variável [!DNL Schema Registry] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo as que pertencem à [!DNL Schema Registry], são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação da sandbox](../../sandboxes/home.md).

Todas as solicitações de pesquisa (GET) para o [!DNL Schema Registry] exigir uma `Accept` cujo valor determina o formato das informações retornadas pela API. Consulte a [Aceitar cabeçalho](#accept) abaixo para obter mais detalhes.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Conhecer seu TENANT_ID {#know-your-tenant_id}

Em todos os guias de API, você verá referências a uma `TENANT_ID`. Essa ID é usada para garantir que os recursos criados tenham o namespace adequado e estejam contidos na Organização IMS. Caso não saiba a ID, é possível acessá-la executando a seguinte solicitação do GET:

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

Uma resposta bem-sucedida retorna informações sobre o uso da [!DNL Schema Registry]. Isso inclui uma `tenantId` atributo, cujo valor é seu `TENANT_ID`.

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

## Compreender o `CONTAINER_ID` {#container}

Chamadas para a [!DNL Schema Registry] A API exige o uso de um `CONTAINER_ID`. Há dois contêineres nos quais as chamadas de API podem ser feitas: o `global` contêiner e o `tenant` recipiente.

### Contêiner global

A variável `global` o contêiner contém todos os Adobe e [!DNL Experience Platform] o parceiro forneceu classes, grupos de campos de esquema, tipos de dados e esquemas. Você só pode executar solicitações de lista e pesquisa (GET) em relação ao `global` recipiente.

Um exemplo de uma chamada que usa a variável `global` O contêiner seria semelhante ao seguinte:

```http
GET /global/classes
```

### Contêiner do inquilino

Para não ser confundido com o seu `TENANT_ID`, o `tenant` O container contém todas as classes, grupos de campos, tipos de dados, esquemas e descritores definidos por uma Organização IMS. Elas são exclusivas de cada organização, o que significa que não são visíveis ou gerenciáveis por outras organizações IMS. Você pode executar todas as operações CRUD (GET, POST, PUT, PATCH, DELETE) em relação aos recursos criados na `tenant` recipiente.

Um exemplo de uma chamada que usa a variável `tenant` O contêiner seria semelhante ao seguinte:

```http
POST /tenant/fieldgroups
```

Ao criar uma classe, grupo de campos, esquema ou tipo de dados no `tenant` contêiner, ele é salvo no [!DNL Schema Registry] e foi atribuído um `$id` URI que inclui seu `TENANT_ID`. Este `$id` O é usado em toda a API para fazer referência a recursos específicos. Exemplos de `$id` Os valores de são fornecidos na próxima seção.

## Identificação do recurso {#resource-identification}

Os recursos XDM são identificados com um `$id` no formato de um URI, como os seguintes exemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para tornar o URI mais amigável, os esquemas também têm uma codificação de notação de pontos do URI em uma propriedade chamada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Chamadas para a [!DNL Schema Registry] A API oferecerá suporte ao formato codificado por URL `$id` URI ou o `meta:altId` (formato de notação de pontos). A prática recomendada é usar o formato codificado por URL `$id` URI ao fazer uma chamada REST para a API, da seguinte maneira:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceitar cabeçalho {#accept}

Ao executar operações de lista e pesquisa (GET) no [!DNL Schema Registry] API, um `Accept` O cabeçalho é necessário para determinar o formato dos dados retornados pela API. Quando procurar recursos específicos, um número de versão também deve ser incluído na variável `Accept` cabeçalho.

A tabela a seguir lista itens compatíveis `Accept` Os valores de cabeçalho, incluindo aqueles com números de versão, juntamente com descrições do que a API retornará quando forem usados.

| Accept | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retorna somente uma lista de IDs. Isso é usado com mais frequência para listar recursos. |
| `application/vnd.adobe.xed+json` | Retorna uma lista do esquema JSON completo com o original `$ref` e `allOf` incluído. Isso é usado para retornar uma lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM bruto com `$ref` e `allOf`. Tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos e `allOf` resolvido. Tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM bruto com `$ref` e `allOf`. Nenhum título ou descrição. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` atributos e `allOf` resolvido. Nenhum título ou descrição. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` atributos e `allOf` resolvido. Os descritores estão incluídos. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` e `allOf` resolvida, tem títulos e descrições. Os campos obsoletos são indicados com uma `meta:status` atributo de `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>No momento, a plataforma oferece suporte a apenas uma versão principal para cada esquema (`1`). Portanto, o valor para `version` deve ser sempre `1` ao executar solicitações de pesquisa para retornar a versão secundária mais recente do esquema. Consulte a subseção abaixo para obter mais informações sobre o controle de versão do schema.

### Controle de versão do esquema {#versioning}

As versões do esquema são referenciadas por `Accept` cabeçalhos na API do Registro de Esquema e em `schemaRef.contentType` propriedades em cargas de API downstream do serviço de plataforma.

Atualmente, a Platform só oferece suporte a uma única versão principal (`1`) para cada schema. De acordo com a [regras de evolução do schema](../schema/composition.md#evolution), cada atualização em um schema não deve ser destrutiva, o que significa que novas versões secundárias de um schema (`1.2`, `1.3`, etc.) são sempre compatíveis com versões anteriores secundárias. Portanto, ao especificar `version=1`, o Registro de esquema sempre retorna o **mais recente** versão principal `1` de um schema , significando que as versões secundárias anteriores não são retornadas.

>[!NOTE]
>
>O requisito não destrutivo para a evolução do esquema só é aplicado depois que o esquema é referenciado por um conjunto de dados e um dos seguintes casos é verdadeiro:
>
>* Os dados foram assimilados no conjunto de dados.
>* O conjunto de dados foi ativado para uso no Perfil do cliente em tempo real (mesmo se nenhum dado tiver sido assimilado).
>
>Se o esquema não tiver sido associado a um conjunto de dados que atenda a um dos critérios acima, qualquer alteração poderá ser feita nele. No entanto, em todos os casos, a `version` componente ainda permanece em `1`.

## Restrições de campo XDM e práticas recomendadas

Os campos de um esquema são listados em seu `properties` objeto. Cada campo é um objeto que contém atributos para descrever e restringir os dados que o campo pode conter. Consulte o guia em [definição de campos personalizados na API](../tutorials/custom-fields-api.md) para amostras de código e restrições opcionais para os tipos de dados mais usados.

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

* O nome de um objeto de campo pode conter caracteres alfanuméricos, traços ou sublinhados, mas **não pode** comece com um sublinhado.
   * **Correto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorreto:** `_fieldName`
* camelCase é preferido para o nome do objeto de campo. Exemplo: `fieldName`
* O campo deve incluir uma `title`, escrito em Title Case. Exemplo: `Field Name`
* O campo requer um `type`.
   * A definição de determinados tipos pode exigir uma configuração `format`.
   * Sempre que seja exigida uma formatação específica dos dados, `examples` pode ser adicionado como uma matriz.
   * O tipo de campo também pode ser definido usando qualquer tipo de dados no registro. Consulte a seção sobre [criação de um tipo de dados](./data-types.md#create) no manual de endpoint de tipos de dados para obter mais informações.
* A variável `description` explica o campo e as informações pertinentes relacionadas aos dados do campo. Ele deve ser escrito em frases completas com linguagem clara para que qualquer pessoa que acesse o schema possa entender a intenção do campo.

## Próximas etapas

Para começar a fazer chamadas usando o [!DNL Schema Registry] , selecione um dos manuais de endpoint disponíveis.
