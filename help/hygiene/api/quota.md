---
title: Endpoint da API de Cota
description: O ponto de extremidade /quota na API da higiene de dados permite monitorar o uso do Gerenciamento avançado do ciclo de vida de dados em relação aos limites de cota mensais de sua organização para cada tipo de trabalho.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---

# Endpoint da cota

A variável `/quota` O endpoint na API da Higiene de dados permite monitorar o uso do Gerenciamento avançado do ciclo de vida dos dados em relação aos limites de cota de sua organização para cada tipo de processo.

As cotas são aplicadas para cada tipo de trabalho do ciclo de vida dos dados das seguintes maneiras:

* As exclusões e atualizações de registros estão limitadas a um determinado número de solicitações a cada mês.
* As expirações de conjunto de dados têm um limite simples para o número de trabalhos ativos simultaneamente, independentemente de quando as expirações serão executadas.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, reveja o [visão geral](./overview.md) para obter as seguintes informações:

* Links para a documentação relacionada
* Um guia para ler as chamadas de API de amostra neste documento
* Informações importantes sobre os cabeçalhos necessários para fazer chamadas para qualquer API Experience Platform

## Listar cotas {#list}

É possível exibir as informações de cota de sua organização fazendo uma solicitação GET ao `/quota` terminal.

**Formato da API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUOTA_TYPE}` | Um parâmetro de consulta opcional que especifica o tipo de cota a ser recuperada. Se não `quotaType` for fornecido, todos os valores de cota serão retornados na resposta da API. Os valores de tipo aceitos incluem:<ul><li>`datasetExpirationQuota`: esse objeto mostra o número de expirações de conjunto de dados ativas simultaneamente para sua organização e a quantidade total de expirações permitida. </li><li>`dailyConsumerDeleteIdentitiesQuota`: este objeto mostra o número total de solicitações de exclusão de registro feitas hoje pela sua organização e o total de ajudas de custo diárias.<br>Observação: somente as solicitações aceitas são contadas. Se uma ordem de serviço for rejeitada por falhar na validação, essas exclusões de identidade não serão consideradas na sua cota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: este objeto mostra o número total de solicitações de exclusão de registro feitas pela organização este mês e a permissão mensal total.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: este objeto mostra o número total de solicitações de atualizações de registros feitas por sua organização este mês e sua permissão mensal total.</li></ul> |

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
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Propriedade | Descrição |
| --- | --- |
| `quotas` | Lista as informações de cota para cada tipo de trabalho do ciclo de vida dos dados. Cada objeto de cota contém as seguintes propriedades:<ul><li>`name`: O tipo de trabalho do ciclo de vida dos dados:<ul><li>`expirationDatasetQuota`: expirações do conjunto de dados</li><li>`deleteIdentityWorkOrderDatasetQuota`: exclusões de registro</li></ul></li><li>`description`: uma descrição do tipo de trabalho do ciclo de vida dos dados.</li><li>`consumed`: O número de trabalhos desse tipo executados no período atual. O nome do objeto indica o período de cota.</li><li>`quota`: a alocação desse tipo de trabalho para sua organização. Para exclusões e atualizações de registros, a cota representa o número de trabalhos que podem ser executados para cada período mensal. Para expirações de conjunto de dados, a cota representa o número de trabalhos que podem estar ativos simultaneamente em um determinado momento.</li></ul> |

{style="table-layout:auto"}
