---
keywords: Experience Platform, página inicial, tópicos populares, segmentação, Segmentação, Serviço de segmentação, segmentação por streaming, segmentação por streaming, avaliação contínua;
solution: Experience Platform
title: 'Avaliar eventos em quase tempo real com a segmentação de streaming '
topic: guia do desenvolvedor
description: Este documento contém exemplos de como usar a segmentação de fluxo com a API do serviço de segmentação da Adobe Experience Platform.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# Avaliar eventos em tempo quase real com a segmentação de fluxo

>[!NOTE]
>
>O documento a seguir explica como usar a segmentação de transmissão usando a API. Para obter informações sobre como usar a segmentação de transmissão usando a interface do usuário, leia o [guia da interface do usuário de segmentação de transmissão](../ui/streaming-segmentation.md).

A segmentação por streaming em [!DNL Adobe Experience Platform] permite que os clientes façam a segmentação quase em tempo real, concentrando-se na riqueza de dados. Com a segmentação de transmissão, a qualificação de segmento agora acontece à medida que os dados de transmissão chegam [!DNL Platform], o que diminui a necessidade de agendar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>A segmentação de fluxo só pode ser usada para avaliar dados transmitidos para a Plataforma. Em outras palavras, os dados assimilados por meio da assimilação em lote não serão avaliados por meio da segmentação de fluxo e serão avaliados junto com o trabalho segmentado agendado à noite.

## Introdução

Este guia do desenvolvedor requer uma compreensão funcional dos vários serviços [!DNL Adobe Experience Platform] envolvidos com a segmentação de transmissão. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Segmentation]](../home.md): Fornece a capacidade de criar segmentos e públicos-alvo a partir de seus  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs [!DNL Platform].

### Lendo exemplos de chamadas de API

Este guia do desenvolvedor fornece exemplos de chamadas da API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Cabeçalhos adicionais podem ser necessários para concluir solicitações específicas. Os cabeçalhos corretos são mostrados em cada um dos exemplos neste documento. Preste especial atenção às solicitações de amostra para garantir que todos os cabeçalhos necessários sejam incluídos.

### Tipos de query com segmentação de fluxo ativado {#streaming-segmentation-query-types}

>[!NOTE]
>
>Você precisará ativar a segmentação agendada para a organização para que a segmentação de fluxo funcione. As informações sobre como ativar a segmentação agendada podem ser encontradas na seção [ativar segmentação agendada](#enable-scheduled-segmentation)

Para que um segmento seja avaliado usando a segmentação de transmissão, a consulta deve estar em conformidade com as diretrizes a seguir.

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Ocorrência de entrada | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. |
| Ocorrência recebida em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada. |
| Ocorrência recebida com uma janela de tempo | Qualquer definição de segmento que se refere a um único evento de entrada com uma janela de tempo. |
| Somente perfil | Qualquer definição de segmento que se refere somente a um atributo de perfil. |
| Ocorrência recebida que se refere a um perfil | Qualquer definição de segmento que se refere a um único evento de entrada, sem restrição de tempo e um ou mais atributos de perfil. |
| Ocorrência recebida que se refere a um perfil dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada e um ou mais atributos de perfil. |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou em fluxo. |
| Vários eventos que se referem a um perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. |

Uma definição de segmento **não** será ativada para a segmentação de fluxo nos seguintes cenários:

- A definição de segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição de segmento inclui várias entidades (consultas de várias entidades).

Além disso, algumas diretrizes se aplicam ao fazer a segmentação de fluxo:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Query de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de retrospectiva é limitada a **um dia**.</li><li>Uma condição de ordem de tempo estrita **deve** existir entre os eventos.</li><li>Consultas com pelo menos um evento negado são suportadas. No entanto, o evento inteiro **não pode** ser uma negação.</li></ul> |

## Recuperar todos os segmentos habilitados para a segmentação de streaming

Você pode recuperar uma lista de todos os seus segmentos que são ativados para segmentação de fluxo na Organização IMS fazendo uma solicitação GET para o terminal `/segment/definitions`.

**Formato da API**

Para recuperar segmentos ativados para transmissão, você deve incluir o parâmetro de consulta `evaluationInfo.continuous.enabled=true` no caminho da solicitação.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Solicitação**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de segmentos na organização IMS que são ativados para a segmentação de transmissão.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Criar um segmento habilitado para transmissão

Um segmento será ativado automaticamente para transmissão se corresponder a um dos [tipos de segmentação de transmissão listados acima](#streaming-segmentation-query-types).

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>Esta é uma solicitação padrão de &quot;criar um segmento&quot;. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criar um segmento](../tutorials/create-a-segment.md).

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento habilitado para transmissão recém-criada.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Habilitar avaliação agendada {#enable-scheduled-segmentation}

Após habilitar a avaliação do streaming, é necessário criar uma linha de base (após a qual o segmento sempre estará atualizado). A avaliação agendada (também conhecida como segmentação agendada) deve primeiro ser ativada para que o sistema execute automaticamente a definição de linha de base. Com a segmentação agendada, a Organização IMS pode aderir a um agendamento recorrente para executar automaticamente tarefas de exportação para avaliar segmentos.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para sandboxes com no máximo cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, você não poderá usar a avaliação agendada.

### Criar um agendamento

Ao fazer uma solicitação de POST para o endpoint `/config/schedules`, é possível criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

**Formato da API**

```http
POST /config/schedules
```

**Solicitação**

A solicitação a seguir cria um novo agendamento com base nas especificações fornecidas no payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | **(Obrigatório)** O nome da programação. Deve ser uma string. |
| `type` | **(Obrigatório)** O tipo de trabalho no formato de string. Os tipos suportados são `batch_segmentation` e `export`. |
| `properties` | **(Obrigatório)** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **(Obrigatório quando  `type` é igual  `batch_segmentation`)** Usar  `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | **(Obrigatório)** Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. O exemplo mostrado (`0 0 1 * * ?`) significa que o trabalho é acionado todos os dias às 1:00:00 UTC. Para obter mais informações, consulte a documentação [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). |
| `state` | *(Opcional)* Sequência de caracteres contendo o estado da programação. Valores disponíveis: `active` e `inactive`. O valor padrão é `inactive`. Uma Organização IMS só pode criar uma programação. As etapas para atualizar o cronograma estão disponíveis posteriormente neste tutorial. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do agendamento recém-criado.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### Habilitar um agendamento

Por padrão, um agendamento fica inativo quando criado, a menos que a propriedade `state` esteja definida como `active` no corpo da solicitação de criação (POST). Você pode habilitar um agendamento (defina `state` como `active`) fazendo uma solicitação de PATCH para o endpoint `/config/schedules` e incluindo a ID do agendamento no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa [JSON Patch formatting](http://jsonpatch.com/) para atualizar `state` do agendamento para `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Resposta**

Uma atualização bem-sucedida retorna um corpo de resposta vazio e o Status HTTP 204 (Sem conteúdo).

A mesma operação pode ser usada para desabilitar um agendamento, substituindo o &quot;valor&quot; na solicitação anterior por &quot;inativo&quot;.

## Próximas etapas

Agora que você ativou segmentos novos e existentes para a segmentação de streaming e habilitou a segmentação agendada para desenvolver uma linha de base e realizar avaliações recorrentes, você pode começar a criar segmentos ativados para streaming para sua organização.

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [Guia do usuário do Construtor de segmentos](../ui/segment-builder.md).
