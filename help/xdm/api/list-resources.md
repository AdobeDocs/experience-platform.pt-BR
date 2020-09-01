---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;list;List;get;GET
solution: Experience Platform
title: Recursos de lista
description: Você pode visualização uma lista de todos os recursos do Registro de Schemas de um determinado tipo (classes, mixins, schemas, tipos de dados ou descritores) em um container executando uma única solicitação de GET.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---


# Recursos de lista

Você pode visualização uma lista de todos os [!DNL Schema Registry] recursos de um determinado tipo (classes, mixins, schemas, tipos de dados ou descritores) em um container executando uma única solicitação de GET.

>[!NOTE]
>
>Ao listar recursos, o resultado [!DNL Schema Registry] limita a 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros [de](#paging)paginação. Também é recomendável usar parâmetros de query para [filtrar os resultados](#filtering) e reduzir o número de recursos retornados.

**Formato da API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container no qual os recursos estão localizados (&quot;global&quot; ou &quot;locatário&quot;). |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser recuperado do [!DNL Schema Library]. Os tipos válidos são `classes`, `mixins`, `schemas`, `datatypes`e `descriptors`. |
| `{QUERY_PARAMS}` | Parâmetros de query opcionais para filtrar os resultados. Consulte a seção sobre parâmetros [de](#query) query para obter mais informações. |

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

O formato de resposta depende do cabeçalho Aceitar enviado na solicitação. Os seguintes cabeçalhos Accept estão disponíveis para recursos de listagem:

| Aceitar cabeçalho | Descrição |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Retorna um breve resumo de cada recurso. Este é o cabeçalho recomendado para a listagem de recursos. (Limite: 300) |
| application/vnd.adobe.xed+json | Retorna o schema JSON completo para cada recurso, com original `$ref` e `allOf` incluído. (Limite: 300) |
| application/vnd.adobe.xdm-v2+json | Ao usar o `/descriptors` terminal, esse cabeçalho Accept deve ser usado para utilizar os recursos de paginação. |

**Resposta**

A solicitação acima usou o cabeçalho `application/vnd.adobe.xed-id+json` Aceitar, portanto, a resposta inclui apenas os atributos `title`, `$id`, `meta:altId`e `version` de cada recurso. A substituição `full` no cabeçalho Aceitar retorna todos os atributos de cada recurso. Selecione o cabeçalho Aceitar apropriado, dependendo das informações necessárias na sua resposta.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Uso de parâmetros de query {#query}

O [!DNL Schema Registry] oferece suporte ao uso de parâmetros de query para a página e filtrar resultados ao listar recursos.

>[!NOTE]
>
>Ao combinar vários parâmetros de query, eles devem ser separados por E comercial (`&`).

### Paginação {#paging}

Os parâmetros de query mais comuns para paginação incluem:

| Parâmetro | Descrição |
| --- | --- |
| `start` | Especifique onde os resultados listados devem começar. Esse valor pode ser obtido a partir do `_page.next` atributo de uma resposta de lista e usado para acessar a próxima página de resultados. Se o `_page.next` valor for nulo, então não há nenhuma página adicional disponível. |
| `limit` | Limite o número de recursos retornados. Exemplo: `limit=5` retornará uma lista de cinco recursos. |
| `orderby` | Classifique os resultados por uma propriedade específica. Exemplo: `orderby=title` classificará os resultados por título em ordem crescente (A-Z). Adicionar um título `-` antes (`orderby=-title`) classificará os itens por título em ordem decrescente (Z-A). |

### Filtragem {#filtering}

Você pode filtrar os resultados usando o `property` parâmetro, que é usado para aplicar um operador específico em relação a uma determinada propriedade JSON dentro dos recursos recuperados. Os operadores suportados incluem:

| Operador | Descrição | Exemplo |
| --- | --- | --- |
| `==` | Filtros se a propriedade é igual ao valor fornecido. | `property=title==test` |
| `!=` | Filtros se a propriedade não é igual ao valor fornecido. | `property=title!=test` |
| `<` | Filtros se a propriedade é menor que o valor fornecido. | `property=version<5` |
| `>` | Filtros se a propriedade é maior que o valor fornecido. | `property=version>5` |
| `<=` | Filtros se a propriedade é menor ou igual ao valor fornecido. | `property=version<=5` |
| `>=` | Filtros se a propriedade é maior ou igual ao valor fornecido. | `property=version>=5` |
| `~` | Filtros se a propriedade corresponde a uma expressão regular fornecida. | `property=title~test$` |
| (None) | A indicação apenas do nome da propriedade retorna somente entradas nas quais a propriedade existe. | `property=title` |

>[!TIP]
>
>Você pode usar o `property` parâmetro para filtrar as misturas por sua classe compatível. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente misturas compatíveis com a [!DNL XDM Individual Profile] classe.
