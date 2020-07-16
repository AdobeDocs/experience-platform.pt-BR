---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Pesquisar um recurso
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 2%

---


# Pesquisar um recurso

Você pode pesquisar recursos específicos fazendo uma solicitação GET que inclua o recurso `$id` (URI codificado por URL) no caminho da solicitação.

**Formato da API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parâmetro | Descrição |
| --- | --- |
| `{CONTAINER_ID}` | O container no qual os recursos estão localizados (&quot;global&quot; ou &quot;locatário&quot;). |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser recuperado do [!DNL Schema Library]. Os tipos válidos são `datatypes`, `mixins`, `schemas`e `classes`. |
| `{RESOURCE_ID}` | O `$id` URI codificado por URL ou `meta:altId` do recurso. |

**Solicitação**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

As solicitações de pesquisa de recursos exigem que `version` sejam incluídas no cabeçalho Aceitar. Os seguintes cabeçalhos Accept estão disponíveis para pesquisas:

| Aceitar | Descrição |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Bruto com `$ref` e `allOf`, tem títulos e descrições. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido, tem títulos e descrições. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Bruto com `$ref` e `allOf`, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvido, sem títulos ou descrições. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` e `allOf` resolvidos, descritores incluídos. |

>[!NOTE]
>
>Se você fornecer apenas a `major` versão (1, 2, 3, etc), o registro retornará automaticamente a versão mais recente `minor` (.1, .2, .3 etc).

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do recurso. Os campos retornados dependem do cabeçalho Aceitar enviado na solicitação. Experimente com cabeçalhos Accept diferentes para comparar as respostas e determinar qual cabeçalho é melhor para o caso de uso.

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
