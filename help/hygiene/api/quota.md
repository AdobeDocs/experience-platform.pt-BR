---
title: Endpoint da API de cota
description: O endpoint /quota na API da Higiene de Dados permite monitorar o uso da higiene de dados em relação aos limites de cota mensal da organização para cada tipo de trabalho.
source-git-commit: 364ada0c354ddba8a855945f4f806f5600f21416
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 3%

---

# Ponto final da quota

>[!IMPORTANT]
>
>Os recursos de higiene de dados no Adobe Experience Platform estão disponíveis apenas para organizações que compraram o Healthcare Shield.

O `/quota` O endpoint na API da Higiene de dados permite monitorar o uso da higiene de dados em relação aos limites de cota de sua organização para cada tipo de trabalho.

As cotas são aplicadas para cada tipo de trabalho de higiene de dados das seguintes maneiras:

* As exclusões de clientes e as atualizações de campo são limitadas a um determinado número de solicitações por mês.
* As expirações do conjunto de dados têm um limite fixo para o número de trabalhos ativos simultaneamente, independentemente de quando as expirações serão executadas.

## Introdução

O endpoint usado neste guia faz parte da API da Higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para as seguintes informações:

* Links para a documentação relacionada
* Um guia para ler as chamadas de API de exemplo neste documento
* Informações importantes sobre cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API do Experience Platform

## Listar cotas {#list}

Você pode visualizar as informações de cota de sua organização fazendo uma solicitação de GET para a `/quota` endpoint .

**Formato da API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUOTA_TYPE}` | Um parâmetro de consulta opcional que especifica o tipo de cota a ser recuperada. Se não `quotaType` for fornecido, todos os valores de cota serão retornados na resposta da API. Os valores de tipo aceitos incluem:<ul><li>`expirationDatasetQuota`: Expirações do conjunto de dados</li><li>`deleteIdentityWorkOrderDatasetQuota`: Exclusões de consumidores</li><li>`fieldUpdateWorkOrderDatasetQuota`: Atualizações de campo</li></ul> |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes de suas cotas de higiene de dados.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `quotas` | Lista as informações de cota para cada tipo de trabalho de higiene de dados. Cada objeto de cota contém as seguintes propriedades:<ul><li>`name`: Tipo de trabalho de higiene de dados:<ul><li>`expirationDatasetQuota`: Expirações do conjunto de dados</li><li>`deleteIdentityWorkOrderDatasetQuota`: Exclusões de consumidores</li></ul></li><li>`description`: Uma descrição do tipo de trabalho de higiene de dados.</li><li>`consumed`: O número de ordens de produção desse tipo são executadas no período mensal atual.</li><li>`quota`: O limite de cota para esse tipo de trabalho. Para exclusões de clientes e atualizações de campo, isso representa o número de tarefas que podem ser executadas para cada período mensal. Para expirações do conjunto de dados, representa o número de trabalhos que podem estar ativos simultaneamente em um determinado momento.</li></ul> |

{style=&quot;table-layout:auto&quot;}
