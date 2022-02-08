---
keywords: Experience Platform; home; tópicos populares; segmentação; Segmentação; Serviço de segmentação; agendamentos; agendamento; api; API;
solution: Experience Platform
title: Agendamentos do Ponto de Extremidade da API
topic-legacy: developer guide
description: Os agendamentos são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: a4f5602365d5db28ba375db0794b80670229fa75
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 4%

---

# Ponto de extremidade de agendamentos

Os agendamentos são uma ferramenta que pode ser usada para executar automaticamente tarefas de segmentação em lote uma vez por dia. Você pode usar o `/config/schedules` endpoint para recuperar uma lista de programações, criar uma nova programação, recuperar detalhes de uma programação específica, atualizar uma programação específica ou excluir uma programação específica.

## Introdução

Os endpoints usados neste guia fazem parte do [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

## Recuperar uma lista de programações {#retrieve-list}

Você pode recuperar uma lista de todas as programações para sua Organização IMS fazendo uma solicitação de GET para a `/config/schedules` endpoint .

**Formato da API**

O `/config/schedules` O endpoint oferece suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Fazer uma chamada para esse terminal sem parâmetros recuperará todos os agendamentos disponíveis para sua organização. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{START}` | Especifica de qual página o deslocamento começará. Por padrão, esse valor será 0. |
| `{LIMIT}` | Especifica o número de programações retornadas. Por padrão, esse valor será 100. |

**Solicitação**

A solicitação a seguir recuperará as últimas dez programações publicadas na organização IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de agendamentos para a organização IMS especificada como JSON.

>[!NOTE]
>
>A resposta a seguir foi truncada para espaço e mostra apenas o primeiro agendamento retornado.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propriedade | Descrição |
| -------- | ------------ |
| `_page.totalCount` | O número total de programações retornadas. |
| `_page.pageSize` | O tamanho da página de agendamentos. |
| `children.name` | O nome do agendamento como uma string. |
| `children.type` | O tipo de trabalho como uma string. Os dois tipos compatíveis são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `children.properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `children.properties.segments` | Usando `["*"]` garante que todos os segmentos sejam incluídos. |
| `children.schedule` | Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações de cron, leia o apêndice no [formato de expressão cron](#appendix). Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado às 1:00 AM todos os dias. |
| `children.state` | Uma string contendo o estado do agendamento. Os dois estados compatíveis são &quot;ativos&quot; e &quot;inativos&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

## Criar um novo agendamento {#create}

Você pode criar um novo agendamento fazendo uma solicitação POST para o `/config/schedules` endpoint .

**Formato da API**

```http
POST /config/schedules
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| Propriedade | Descrição |
| -------- | ------------ |
| `name` | **Obrigatório.** O nome do agendamento como uma string. |
| `type` | **Obrigatório.** O tipo de trabalho como uma string. Os dois tipos compatíveis são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `properties` | **Obrigatório.** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **Obrigatório quando `type` é igual a &quot;batch_segmentation&quot;.** Usando `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | *Opcional.* Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações de cron, leia o apêndice no [formato de expressão cron](#appendix). Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado às 1:00 AM todos os dias. <br><br>Se essa sequência de caracteres não for fornecida, um agendamento gerado pelo sistema será gerado automaticamente. |
| `state` | *Opcional.* Uma string contendo o estado do agendamento. Os dois estados compatíveis são &quot;ativos&quot; e &quot;inativos&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do agendamento recém-criado.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## Recuperar uma programação específica {#get}

Você pode recuperar informações detalhadas sobre uma programação específica fazendo uma solicitação do GET para a `/config/schedules` endpoint e fornecer a ID do agendamento que deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que deseja recuperar. |

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o agendamento especificado.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

| Propriedade | Descrição |
| -------- | ------------ |
| `name` | O nome do agendamento como uma string. |
| `type` | O tipo de trabalho como uma string. Os dois tipos compatíveis são `batch_segmentation` e `export`. |
| `properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | Usando `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre programações de cron, leia o apêndice no [formato de expressão cron](#appendix). Neste exemplo, &quot;0 0 1 * *&quot; significa que este agendamento será executado às 1:00 AM todos os dias. |
| `state` | Uma string contendo o estado do agendamento. Os dois estados compatíveis são `active` e `inactive`. Por padrão, o estado é definido como `inactive`. |

## Atualizar detalhes de um agendamento específico {#update}

Você pode atualizar um agendamento específico fazendo uma solicitação de PATCH para o `/config/schedules` endpoint e fornecendo a ID do agendamento que você está tentando atualizar no caminho da solicitação.

A solicitação do PATCH permite atualizar a variável [state](#update-state) ou [programação do cron](#update-schedule) para um agendamento individual.

### Atualizar estado da agenda {#update-state}

Você pode usar uma operação Patch JSON para atualizar o estado do agendamento. Para atualizar o estado, você declara a variável `path` propriedade como `/state` e defina a `value` para `active` ou `inactive`. Para obter mais informações sobre o Patch JSON, leia o [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentação.

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que deseja atualizar. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op": "add",
        "path": "/state",
        "value": "active"
    }
]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado do agendamento, é necessário definir o valor de `path` para &quot;/state&quot;. |
| `value` | O valor atualizado do estado do agendamento. Esse valor pode ser definido como &quot;ativo&quot; ou &quot;inativo&quot; para ativar ou desativar o agendamento. Observe que você **cannot** desative uma programação se a Organização IMS tiver sido habilitada para transmissão. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

### Atualizar programação do cron {#update-schedule}

Você pode usar uma operação de Patch JSON para atualizar o agendamento do cron. Para atualizar o agendamento, declare o `path` propriedade como `/schedule` e defina a `value` para uma programação cron válida. Para obter mais informações sobre o Patch JSON, leia o [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) documentação. Para obter mais informações sobre programações de cron, leia o apêndice no [formato de expressão cron](#appendix).

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que deseja atualizar. |

**Solicitação**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja atualizar. Nesse caso, como você está atualizando o cronograma do cron, é necessário definir o valor de `path` para `/schedule`. |
| `value` | O valor atualizado da programação do cron. Esse valor precisa estar no formato de um cronograma de execução. Neste exemplo, o agendamento será executado no segundo de cada mês. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Excluir uma programação específica

Você pode solicitar a exclusão de uma programação específica fazendo uma solicitação de DELETE para a variável `/config/schedules` endpoint e fornecer a ID do agendamento que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O `id` valor do agendamento que deseja excluir. |

**Solicitação**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Próximas etapas

Após a leitura deste guia, você tem uma melhor compreensão de como as programações funcionam.

## Apêndice {#appendix}

O apêndice a seguir explica o formato de expressões cron usadas em programações.

### Formato

Uma expressão cron é uma string composta de 6 ou 7 campos. A expressão seria semelhante ao seguinte:

`0 0 12 * * ?`

Em uma string de expressão cron, o primeiro campo representa os segundos, o segundo campo representa os minutos, o terceiro campo representa as horas, o quarto campo representa o dia do mês, o quinto campo representa o mês e o sexto campo representa o dia da semana. Opcionalmente, também é possível incluir um sétimo campo, que representa o ano.

| Nome do campo | Obrigatório | Valores possíveis | Caracteres especiais permitidos |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Sim | 0-59 | `, - * /` |
| Minutes | Sim | 0-59 | `, - * /` |
| Horas | Sim | 0-23 | `, - * /` |
| Dia do mês | Sim | 1-31 | `, - * ? / L W` |
| Mês | Sim | 1-12, JAN-DEC | `, - * /` |
| Dia da semana | Sim | 1-7, SUN-SAT | `, - * ? / L #` |
| Ano | Não | Empty, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Os nomes dos meses e dos dias da semana são **not** diferencia maiúsculas de minúsculas. Por conseguinte, `SUN` é equivalente a usar `sun`.

Os caracteres especiais permitidos representam os seguintes significados:

| Caractere especial | Descrição |
| ----------------- | ----------- |
| `*` | Esse valor é usado para selecionar **all** em um campo. Por exemplo, colocar `*` no campo de horas significaria **each** hora. |
| `?` | Esse valor significa que nenhum valor específico é necessário. Isso geralmente é usado para especificar algo em um campo onde o caractere é permitido, mas não o especifica no outro. Por exemplo, se você quiser que um evento seja acionado a cada três dias do mês, mas não se preocupe com o dia da semana, você colocará `3` no campo dia do mês e `?` no campo dia da semana . |
| `-` | Esse valor é usado para especificar **inclusivo** intervalos para o campo. Por exemplo, se você colocar `9-15` no campo de horas, isso significaria que as horas incluiriam 9, 10, 11, 12, 13, 14 e 15. |
| `,` | Esse valor é usado para especificar valores adicionais. Por exemplo, se você colocar `MON, FRI, SAT` no campo dia da semana , isso significa que os dias da semana incluiriam segunda, sexta e sábado. |
| `/` | Esse valor é usado para especificar incrementos. O valor colocado antes da variável `/` determina de onde ele é incrementado, enquanto o valor colocado após a variável `/` determina o quanto é incrementado pelo. Por exemplo, se você colocar `1/7` no campo minutos, isso significaria que os minutos incluiriam 1, 8, 15, 22, 29, 36, 43, 50 e 57. |
| `L` | Esse valor é usado para especificar `Last`e tem um significado diferente, dependendo do campo em que é usado. Se for usado com o campo do dia do mês , representa o último dia do mês. Se for usado com o campo day of the week , ele representa o último dia da semana, que é sábado (`SAT`). Se for usado com o campo do dia da semana , juntamente com outro valor, representa o último dia desse tipo para o mês. Por exemplo, se você colocar `5L` no campo do dia da semana, ele **only** incluir a última sexta-feira do mês. |
| `W` | Esse valor é usado para especificar o dia da semana mais próximo do dia especificado. Por exemplo, se você colocar `18W` no campo do dia do mês, e o dia 18 daquele mês era um sábado, ele disparava na sexta-feira 17, que é o dia da semana mais próximo. Se o dia 18 desse mês fosse um domingo, ele acionaria na segunda-feira, 19, que é o dia da semana mais próximo. Observe que, se você colocar `1W` no campo dia do mês, e o dia da semana mais próximo estaria no mês anterior, o evento ainda será acionado no dia da semana mais próximo do **atual** mês.</br></br>Além disso, você pode combinar `L` e `W` para `LW`, que especificaria o último dia da semana do mês. |
| `#` | Esse valor é usado para especificar o nono dia da semana em um mês. O valor colocado antes da variável `#` representa o dia da semana, enquanto o valor colocado após a `#` representa qual ocorrência no mês. Por exemplo, se você colocar `1#3`, o evento seria acionado no terceiro domingo do mês. Observe que, se você colocar `X#5` e não há a quinta ocorrência desse dia da semana nesse mês, o evento irá **not** ser acionado. Por exemplo, se você colocar `1#5`e não há quinto domingo naquele mês, o evento vai **not** ser acionado. |

### Exemplos

A tabela a seguir mostra amostras de sequências de expressão cron e explica o que significam.

| Expressão | Explicação |
| ---------- | ----------- |
| `0 0 13 * * ?` | O evento será acionado às 1 P.M. todos os dias. |
| `0 30 9 * * ? 2022` | O evento será acionado todos os dias às 9h30 do ano de 2022. |
| `0 * 18 * * ?` | O evento será disparado a cada minuto, começando às 6 e terminando às 6:59 PM, todos os dias. |
| `0 0/10 17 * * ?` | O evento será acionado a cada 10 minutos, começando às 17:00 e terminando às 6:00 PM, todos os dias. |
| `0 13,38 5 ? 6 WED` | O evento será disparado às 5:13AM e às 5:38AM todas as quartas-feiras de junho. |
| `0 30 12 ? * 4#3` | O evento será disparado às 12h30 na terceira quarta-feira, todo mês. |
| `0 30 12 ? * 6L` | O evento será disparado às 12h30 na última sexta-feira de cada mês. |
| `0 45 11 ? * MON-THU` | O evento será disparado às 11h45 todas as segundas-feiras, terças-feiras, quartas e quintas-feiras. |