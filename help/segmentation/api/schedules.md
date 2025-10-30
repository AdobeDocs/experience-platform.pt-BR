---
solution: Experience Platform
title: Endpoint da API de Agendamentos
description: Os cronogramas são uma ferramenta que pode ser usada para executar automaticamente trabalhos de segmentação em lote uma vez por dia.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 3%

---

# Endpoint de agendamentos

Os cronogramas são uma ferramenta que pode ser usada para executar automaticamente trabalhos de segmentação em lote uma vez por dia. Você pode usar o ponto de extremidade `/config/schedules` para recuperar uma lista de agendamentos, criar um novo agendamento, recuperar detalhes de um agendamento específico, atualizar um agendamento específico ou excluir um agendamento específico.

## Introdução

Os pontos de extremidade usados neste guia fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo os cabeçalhos necessários e como ler as chamadas de exemplo da API.

## Recuperar uma lista de agendamentos {#retrieve-list}

Você pode recuperar uma lista de todas as agendas para sua organização fazendo uma solicitação GET para o ponto de extremidade `/config/schedules`.

**Formato da API**

O ponto de extremidade `/config/schedules` dá suporte a vários parâmetros de consulta para ajudar a filtrar os resultados. Embora esses parâmetros sejam opcionais, seu uso é altamente recomendado para ajudar a reduzir a sobrecarga cara. Fazer uma chamada para esse endpoint sem parâmetros recuperará todas as agendas disponíveis para sua organização. Vários parâmetros podem ser incluídos, separados por &quot;E&quot; comercial (`&`).

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**Parâmetros de consulta**

+++ Uma lista de parâmetros de consulta disponíveis.

| Parâmetro | Descrição | Exemplo |
| --------- | ----------- | ------- |
| `start` | Especifica de qual página o deslocamento iniciará. Por padrão, esse valor será 0. | `start=5` |
| `limit` | Especifica o número de agendas retornadas. Por padrão, esse valor será 100. | `limit=20` |

+++

**Solicitação**

A solicitação a seguir recuperará as dez últimas programações publicadas em sua organização.

+++ Uma solicitação de amostra para recuperar uma lista de agendamentos.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com uma lista de agendamentos para a organização especificada como JSON.

>[!NOTE]
>
>A resposta a seguir foi truncada por espaço e mostra apenas o primeiro agendamento retornado.

+++ Um exemplo de resposta ao recuperar uma lista de agendamentos.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
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
| `_page.totalCount` | O número total de agendas retornadas. |
| `_page.pageSize` | O tamanho da página de agendamentos. |
| `children.name` | O nome do agendamento como uma cadeia de caracteres. |
| `children.type` | O tipo de trabalho como uma string. Os dois tipos compatíveis são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `children.properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `children.properties.segments` | Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `children.schedule` | Uma string contendo o agendamento do job. Os jobs só podem ser programados para serem executados uma vez por dia, o que significa que você não pode programar um job para ser executado mais de uma vez durante um período de 24 horas. Para obter mais informações sobre cronogramas cron, leia o apêndice no [formato de expressão cron](#appendix). Neste exemplo, &quot;`0 0 1 * *`&quot; significa que este agendamento será executado às 1:00 AM todos os dias. |
| `children.state` | Uma string que contém o estado do agendamento. Os dois estados compatíveis são &quot;ativo&quot; e &quot;inativo&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

+++

## Criar um novo agendamento {#create}

Você pode criar um novo agendamento fazendo uma solicitação POST para o ponto de extremidade `/config/schedules`.

**Formato da API**

```http
POST /config/schedules
```

**Solicitação**

+++ Um exemplo de solicitação para criar um agendamento. 

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **Obrigatório.** O nome do agendamento como uma cadeia de caracteres. |
| `type` | **Obrigatório.** O tipo de trabalho como uma cadeia de caracteres. Os dois tipos compatíveis são &quot;batch_segmentation&quot; e &quot;export&quot;. |
| `properties` | **Obrigatório.** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **Obrigatório quando `type` é igual a &quot;batch_segmentation&quot;.** usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | *Opcional.* Uma cadeia de caracteres que contém o cronograma do trabalho. Os jobs só podem ser programados para serem executados uma vez por dia, o que significa que você não pode programar um job para ser executado mais de uma vez durante um período de 24 horas. Para obter mais informações sobre cronogramas cron, leia o apêndice no [formato de expressão cron](#appendix). Neste exemplo, &quot;`0 0 1 * *`&quot; significa que este agendamento será executado às 1:00 AM todos os dias. <br><br>Se esta cadeia de caracteres não for fornecida, um agendamento gerado pelo sistema será gerado automaticamente. |
| `state` | *Opcional.* Uma cadeia de caracteres que contém o estado do agendamento. Os dois estados compatíveis são &quot;ativo&quot; e &quot;inativo&quot;. Por padrão, o estado é definido como &quot;inativo&quot;. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes do agendamento recém-criado.

+++ Um exemplo de resposta ao criar um agendamento.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

+++

## Recuperar uma programação específica {#get}

Você pode recuperar informações detalhadas sobre um agendamento específico fazendo uma solicitação GET para o ponto de extremidade `/config/schedules` e fornecendo a ID do agendamento que você deseja recuperar no caminho da solicitação.

**Formato da API**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que você deseja recuperar. |

**Solicitação**

+++ Uma solicitação de amostra para recuperar um agendamento. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o agendamento especificado.

+++ Uma resposta de exemplo ao recuperar um agendamento.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `name` | O nome do agendamento como uma cadeia de caracteres. |
| `type` | O tipo de trabalho como uma string. Os dois tipos suportados são `batch_segmentation` e `export`. |
| `properties` | Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | Uma string contendo o agendamento do job. As ordens de produção só podem ser programadas para serem executadas uma vez por dia, o que significa que não é possível programar uma ordem de produção para ser executada mais de uma vez durante um período de 24 horas. Para obter mais informações sobre cronogramas cron, leia o apêndice no [formato de expressão cron](#appendix). Neste exemplo, &quot;`0 0 1 * *`&quot; significa que este agendamento será executado às 1:00 AM todos os dias. |
| `state` | Uma string que contém o estado do agendamento. Os dois estados com suporte são `active` e `inactive`. Por padrão, o estado é definido como `inactive`. |

+++

## Atualizar detalhes de um agendamento específico {#update}

Você pode atualizar um agendamento específico fazendo uma solicitação PATCH para o ponto de extremidade `/config/schedules` e fornecendo a ID do agendamento que você está tentando atualizar no caminho da solicitação.

A solicitação PATCH permite atualizar o [estado](#update-state) ou o [cron schedule](#update-schedule) para um agendamento individual.

**Formato da API**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que você deseja atualizar. |

>[!BEGINTABS]

>[!TAB Atualizar estado do agendamento]

Você pode usar uma operação de patch de JSON para atualizar o estado da programação. Para atualizar o estado, declare a propriedade `path` como `/state` e defina o `value` como `active` ou `inactive`. Para obter mais informações sobre o Patch JSON, leia a documentação do [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902).

**Solicitação**

+++ Um exemplo de solicitação para atualizar o estado do agendamento.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

+++

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja corrigir. Nesse caso, como você está atualizando o estado do agendamento, é necessário definir o valor de `path` como &quot;/state&quot;. |
| `value` | O valor atualizado do estado do agendamento. Esse valor pode ser definido como &quot;ativo&quot; ou &quot;inativo&quot; para ativar ou desativar o agendamento. Observe que você **não pode** desabilitar um agendamento se a organização tiver sido habilitada para streaming. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

>[!TAB Atualizar cronograma cron]

Você pode usar uma operação de patch de JSON para atualizar a programação cron. Para atualizar o agendamento, declare a propriedade `path` como `/schedule` e defina `value` como um agendamento cron válido. Para obter mais informações sobre o Patch JSON, leia a documentação do [Patch JSON](https://datatracker.ietf.org/doc/html/rfc6902). Para obter mais informações sobre cronogramas cron, leia o apêndice no [formato de expressão cron](#appendix).

>[!ENDTABS]

**Solicitação**

+++ Um exemplo de solicitação para atualizar o agendamento.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `path` | O caminho do valor que você deseja atualizar. Nesse caso, como você está atualizando o agendamento do cron, é necessário definir o valor de `path` como `/schedule`. |
| `value` | O valor atualizado do cronograma cron. Esse valor precisa estar no formato de um cronograma cron. Neste exemplo, a programação será executada no segundo dia de cada mês. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Excluir um agendamento específico

Você pode solicitar a exclusão de um agendamento específico fazendo uma solicitação DELETE para o ponto de extremidade `/config/schedules` e fornecendo a ID do agendamento que deseja excluir no caminho da solicitação.

**Formato da API**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SCHEDULE_ID}` | O valor `id` do agendamento que você deseja excluir. |

**Solicitação**

+++ Um exemplo de solicitação para excluir um agendamento.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 204 (Sem conteúdo).

## Próximas etapas

Depois de ler este guia, você compreenderá melhor como as agendas funcionam.

## Apêndice {#appendix}

O apêndice a seguir explica o formato das expressões cron usadas em agendamentos.

### Formato

Uma expressão cron é uma cadeia de caracteres formada por 6 ou 7 campos. A expressão seria semelhante ao seguinte:

`0 0 12 * * ?`

Em uma sequência de expressão cron, o primeiro campo representa os segundos, o segundo campo representa os minutos, o terceiro campo representa as horas, o quarto campo representa o dia do mês, o quinto campo representa o mês e o sexto campo representa o dia da semana. Opcionalmente, também é possível incluir um sétimo campo, que representa o ano.

| Nome do campo | Obrigatório | Valores possíveis | Caracteres especiais permitidos |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | Sim | 0-59 | `, - * /` |
| Minutes | Sim | 0-59 | `, - * /` |
| Horas | Sim | 0-23 | `, - * /` |
| Dia do mês | Sim | 1-31 | `, - * ? / L W` |
| Month | Sim | 1-12, JAN-DEZ | `, - * /` |
| Dia da semana | Sim | 1-7, SOL-SÁB | `, - * ? / L #` |
| Year | Não | Vazio, 1970-2099 | `, - * /` |

>[!NOTE]
>
>Os nomes dos meses e dos dias da semana **não** diferenciam maiúsculas de minúsculas. Portanto, `SUN` é equivalente a usar `sun`.

Os caracteres especiais permitidos representam os seguintes significados:

| Caractere especial | Descrição |
| ----------------- | ----------- |
| `*` | Este valor é usado para selecionar **todos** valores em um campo. Por exemplo, colocar `*` no campo de horas significaria **a cada** hora. |
| `?` | Esse valor significa que nenhum valor específico é necessário. Isso geralmente é usado para especificar algo em um campo onde o caractere é permitido, mas não especificá-lo no outro. Por exemplo, se você quiser que um evento seja acionado todo dia 3 do mês, mas não se importar com o dia da semana, coloque `3` no campo de dia do mês e `?` no campo de dia da semana. |
| `-` | Este valor é usado para especificar intervalos **inclusivos** para o campo. Por exemplo, se você colocar `9-15` no campo de horas, isso significa que as horas incluiriam 9, 10, 11, 12, 13, 14 e 15. |
| `,` | Este valor é usado para especificar valores adicionais. Por exemplo, se você colocar `MON, FRI, SAT` no campo de dia da semana, isso significa que os dias da semana incluiriam segunda, sexta e sábado. |
| `/` | Esse valor é usado para especificar incrementos. O valor colocado antes de `/` determina de onde ele é incrementado, enquanto o valor colocado depois de `/` determina o quanto ele é incrementado. Por exemplo, se você colocar `1/7` no campo de minutos, isso significa que os minutos incluirão 1, 8, 15, 22, 29, 36, 43, 50 e 57. |
| `L` | Este valor é usado para especificar `Last`, e tem um significado diferente dependendo de qual campo é usado. Se for usado com o campo day of the month, representará o último dia do mês. Se for usado com o campo de dia da semana sozinho, ele representará o último dia da semana, que é sábado (`SAT`). Se for usado com o campo day of the week, juntamente com outro valor, ele representará o último dia desse tipo para o mês. Por exemplo, se você colocar `5L` no campo de dia da semana, **somente** incluirá a última sexta-feira do mês. |
| `W` | Esse valor é usado para especificar o dia da semana mais próximo do dia determinado. Por exemplo, se você colocar `18W` no campo de dia do mês, e o dia 18 daquele mês for um sábado, ele será acionado na sexta-feira 17, que é o dia da semana mais próximo. Se o dia 18 daquele mês fosse um domingo, dispararia na segunda-feira dia 19, que é o dia da semana mais próximo. Observe que se você colocar `1W` no campo de dia do mês, e o dia da semana mais próximo estiver no mês anterior, o evento ainda será acionado no dia da semana mais próximo do mês **atual**.</br></br>Além disso, você pode combinar `L` e `W` para criar `LW`, que especificaria o último dia da semana do mês. |
| `#` | Esse valor é usado para especificar o enésimo dia da semana em um mês. O valor colocado antes de `#` representa o dia da semana, enquanto o valor colocado depois de `#` representa qual ocorrência no mês é. Por exemplo, se você colocar `1#3`, o evento será acionado no terceiro domingo do mês. Observe que se você colocar `X#5` e não houver quinta ocorrência desse dia da semana nesse mês, o evento **não** será acionado. Por exemplo, se você colocar `1#5` e não houver quinto domingo nesse mês, o evento **não** será acionado. |

### Exemplos

A tabela a seguir mostra exemplos de cadeias de caracteres de expressão cron e explica o que elas significam.

| Expressão | Explicação |
| ---------- | ----------- |
| `0 0 13 * * ?` | O evento será disparado às 1 P.M. todos os dias. |
| `0 30 9 * * ? 2022` | O evento será disparado todos os dias às 9:30AM no ano de 2022. |
| `0 * 18 * * ?` | O evento será acionado a cada minuto, começando às 18h e terminando às 6:59PM, todos os dias. |
| `0 0/10 17 * * ?` | O evento será disparado a cada 10 minutos, começando às 17h e terminando às 18h, todos os dias. |
| `0 13,38 5 ? 6 WED` | O evento será disparado às 5:13AM e 5:38AM toda quarta-feira de junho. |
| `0 30 12 ? * 4#3` | O evento será disparado às 12:30PM na terceira quarta-feira todos os meses. |
| `0 30 12 ? * 6L` | O evento será disparado às 12:30PM na última sexta-feira de cada mês. |
| `0 45 11 ? * MON-THU` | O evento será disparado às 11:45AM toda segunda, terça, quarta e quinta. |