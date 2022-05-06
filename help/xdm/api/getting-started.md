---
keywords: Experience Platform, home, tópicos populares, api, API, XDM, sistema XDM, modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados de experiência, Modelo de dados, Modelo de dados, Registro do esquema, Registro do esquema;
solution: Experience Platform
title: Introdução à API do Registro de Schema
description: Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API do Registro de Schema.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 1%

---

# Introdução ao [!DNL Schema Registry] API

O [!DNL Schema Registry] A API permite criar e gerenciar vários recursos do Experience Data Model (XDM). Este documento fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para o [!DNL Schema Registry] API.

## Pré-requisitos

O uso do guia do desenvolvedor requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../schema/composition.md): Saiba mais sobre os componentes básicos dos esquemas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

O XDM usa a formatação Esquema JSON para descrever e validar a estrutura dos dados de experiência do cliente assimilados. Portanto, é altamente recomendável revisar a variável [documentação oficial do Esquema JSON](https://json-schema.org/) para uma melhor compreensão desta tecnologia subjacente.

## Lendo exemplos de chamadas de API

O [!DNL Schema Registry] A documentação da API fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos os recursos em [!DNL Experience Platform], incluindo os pertencentes ao [!DNL Schema Registry], são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação da sandbox](../../sandboxes/home.md).

Todas as solicitações de pesquisa (GET) para a [!DNL Schema Registry] exigir um `Accept` , cujo valor determina o formato das informações retornadas pela API. Consulte a [Aceitar cabeçalho](#accept) para obter mais detalhes.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna informações sobre o uso da variável [!DNL Schema Registry]. Isso inclui uma `tenantId` , cujo valor é o seu `TENANT_ID`.

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

## Entenda o `CONTAINER_ID` {#container}

Chamadas à [!DNL Schema Registry] A API requer o uso de um `CONTAINER_ID`. Há dois contêineres para fazer chamadas de API: o `global` e o `tenant` contêiner.

### Contêiner global

O `global` o contêiner contém todos os Adobe padrão e [!DNL Experience Platform] o parceiro forneceu classes, grupos de campos de esquema, tipos de dados e esquemas. Você só pode executar solicitações de lista e pesquisa (GET) em relação à variável `global` contêiner.

Um exemplo de chamada que usa a variável `global` contêiner seria semelhante ao seguinte:

```http
GET /global/classes
```

### Contêiner de locatário

Não confundir com seu `TENANT_ID`, o `tenant` O contêiner contém todas as classes, grupos de campos, tipos de dados, esquemas e descritores definidos por uma Organização IMS. Elas são exclusivas de cada organização, o que significa que não são visíveis ou gerenciáveis por outras Orgs do IMS. Você pode executar todas as operações CRUD (GET, POST, PUT, PATCH, DELETE) em relação aos recursos que você cria na `tenant` contêiner.

Um exemplo de chamada que usa a variável `tenant` contêiner seria semelhante ao seguinte:

```http
POST /tenant/fieldgroups
```

Ao criar uma classe, grupo de campos, esquema ou tipo de dados na `tenant` , ele é salvo no [!DNL Schema Registry] e atribuiu uma `$id` URI que inclui `TENANT_ID`. Essa `$id` é usada em toda a API para fazer referência a recursos específicos. Exemplos de `$id` são fornecidos na próxima seção.

## Identificação do recurso {#resource-identification}

Os recursos XDM são identificados com um `$id` no formato de um URI, como os seguintes exemplos:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para tornar o URI mais compatível com REST, os schemas também têm uma codificação de notação de pontos do URI em uma propriedade chamada `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Chamadas à [!DNL Schema Registry] A API oferecerá suporte a `$id` URI ou o `meta:altId` (formato de notação de pontos). A prática recomendada é usar o cookie codificado por URL `$id` URI ao fazer uma chamada REST para a API, da seguinte maneira:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceitar cabeçalho {#accept}

Ao executar operações de lista e pesquisa (GET) no [!DNL Schema Registry] API, um `Accept` é necessário para determinar o formato dos dados retornados pela API. Ao pesquisar recursos específicos, um número de versão também deve ser incluído na variável `Accept` cabeçalho.

A tabela a seguir lista os compatíveis `Accept` valores de cabeçalho, incluindo aqueles com números de versão, juntamente com descrições do que a API retornará quando forem usadas.

| Accept | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retorna somente uma lista de IDs. Isso é usado mais frequentemente para listar recursos. |
| `application/vnd.adobe.xed+json` | Retorna uma lista de esquema JSON completo com o original `$ref` e `allOf` incluído. Isso é usado para retornar uma lista de recursos completos. |
| `application/vnd.adobe.xed+json; version=1` | XDM bruto com `$ref` e `allOf`. Possui títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` atributos e `allOf` resolvido. Possui títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM bruto com `$ref` e `allOf`. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` atributos e `allOf` resolvido. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` atributos e `allOf` resolvido. Os descritores são incluídos. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>No momento, a plataforma suporta apenas uma versão principal para cada esquema (`1`). Portanto, o valor de `version` deve ser sempre `1` ao executar solicitações de pesquisa para retornar a versão secundária mais recente do esquema. Consulte a subseção abaixo para obter mais informações sobre o controle de versão do schema.

### Controle de versão do esquema {#versioning}

As versões de esquema são referenciadas por `Accept` cabeçalhos na API do Registro de Schema e em `schemaRef.contentType` propriedades em cargas downstream da API do serviço da plataforma.

Atualmente, a Platform suporta apenas uma única versão principal (`1`) para cada schema. De acordo com a [regras de evolução do schema](../schema/composition.md#evolution), cada atualização em um schema deve ser não destrutiva, o que significa que novas versões secundárias de um schema (`1.2`, `1.3`, etc.) são sempre compatíveis com versões secundárias anteriores. Portanto, ao especificar `version=1`, o Registro de Schema sempre retorna a variável **mais recente** versão principal `1` de um schema , o que significa que versões anteriores secundárias não são retornadas.

>[!NOTE]
>
>O requisito não destrutivo da evolução do schema é empregado somente após o schema ter sido referenciado por um conjunto de dados e um dos seguintes casos ser verdadeiro:
>
>* Os dados foram assimilados no conjunto de dados.
>* O conjunto de dados foi ativado para uso no Perfil do cliente em tempo real (mesmo se nenhum dado tiver sido assimilado).
>
>Se o esquema não tiver sido associado a um conjunto de dados que atende a um dos critérios acima, qualquer alteração poderá ser feita nele. No entanto, em todos os casos, o `version` o componente ainda permanece em `1`.

## Restrições de campo e práticas recomendadas do XDM

Os campos de um schema são listados em suas `properties` objeto. Cada campo é um objeto contendo atributos para descrever e restringir os dados que o campo pode conter. Consulte o guia em [definição de campos personalizados na API](../tutorials/custom-fields-api.md) para amostras de código e restrições opcionais para os tipos de dados mais usados.

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

* O nome de um objeto de campo pode conter caracteres alfanuméricos, traço ou sublinhados, mas **podem não** comece com um sublinhado.
   * **Correto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorreto:** `_fieldName`
* camelCase é preferível para o nome do objeto de campo. Exemplo: `fieldName`
* O campo deve incluir uma `title`, escrito em Caso de título. Exemplo: `Field Name`
* O campo requer um `type`.
   * A definição de certos tipos pode exigir uma `format`.
   * Quando for necessária uma formatação específica dos dados, `examples` pode ser adicionado como uma matriz.
   * O tipo de campo também pode ser definido usando qualquer tipo de dados no registro. Consulte a seção sobre [criação de um tipo de dados](./data-types.md#create) no guia do endpoint tipos de dados para obter mais informações.
* O `description` explica o campo e as informações pertinentes sobre os dados do campo. Ele deve ser escrito em frases completas com linguagem clara para que qualquer pessoa que acessar o esquema possa entender a intenção do campo.

## Próximas etapas

Para começar a fazer chamadas usando a variável [!DNL Schema Registry] Selecione um dos guias de endpoint disponíveis para a API.
