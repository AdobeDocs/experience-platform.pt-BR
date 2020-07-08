---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor da API de Registro do Schema
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---


# Guia do desenvolvedor da API de Registro do Schema

O Registro do Schema é usado para acessar a Biblioteca de Schemas no Adobe Experience Platform, fornecendo uma interface do usuário e uma API RESTful a partir da qual todos os recursos disponíveis da biblioteca estão acessíveis.

Usando a API do Registro do Schema, você pode executar operações CRUD básicas para visualização e gerenciamento de todos os schemas e recursos relacionados disponíveis para você no Adobe Experience Platform. Isso inclui aqueles definidos pela Adobe, parceiros de Experience Platform e fornecedores cujos aplicativos você usa. Você também pode usar chamadas de API para criar novos schemas e recursos para sua organização, bem como visualização e editar recursos que já foram definidos.

Este guia do desenvolvedor fornece etapas para ajudá-lo a start usando a API de registro do Schema. O guia então fornece exemplos de chamadas de API para executar operações principais usando o Registro do Schema.

## Pré-requisitos

Este guia exige uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM.
* [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
* [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para a API do Registro do Schema.

## Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para as APIs da Platform, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform, incluindo os pertencentes ao Registro do Schema, estão isolados para caixas de proteção virtuais específicas. Todas as solicitações às APIs do Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações de pesquisa (GET) para o Registro do Schema exigem um cabeçalho Accept adicional, cujo valor determina o formato das informações retornadas pela API. Consulte a seção [Aceitar cabeçalho](#accept) abaixo para obter mais detalhes.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Conheça sua TENANT_ID {#know-your-tenant_id}

Ao longo deste guia você verá referências a um `TENANT_ID`. Essa ID é usada para garantir que os recursos criados sejam devidamente nomeados e estejam contidos em sua Organização IMS. Se você não souber sua ID, poderá acessá-la executando a seguinte solicitação GET:

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

Uma resposta bem-sucedida retorna informações sobre o uso do Registro do Schema por parte de sua organização. Isso inclui um `tenantId` atributo cujo valor é o seu `TENANT_ID`.

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

* `tenantId`: O `TENANT_ID` valor da sua Organização IMS.

## Entenda o `CONTAINER_ID` {#container}

As chamadas à API do Registro do Schema exigem o uso de um `CONTAINER_ID`. Há dois container contra os quais as chamadas de API podem ser feitas: o container **** global e o container **do** locatário.

### container global

O container global contém todas as classes padrão, mixins, tipos de dados e schemas fornecidos pela Adobe e por parceiros de Experience Platform. Você só pode executar solicitações de lista e pesquisa (GET) em relação ao container global.

### container de inquilino

Para não ser confundido com o seu exclusivo `TENANT_ID`, o container locatário armazena todas as classes, misturas, tipos de dados, schemas e descritores definidos por uma Organização IMS. Elas são exclusivas de cada organização, o que significa que não são visíveis ou gerenciáveis por outras Organizações IMS. Você pode executar todas as operações CRUD (GET, POST, PUT, PATCH, DELETE) em relação aos recursos criados no container do locatário.

Quando você cria uma classe, combinação, schema ou tipo de dados no container do locatário, ela é salva no Registro do Schema e recebe um `$id` URI que inclui seu `TENANT_ID`. Isso `$id` é usado em toda a API para fazer referência a recursos específicos. Exemplos de `$id` valores são fornecidos na próxima seção.

## identificação do Schema {#schema-identification}

Os Schemas são identificados com um `$id` atributo na forma de um URI, como:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Para tornar o URI mais compatível com REST, os schemas também têm uma codificação de notação de pontos do URI em uma propriedade chamada `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

As chamadas para a API do Registro do Schema oferecerão suporte ao `$id` URI codificado por URL ou ao `meta:altId` (formato de notação de pontos). A prática recomendada é usar o `$id` URI codificado por URL ao fazer uma chamada REST para a API, como:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Aceitar cabeçalho {#accept}

Ao executar operações de lista e pesquisa (GET) na API do Registro do Schema, um cabeçalho Accept é necessário para determinar o formato dos dados retornados pela API. Ao procurar recursos específicos, um número de versão também deve ser incluído no cabeçalho Aceitar.

A tabela a seguir lista valores de cabeçalho compatíveis com o Accept, incluindo aqueles com números de versão, juntamente com descrições do que a API retornará quando for usada.

| Aceitar | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retorna apenas uma lista de IDs. Isso é usado com mais frequência para a listagem de recursos. |
| `application/vnd.adobe.xed+json` | Retorna uma lista de schema JSON completo com original `$ref` e `allOf` incluído. Isto é usado para devolver uma lista de recursos completos. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | XDM bruto com `$ref` e `allOf`. Tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido. Tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | XDM bruto com `$ref` e `allOf`. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido. Sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido. Os descritores estão incluídos. |

>[!NOTE]
>
>Se apenas for fornecida a `major` versão (por exemplo, 1, 2, 3), o registro retornará a versão mais recente `minor` (por exemplo, .1, .2, .3) automaticamente.

## Restrições de campo XDM e práticas recomendadas

Os campos de um schema são listados dentro de seu `properties` objeto. Cada campo é um objeto, contendo atributos para descrever e restringir os dados que o campo pode conter.

Para obter mais informações sobre a definição de tipos de campos na API, consulte o [apêndice](appendix.md) deste guia, incluindo exemplos de código e restrições opcionais para os tipos de dados mais usados.

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

* O nome de um objeto de campo pode conter caracteres alfanuméricos, traço ou sublinhado, mas não **pode** start com um sublinhado.
   * **Correto:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorreto:** `_fieldName`
* camelCase é o preferido para o nome do objeto field. Exemplo: `fieldName`
* O campo deve incluir um `title`, escrito em Caso de título. Exemplo: `Field Name`
* O campo requer um `type`.
   * A definição de certos tipos pode exigir uma opção `format`.
   * Quando uma formatação específica de dados é necessária, `examples` pode ser adicionada como uma matriz.
   * O tipo de campo também pode ser definido usando qualquer tipo de dados no registro. Consulte a seção sobre como [criar um tipo](create-data-type.md) de dados neste guia para obter mais informações.
* O `description` explica o campo e as informações pertinentes sobre os dados do campo. Deve ser escrito em frases completas, com linguagem clara, para que qualquer pessoa que acesse o schema possa entender a intenção do campo.

Consulte o [apêndice](appendix.md) para obter mais informações sobre como definir tipos de campos na API.

## Próximas etapas

Este documento cobriu os conhecimentos de pré-requisito necessários para fazer chamadas para a API do Registro do Schema, incluindo as credenciais de autenticação necessárias. Agora você pode continuar com as chamadas de amostra fornecidas neste guia do desenvolvedor e seguir com suas instruções. Para obter uma apresentação passo a passo sobre como fazer um schema na API, consulte o [tutorial](../tutorials/create-schema-api.md)a seguir.
