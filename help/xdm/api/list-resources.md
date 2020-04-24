---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recursos de Lista
topic: developer guide
translation-type: tm+mt
source-git-commit: 4b052cdd3aca9c771855b2dc2a97ca48c7b8ffb0

---


# Recursos de Lista

Você pode visualização uma lista de todos os recursos (schemas, classes, mixins ou tipos de dados) dentro de um container executando uma única solicitação GET.

>[!NOTE] Ao listar recursos, o resultado do Limite do Registro do Schema é definido como 300 itens. Para retornar recursos além desse limite, você deve usar parâmetros [de](#paging)paginação. Também é recomendável usar parâmetros de query para [filtrar os resultados](#filtering) e reduzir o número de recursos retornados.
>
> Se quiser substituir totalmente o limite de 300 itens, use o cabeçalho Aceitar `application/vnd.adobe.xdm-v2+json` para retornar todos os resultados em uma única solicitação.

**Formato da API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container no qual os recursos estão localizados (&quot;global&quot; ou &quot;locatário&quot;). |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser recuperado da Biblioteca de Schemas. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |
| `{QUERY_PARAMS`} | Parâmetros de query opcionais para filtrar os resultados. Consulte a seção sobre parâmetros [de](#query) query para obter mais informações. |

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
| application/vnd.adobe.xdm-v2+json | Retorna o schema JSON completo para todos os resultados em uma única solicitação, substituindo o limite de 300 itens. |

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

O Registro de Schemas suporta o uso de parâmetros de query para a página e filtrar os resultados ao listar os recursos.

>[!NOTE] Ao combinar vários parâmetros de query, eles devem ser separados por E comercial (`&`).

### Paginação {#paging}

Os parâmetros de query mais comuns para paginação incluem:

| Parâmetro | Descrição |
| --- | --- |
| `start` | Especifique para onde os resultados listados devem começar. Exemplo: Os resultados da lista do terceiro item retornado serão `start=2` . |
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
| (Nenhum) | A indicação apenas do nome da propriedade retorna somente entradas nas quais a propriedade existe. | `property=title` |

>[!TIP] Você pode usar o `property` parâmetro para filtrar as misturas por sua classe compatível. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente misturas compatíveis com a classe de Perfil individual XDM.
