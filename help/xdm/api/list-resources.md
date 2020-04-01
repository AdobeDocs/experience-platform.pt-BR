---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recursos de Lista
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# Recursos de Lista

Você pode visualização uma lista de todos os recursos (schemas, classes, mixins ou tipos de dados) dentro de um container executando uma única solicitação GET. Para ajudar a filtrar os resultados, o Registro do Schema suporta o uso de parâmetros de query ao listar recursos.

Os parâmetros de query mais comuns incluem:

* `limit` - Limitar o número de recursos devolvidos. Exemplo: `limit=5` retornará uma lista de cinco recursos.
* `orderby` - Classifique os resultados por uma propriedade específica. Exemplo: `orderby=title` classificará os resultados por título em ordem crescente (A-Z). Adicionar um título `-` antes (`orderby=-title`) classificará os itens por título em ordem decrescente (Z-A).
* `property` - Filtre os resultados em qualquer atributo de nível superior. Por exemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` retorna somente misturas compatíveis com a classe de Perfil individual XDM.

Ao combinar vários parâmetros de query, eles devem ser separados por E comercial (`&`).

**Formato da API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container no qual os recursos estão localizados (&quot;global&quot; ou &quot;locatário&quot;). |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser recuperado da Biblioteca de Schemas. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |

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
| application/vnd.adobe.xed-id+json | Retorna um breve resumo de cada recurso, geralmente o cabeçalho preferencial para listagem |
| application/vnd.adobe.xed+json | Retorna o schema JSON completo para cada recurso, com original `$ref` e `allOf` incluído |

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
