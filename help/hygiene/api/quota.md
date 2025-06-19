---
title: Endpoint da API de Cota
description: O ponto de extremidade /quota na API da higiene de dados permite monitorar o uso do Gerenciamento avançado do ciclo de vida de dados em relação aos limites de cota mensais de sua organização para cada tipo de trabalho.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 4d34ae1885f8c4b05c7bb4ff9de9c0c0e26154bd
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# Endpoint da cota

O ponto de extremidade `/quota` na API da higiene de dados permite monitorar o uso do Gerenciamento avançado do ciclo de vida de dados em relação aos limites de cota da organização para cada tipo de trabalho.

O uso de cota é rastreado para cada tipo de trabalho do ciclo de vida dos dados. Os limites de cota reais dependem dos direitos da sua organização e podem ser revisados periodicamente. As expirações de conjuntos de dados estão sujeitas a um limite rígido no número de tarefas ativas ao mesmo tempo.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, consulte a [visão geral](./overview.md) para obter as seguintes informações:

* Links para a documentação relacionada
* Um guia para ler as chamadas de API de amostra neste documento
* Informações importantes sobre os cabeçalhos necessários para fazer chamadas para qualquer API do Experience Platform

## Cotas e cronogramas de processamento {#quotas}

As solicitações de exclusão de registros estão sujeitas a cotas e expectativas de nível de serviço com base em seus direitos de licença. Esses limites se aplicam às solicitações de exclusão baseadas em interface e API.

>[!TIP]
> 
>Este documento mostra como consultar seu uso em relação a limites baseados em direitos. Para obter uma descrição completa das camadas de cota, dos direitos de exclusão de registro e do comportamento da SLA, consulte os documentos [exclusão de registro com base na interface](../ui/record-delete.md#quotas) ou[exclusão de registro com base em API](./workorder.md#quotas).

## Listar cotas {#list}

Você pode exibir as informações de cota de sua organização fazendo uma solicitação GET para o ponto de extremidade `/quota`.

**Formato da API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{QUOTA_TYPE}` | Um parâmetro de consulta opcional que especifica o tipo de cota a ser recuperada. Se nenhum parâmetro `quotaType` for fornecido, todos os valores de cota serão retornados na resposta da API. Os valores de tipo aceitos incluem:<ul><li>`datasetExpirationQuota`: esse objeto mostra o número de expirações de conjunto de dados ativas simultaneamente para sua organização, e sua permissão total de expirações. </li><li>`dailyConsumerDeleteIdentitiesQuota`: este objeto mostra o número total de solicitações de exclusão de registro feitas hoje pela sua organização e o total de ajudas de custo diárias.<br>Observação: somente as solicitações aceitas são contadas. Se uma ordem de serviço for rejeitada por falhar na validação, essas exclusões de identidade não serão consideradas na sua cota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: este objeto mostra o número total de solicitações de exclusão de registro feitas por sua organização este mês e sua permissão mensal total.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: este objeto mostra o número total de solicitações de atualizações de registro feitas por sua organização este mês e sua mesada mensal total.</li></ul> |

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
      "quota": 1000000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 2000000
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
| -------- | ------- |
| `quotas` | Lista as informações de cota para cada tipo de trabalho do ciclo de vida dos dados. Cada objeto de cota contém as seguintes propriedades:<ul><li>`name`: O tipo de trabalho do ciclo de vida dos dados:<ul><li>`expirationDatasetQuota`: Expirações do conjunto de dados</li><li>`deleteIdentityWorkOrderDatasetQuota`: exclusões de registro</li></ul></li><li>`description`: uma descrição do tipo de trabalho do ciclo de vida dos dados.</li><li>`consumed`: O número de trabalhos desse tipo executados no período atual. O nome do objeto indica o período de cota.</li><li>`quota`: A atribuição para este tipo de trabalho para sua organização. Para exclusões e atualizações de registros, a cota representa o número de trabalhos que podem ser executados para cada período mensal. Para expirações de conjunto de dados, a cota representa o número de trabalhos que podem estar ativos simultaneamente em um determinado momento.</li></ul> |
