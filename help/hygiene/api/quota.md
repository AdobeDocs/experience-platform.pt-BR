---
title: Endpoint da API de Cota
description: O ponto de extremidade /quota na API da higiene de dados permite monitorar o uso do Gerenciamento avançado do ciclo de vida de dados em relação aos limites de cota mensais de sua organização para cada tipo de trabalho.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 2%

---

# Endpoint da cota

Use o ponto de extremidade `/quota` na API de higiene de dados para verificar o uso e os limites atuais de sua organização. As cotas variam de acordo com os direitos, como o Privacy and Security Shield ou Healthcare Shield.

Monitore o consumo atual de cota para garantir a conformidade com os limites organizacionais para cada tipo de trabalho.

## Introdução

O endpoint usado neste guia faz parte da API de higiene de dados. Antes de continuar, consulte a [visão geral](./overview.md) para obter as seguintes informações:

* Links de documentação relacionados
* Como ler chamadas de API de amostra
* Cabeçalhos obrigatórios para chamadas de API do Experience Platform

## Cotas e cronogramas de processamento {#quotas}

As solicitações de exclusão de registros estão sujeitas a cotas e expectativas de nível de serviço com base em seus direitos de licença. Esses limites se aplicam às solicitações de exclusão baseadas em interface e API.

>[!TIP]
>
>Este documento mostra como consultar seu uso em relação a limites baseados em direitos. Para obter uma descrição completa das camadas de cota, dos direitos de exclusão de registro e do comportamento da SLA, consulte os documentos [exclusão de registro com base na interface](../ui/record-delete.md#quotas) ou [exclusão de registro com base em API](./workorder.md#quotas).

## Listar cotas {#list}

Você pode exibir as informações de cota de sua organização fazendo uma solicitação GET para o ponto de extremidade `/quota`.

**Formato da API**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>O consumo de cota é redefinido diariamente e mensalmente no primeiro dia de cada mês às 00:00 GMT.
>
>Somente as solicitações aceitas são contabilizadas na sua cota. Ordens de serviço rejeitadas não reduzem sua cota.

| Parâmetro | Descrição |
| --- | --- |
| `{QUOTA_TYPE}` | Um parâmetro de consulta opcional que especifica o tipo de cota a ser recuperada. Se nenhum parâmetro `quotaType` for fornecido, todos os valores de cota serão retornados na resposta da API. Os valores aceitos incluem:<ul><li>`datasetExpirationQuota`: o número de expirações do conjunto de dados ativo e sua permissão total.</li><li>`dailyConsumerDeleteIdentitiesQuota`: O número de exclusões de registros hoje e sua cota diária.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: o número de exclusões de registro este mês e sua cota mensal.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Propriedade | Descrição |
| -------- | ------- |
| `quotas` | Lista as informações de cota para cada tipo de trabalho do ciclo de vida dos dados. Cada objeto de cota contém as seguintes propriedades:<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | O identificador de tipo de cota. |
| `description` | Uma descrição dos limites dessa cota. |
| `consumed` | A quantidade de cota consumida no momento. A quantidade consumida é redefinida no primeiro dia do mês, às 00:00 GMT e 00:00 GMT para a cota diária. |
| `quota` | A alocação máxima deste tipo de cota para sua organização. |
