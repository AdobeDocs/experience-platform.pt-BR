---
title: Endpoint da API de Cota
description: O ponto de extremidade /quota na API da higiene de dados permite monitorar o uso do gerenciamento avançado do ciclo de vida dos dados em relação aos limites de cota mensais de sua organização para cada tipo de processo.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---

# Endpoint da cota

A variável `/quota` O endpoint na API da higiene de dados permite monitorar o uso do gerenciamento avançado do ciclo de vida dos dados em relação aos limites de cota da organização para cada tipo de processo.

As cotas são aplicadas para cada tipo de trabalho do ciclo de vida dos dados das seguintes maneiras:

* As exclusões e atualizações de registros estão limitadas a um determinado número de solicitações a cada mês.
* As expirações de conjunto de dados têm um limite simples para o número de trabalhos ativos simultaneamente, independentemente de quando as expirações serão executadas.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para obter as seguintes informações:

* Links para a documentação relacionada
* Um guia para ler as chamadas de API de amostra neste documento
* Informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API Experience Platform

## Listar cotas {#list}

É possível exibir as informações de cota de sua organização fazendo uma solicitação GET ao `/quota` terminal.

**Formato da API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUOTA_TYPE}` | Um parâmetro de consulta opcional que especifica o tipo de cota a ser recuperada. Se não `quotaType` for fornecido, todos os valores de cota serão retornados na resposta da API. Os valores de tipo aceitos incluem:<ul><li>`expirationDatasetQuota`: expirações do conjunto de dados</li><li>`deleteIdentityWorkOrderDatasetQuota`: exclusões de registro</li><li>`fieldUpdateWorkOrderDatasetQuota`: Atualizações de registro</li></ul> |

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

Uma resposta bem-sucedida retorna os detalhes das cotas de ciclo de vida dos dados.

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
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `quotas` | Lista as informações de cota para cada tipo de trabalho do ciclo de vida dos dados. Cada objeto de cota contém as seguintes propriedades:<ul><li>`name`: O tipo de trabalho do ciclo de vida dos dados:<ul><li>`expirationDatasetQuota`: expirações do conjunto de dados</li><li>`deleteIdentityWorkOrderDatasetQuota`: exclusões de registro</li></ul></li><li>`description`: uma descrição do tipo de trabalho do ciclo de vida dos dados.</li><li>`consumed`: o número de trabalhos desse tipo executados no período mensal atual.</li><li>`quota`: o limite de cota para esse tipo de trabalho. Para exclusões e atualizações de registro, representa o número de trabalhos que podem ser executados para cada período mensal. Para expirações de conjunto de dados, representa o número de trabalhos que podem estar ativos simultaneamente em um determinado momento.</li></ul> |

{style="table-layout:auto"}
