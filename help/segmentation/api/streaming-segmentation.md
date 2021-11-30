---
keywords: Experience Platform, página inicial, tópicos populares, segmentação, Segmentação, Serviço de segmentação, segmentação por streaming, segmentação por streaming, avaliação contínua;
solution: Experience Platform
title: 'Avaliar eventos em quase tempo real com a segmentação de streaming '
topic-legacy: developer guide
description: Este documento contém exemplos de como usar a segmentação de fluxo com a API do serviço de segmentação da Adobe Experience Platform.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 65ff1c34e12cc93f614c3c93c4e40e53f2bf51ff
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 1%

---

# Avaliar eventos em tempo quase real com a segmentação de fluxo

>[!NOTE]
>
>O documento a seguir explica como usar a segmentação de transmissão usando a API. Para obter informações sobre como usar a segmentação de transmissão usando a interface do usuário, leia o [guia da interface do usuário de segmentação por streaming](../ui/streaming-segmentation.md).

Transmitir a segmentação em [!DNL Adobe Experience Platform] O permite que os clientes façam segmentação quase em tempo real, concentrando-se na riqueza de dados. Com a segmentação por streaming, a qualificação de segmento agora acontece à medida que os dados de streaming chegam [!DNL Platform], aliviando a necessidade de agendar e executar tarefas de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>A segmentação de fluxo só pode ser usada para avaliar dados transmitidos para a Plataforma. Em outras palavras, os dados assimilados por meio da assimilação em lote não serão avaliados por meio da segmentação de fluxo e serão avaliados junto com o trabalho segmentado agendado à noite.

## Introdução

Este guia do desenvolvedor requer uma compreensão funcional das várias [!DNL Adobe Experience Platform] serviços envolvidos com a segmentação de fluxo. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Segmentation]](../home.md): Fornece a capacidade de criar segmentos e públicos-alvo a partir de [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas para o [!DNL Platform] APIs.

### Lendo exemplos de chamadas de API

Este guia do desenvolvedor fornece exemplos de chamadas da API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Cabeçalhos adicionais podem ser necessários para concluir solicitações específicas. Os cabeçalhos corretos são mostrados em cada um dos exemplos neste documento. Preste especial atenção às solicitações de amostra para garantir que todos os cabeçalhos necessários sejam incluídos.

### Tipos de consulta ativados para segmentação de fluxo {#query-types}

>[!NOTE]
>
>Você precisará ativar a segmentação agendada para a organização para que a segmentação de fluxo funcione. É possível encontrar informações sobre como ativar a segmentação agendada na variável [habilitar a seção de segmentação agendada](#enable-scheduled-segmentation)

Para que um segmento seja avaliado usando a segmentação de transmissão, a consulta deve estar em conformidade com as diretrizes a seguir.

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento de entrada sem restrição de tempo. |
| Evento único em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada. |
| Evento único com janela de tempo | Qualquer definição de segmento que se refere a um único evento de entrada com uma janela de tempo. |
| Somente perfil | Qualquer definição de segmento que se refere somente a um atributo de perfil. |
| Evento único com um atributo de perfil | Qualquer definição de segmento que se refere a um único evento de entrada, sem restrição de tempo e um ou mais atributos de perfil. **Observação:** O query é avaliado imediatamente quando o evento ocorre. No entanto, no caso de um evento de perfil, ele deve aguardar 24 horas para ser incorporado. |
| Evento único com um atributo de perfil dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada e um ou mais atributos de perfil. |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou em fluxo. **Observação:** Se um segmento de segmentos for usado, a desativação do perfil ocorrerá **a cada 24 horas**. |
| Vários eventos com um atributo de perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. |

Uma definição de segmento **not** ser habilitado para segmentação de transmissão nos seguintes cenários:

- A definição de segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição de segmento inclui várias entidades (consultas de várias entidades).

Observe que as seguintes diretrizes se aplicam ao fazer a segmentação de fluxo:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Query de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de retrospectiva está limitada a **um dia**.</li><li>Uma condição de ordem de tempo estrita **must** existir entre os eventos.</li><li>Consultas com pelo menos um evento negado são suportadas. No entanto, o evento inteiro **cannot** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada para que não atenda mais aos critérios para a segmentação de transmissão, a definição de segmento mudará automaticamente de &quot;Streaming&quot; para &quot;Lote&quot;.

Além disso, a inqualificação de segmentos, de forma semelhante à qualificação de segmentos, ocorre em tempo real. Como resultado, se um público-alvo não se qualificar mais para um segmento, ele será imediatamente desqualificado. Por exemplo, se a definição de segmento solicitar &quot;Todos os usuários que compraram sapatos vermelhos nas últimas três horas&quot;, após três horas, todos os perfis que inicialmente se qualificaram para a definição do segmento serão não qualificados.

## Recuperar todos os segmentos habilitados para a segmentação de streaming

Você pode recuperar uma lista de todos os seus segmentos ativados para a segmentação de streaming na Organização IMS fazendo uma solicitação GET para a `/segment/definitions` endpoint .

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

Um segmento será ativado automaticamente para transmissão se corresponder a um dos [tipos de segmentação de fluxo listados acima](#query-types).

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
>Esta é uma solicitação padrão de &quot;criar um segmento&quot;. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criação de um segmento](../tutorials/create-a-segment.md).

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
>A avaliação programada pode ser ativada para sandboxes com no máximo cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, você não poderá usar a avaliação agendada.

### Criar um agendamento

Ao fazer uma solicitação de POST para a `/config/schedules` endpoint , é possível criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

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
| `properties.segments` | **(Obrigatório quando `type` igual `batch_segmentation`)** Usando `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | **(Obrigatório)** Uma string que contém a programação de tarefas. As tarefas só podem ser programadas para serem executadas uma vez por dia, o que significa que você não pode programar uma tarefa para ser executada mais de uma vez durante um período de 24 horas. O exemplo mostrado (`0 0 1 * * ?`) significa que o trabalho é acionado todos os dias às 1:00:00 UTC. Para obter mais informações, consulte a [formato de expressão cron](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) documentação. |
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

Por padrão, um agendamento fica inativo ao ser criado, a menos que a variável `state` está definida como `active` no corpo da solicitação de criação (POST). Você pode ativar uma programação (defina a variável `state` para `active`), fazendo uma solicitação de PATCH à `/config/schedules` endpoint e incluindo a ID do agendamento no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa [Formatação de patch JSON](http://jsonpatch.com/) para atualizar o `state` do calendário para `active`.

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

## Apêndice

A seção a seguir lista as perguntas mais frequentes sobre a segmentação de fluxo:

### A &quot;inqualificação&quot; da segmentação por streaming também ocorre em tempo real?

Para a maioria das instâncias, a inqualificação da segmentação de streaming ocorre em tempo real. No entanto, os segmentos de fluxo que usam segmentos de segmentos **not** não se qualificam em tempo real, em vez disso, não se qualificam após 24 horas.

### Em quais dados a segmentação de fluxo funciona?

A segmentação de transmissão funciona em todos os dados assimilados por meio de uma fonte de transmissão. Os segmentos assimilados usando uma fonte baseada em lote serão avaliados à noite, mesmo que se qualifiquem para a segmentação de transmissão.

### Como os segmentos são definidos como segmentação em lote ou streaming?

Um segmento é definido como segmentação em lote ou em fluxo com base em uma combinação de tipo de query e duração do histórico do evento. Uma lista de quais segmentos serão avaliados como um segmento de transmissão pode ser encontrada no [seção de tipos de consulta de segmentação de fluxo](#query-types).

### Um usuário pode definir um segmento como segmentação em lote ou em fluxo?

No momento, o usuário não pode definir se um segmento é avaliado por meio da assimilação em lote ou streaming, pois o sistema determinará automaticamente com qual método o segmento será avaliado.

### Por que o número de segmentos &quot;qualificados totais&quot; continua aumentando enquanto o número em &quot;Últimos X dias&quot; permanece em zero na seção de detalhes do segmento?

O número total de segmentos qualificados é obtido do trabalho de segmentação diário, que inclui públicos-alvo qualificados para segmentos em lote e em fluxo. Esse valor é mostrado para segmentos em lote e streaming.

O número em &quot;Últimos X dias&quot; **only** inclui públicos-alvo qualificados na segmentação de transmissão, e **only** O aumenta se você tiver transmitido dados para o sistema e isso contar para essa definição de transmissão. Este valor é **only** exibido para segmentos de transmissão. Como resultado, esse valor **pode** exibir como 0 para segmentos em lote.

Como resultado, se você perceber que o número em &quot;Últimos X dias&quot; é zero, e o gráfico de linha também está relatando zero, você terá que **not** os perfis eram transmitidos no sistema e se qualificavam para esse segmento.