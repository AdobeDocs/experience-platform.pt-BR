---
title: Excluir registros usando a API de higiene de dados
description: Saiba como corrigir ou excluir programaticamente os dados pessoais armazenados dos clientes no Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---

# Excluir registros usando a API de higiene de dados

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

A API de higiene de dados permite corrigir ou excluir programaticamente os dados pessoais armazenados dos clientes no Adobe Experience Platform.

Você pode acessar a API por meio do mesmo caminho raiz da variável [API PRIVACY SERVICE](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## Introdução

Esta seção fornece uma introdução aos conceitos principais que você precisa saber antes de tentar fazer chamadas para a API de higiene de dados.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para a API de higiene de dados, primeiro colete suas credenciais de autenticação. Essas são as mesmas credenciais usadas para acessar a API Privacy Service. Consulte a [Visão geral da API](./overview.md#getting-started) para gerar valores para cada um dos cabeçalhos necessários para a API de higiene de dados, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

### Leitura de chamadas de API de amostra

Este documento fornece um exemplo de chamada de API para demonstrar como formatar suas solicitações. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/api-guide.md#sample-api) no guia de introdução às APIs Experience Platform.

## Criar um trabalho de exclusão

Você pode criar um trabalho de exclusão fazendo uma solicitação POST.

**Formato da API**

```http
POST /jobs
```

**Solicitação**

A carga da solicitação é estruturada de forma semelhante à de um [excluir solicitação na API Privacy Service](../../privacy-service/api/privacy-jobs.md#access-delete). Inclui uma `users` matriz cujos objetos representam os usuários cujos dados serão excluídos.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `companyContexts` | Uma matriz que contém informações de autenticação para sua organização. Ele deve conter um único objeto com as seguintes propriedades: <ul><li>`namespace`: Deve ser definido como `imsOrgID`.</li><li>`value`: Seu ID da Org de IMS. Esse é o mesmo valor fornecido na variável `x-gw-ims-org-id` cabeçalho.</li></ul> |
| `users` | Uma matriz que contém uma coleção de pelo menos um usuário cujas informações você deseja excluir. Cada objeto de usuário contém as seguintes informações: <ul><li>`key`: um identificador para um usuário que é usado para qualificar as IDs de trabalho separadas nos dados de resposta. É uma prática recomendada escolher uma string exclusiva e de fácil identificação para esse valor, para que ele possa ser referenciado ou pesquisado posteriormente.</li><li>`action`: uma matriz que lista as ações desejadas para tomar os dados do usuário. Deve conter um único valor de sequência de caracteres: `delete`.</li><li>`userIDs`: uma coleção de identidades para o usuário. O número de identidades que um único usuário pode ter é limitado a nove. Cada identidade contém as seguintes propriedades: <ul><li>`namespace`: A variável [namespace de identidade](../../identity-service/namespaces.md) associado à ID. Isso pode ser um [namespace padrão](../../privacy-service/api/appendix.md#standard-namespaces) reconhecido pela Platform ou pode ser um namespace personalizado definido por sua organização. O tipo de namespace usado deve ser refletido no `type` propriedade.</li><li>`value`: o valor da identidade.</li><li>`type`: deve ser definido como `standard` se estiver usando um namespace reconhecido globalmente ou `custom` se estiver usando um namespace definido por sua organização.</li></ul></li></ul> |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos trabalhos criados.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
