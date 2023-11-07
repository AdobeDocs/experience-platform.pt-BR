---
title: Ponto de acesso da API de ferramentas de ferramentas de sandbox
description: O ponto de extremidade /tools na API de ferramentas de sandbox permite recuperar dados JSON de tarefas no Adobe Experience Platform.
exl-id: 529cb7d6-6b3f-459c-be03-35fc28b891cf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 20%

---

# Endpoint de ferramentas

As ferramentas de sandbox permitem selecionar diferentes artefatos e exportá-los em um pacote. Um pacote pode consistir em um único objeto ou em vários objetos. Todos os objetos incluídos em um pacote precisam ser da mesma sandbox.

A variável `/tools` O endpoint na API de ferramentas da sandbox permite listar e recuperar dados JSON do trabalho.

## Detalhes do trabalho {#details}

Para buscar de forma independente os dados JSON do trabalho, faça uma solicitação GET ao `/tools` e forneça a ID do trabalho.

**Formato da API**

```http
GET /tools/job/{JOB_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| {JOB_ID} | A ID do trabalho que você deseja pesquisar. |

**Solicitação**

A solicitação a seguir recupera informações para {JOB_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/tools/job/{JOB_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da ID de trabalho consultada, fornecendo atualizações de status em tempo real conforme `completedTasks` e `failedTasks` são atualizados conforme o trabalho avança.

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "message": "Job with ID: 0fe588dc4af64f9f98396cb6b49afb6c found",
    "object": {
        "id": "0fe588dc4af64f9f98396cb6b49afb6c",
        "name": "acme",
        "description": "Acme Business Group",
        "visibility": "TENANT",
        "requestType": "IMPORT",
        "expiry": 0,
        "snapshotId": "dd0b89579d554d07a814a620a44f9e43",
        "createdTimestamp": 1696510894380,
        "modifiedTimestamp": 1696510894380,
        "type": "PARTIAL",
        "jobStatus": "SUCCESS",
        "jobType": "NEW",
        "counter": 0,
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
        "jobHash": "6n8iV3KS6OGb0YQIQBaGhoAKKNeATeROqzV8/zbkNM8=",
        "sourceSandbox": {
            "name": "acme-sandbox",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "empty": false
        },
        "destinationSandbox": {
            "name": "acme-sandbox1",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "empty": false
        },
        "completedTasks": [
            {
                "taskType": "POST",
                "taskStatus": "SUCCESS",
                "artifact": {
                    "id": "https://ns.adobe.com/cjmstage/mixins/68f038b712e54546f99035a20d6ead649ca9d5b135eb24de",
                    "type": "REGISTRY_MIXIN",
                    "found": false,
                    "count": 0,
                    "title": "drb",
                    "messages": [
                        {
                            "status": "CREATED",
                            "attempt": 1,
                            "message": "REGISTRY_MIXIN created. Source id=https://ns.adobe.com/cjmstage/mixins/68f038b712e54546f99035a20d6ead649ca9d5b135eb24de; Target id=https://ns.adobe.com/cjmstage/mixins/220968a10a69ced58180ff1ccbe4f03124e44d17a0f23383"
                        }
                    ],
                    "newId": "https://ns.adobe.com/cjmstage/mixins/220968a10a69ced58180ff1ccbe4f03124e44d17a0f23383"
                }
            },
            {
                "taskType": "POST",
                "taskStatus": "SUCCESS",
                "artifact": {
                    "id": "https://ns.adobe.com/cjmstage/schemas/3926d1ff658a191bcb511b7c4ec45afee1c146a5b152e500",
                    "type": "REGISTRY_SCHEMA",
                    "found": false,
                    "count": 0,
                    "title": "drbFormSubmissions",
                    "messages": [
                        {
                            "status": "CREATED",
                            "attempt": 1,
                            "message": "REGISTRY_SCHEMA created. Source id=https://ns.adobe.com/cjmstage/schemas/3926d1ff658a191bcb511b7c4ec45afee1c146a5b152e500; Target id=https://ns.adobe.com/cjmstage/schemas/5e32908b8db9b37a5f3e7b5851d6ffa9e3bf8487abaef3c5"
                        }
                    ],
                    "newId": "https://ns.adobe.com/cjmstage/schemas/5e32908b8db9b37a5f3e7b5851d6ffa9e3bf8487abaef3c5"
                }
            },
            {
                "taskType": "POST",
                "taskStatus": "SUCCESS",
                "artifact": {
                    "id": "651344d17c8c8d289d10a8e6",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0,
                    "title": "drbFormSubmissions",
                    "messages": [
                        {
                            "status": "CREATED",
                            "attempt": 1,
                            "message": "CATALOG_DATASET created. Source id=651344d17c8c8d289d10a8e6; Target id=651eb3af5901df289dcb4511"
                        }
                    ],
                    "newId": "651eb3af5901df289dcb4511"
                }
            }
        ],
        "importReplacementMap": {
            "651344d17c8c8d289d10a8e6": "651eb3af5901df289dcb4511",
            "5a3b530ee7c4b38e9b33a69d22bfb75a2c5020e5a7a61e51": "b6d8ae6376864e22ed8169a9dac3b2115d1c72b5c1d1bced",
            "https://ns.adobe.com/cjmstage/mixins/68f038b712e54546f99035a20d6ead649ca9d5b135eb24de": "https://ns.adobe.com/cjmstage/mixins/220968a10a69ced58180ff1ccbe4f03124e44d17a0f23383",
            "https://ns.adobe.com/cjmstage/schemas/3926d1ff658a191bcb511b7c4ec45afee1c146a5b152e500": "https://ns.adobe.com/cjmstage/schemas/5e32908b8db9b37a5f3e7b5851d6ffa9e3bf8487abaef3c5"
        },
        "sourceParentArtifactMap": {
            "651344d17c8c8d289d10a8e6": "745F37C35E4B776E0A49421B@AdobeOrg::ajo-object-copy::CATALOG_DATASET::6512ec5a5bcd5e289c33a594",
            "5a3b530ee7c4b38e9b33a69d22bfb75a2c5020e5a7a61e51": "745F37C35E4B776E0A49421B@AdobeOrg::ajo-object-copy::REGISTRY_DESCRIPTOR::9d20176f1eb3f09dac4070b4bd6c4f79e8debdc8a0535725",
            "https://ns.adobe.com/cjmstage/mixins/68f038b712e54546f99035a20d6ead649ca9d5b135eb24de": "745F37C35E4B776E0A49421B@AdobeOrg::ajo-object-copy::REGISTRY_MIXIN::https://ns.adobe.com/cjmstage/mixins/37d29b7590c59928583b4d9a189229261291e388b7aa1031",
            "https://ns.adobe.com/cjmstage/schemas/3926d1ff658a191bcb511b7c4ec45afee1c146a5b152e500": "745F37C35E4B776E0A49421B@AdobeOrg::ajo-object-copy::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/926a7aa38b7cc93b87dd03c8f73e6e7537651407c30b66a0"
        }
    }
}
```
