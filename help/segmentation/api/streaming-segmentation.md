---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation Service;streaming segmentation;Streaming segmentation;Streaming segmentation;Continuous assessment;
solution: Experience Platform
title: Segmentação em streaming
topic: developer guide
description: Este documento contém exemplos de como usar a segmentação de fluxo com a API de segmentação de fluxo.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 1%

---


# Avalie os eventos em tempo quase real com a segmentação contínua

>[!NOTE]
>
>O documento a seguir indica como usar a segmentação de fluxo contínuo usando a API. Para obter informações sobre como usar a segmentação de streaming usando a interface do usuário, leia o [guia da interface de segmentação de streaming](../ui/streaming-segmentation.md).

A segmentação contínua em [!DNL Adobe Experience Platform] permite que os clientes façam a segmentação em tempo quase real, enquanto se concentram na riqueza de dados. Com a segmentação de fluxo contínuo, a qualificação de segmentos agora acontece à medida que os dados de streaming chegam [!DNL Platform], diminuindo a necessidade de programar e executar trabalhos de segmentação. Com esse recurso, a maioria das regras de segmento pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação de segmento será mantida atualizada sem executar trabalhos de segmentação programados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>A segmentação de fluxo só pode ser usada para avaliar dados que são transmitidos para a Plataforma. Em outras palavras, os dados ingeridos por meio da ingestão em lote não serão avaliados por meio da segmentação em streaming e serão avaliados juntamente com o trabalho segmentado agendado à noite.

## Introdução

Este guia do desenvolvedor requer um entendimento prático dos vários [!DNL Adobe Experience Platform] serviços envolvidos com a segmentação de streaming. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado do consumidor em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Segmentation]](../home.md): Fornece a capacidade de criar segmentos e audiências a partir de seus  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para [!DNL Platform] APIs.

### Lendo chamadas de exemplo da API

Este guia do desenvolvedor fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Cabeçalhos adicionais podem ser necessários para concluir solicitações específicas. Os cabeçalhos corretos são mostrados em cada um dos exemplos dentro desse documento. Preste especial atenção às solicitações de amostra para garantir que todos os cabeçalhos obrigatórios sejam incluídos.

### Tipos de query com segmentação de fluxo ativada {#streaming-segmentation-query-types}

>[!NOTE]
>
>Será necessário ativar a segmentação programada para a organização para que a segmentação de fluxo funcione. Informações sobre como ativar a segmentação programada podem ser encontradas na seção [ativar segmentação programada](#enable-scheduled-segmentation)

Para que um segmento seja avaliado usando a segmentação de fluxo contínuo, o query deve estar em conformidade com as diretrizes a seguir.

| Tipo de query | Detalhes |
| ---------- | ------- |
| Ocorrência recebida | Qualquer definição de segmento que se refere a um único evento recebido sem nenhuma restrição de tempo. |
| Ocorrência recebida dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento recebido. |
| Somente perfil | Qualquer definição de segmento que se refere somente a um atributo de perfil. |
| Ocorrência recebida que se refere a um perfil | Qualquer definição de segmento que se refere a um único evento recebido, sem restrição de tempo, e um ou mais atributos de perfil. |
| Ocorrência recebida que se refere a um perfil dentro de uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento recebido e um ou mais atributos do perfil. |
| Vários eventos que se referem a um perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. |

Uma definição de segmento **não** será ativada para a segmentação de streaming nos seguintes cenários:

- A definição do segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição do segmento inclui várias entidades (query de várias entidades).

Além disso, algumas diretrizes se aplicam ao fazer a segmentação de streaming:

| Tipo de query | Orientação |
| ---------- | -------- |
| Query de evento único | Não há limites para a janela de pesquisa. |
| Query com histórico de eventos | <ul><li>A janela de pesquisa é limitada a **um dia**.</li><li>Há uma condição de ordem de tempo estrita **must** entre os eventos.</li><li>Query com pelo menos um evento negado são suportados. No entanto, todo o evento **não pode** ser uma negação.</li></ul> |

## Recuperar todos os segmentos habilitados para a segmentação em streaming

Você pode recuperar uma lista de todos os seus segmentos que estão habilitados para a segmentação de fluxo contínuo dentro da organização IMS, fazendo uma solicitação de GET para o terminal `/segment/definitions`.

**Formato da API**

Para recuperar segmentos habilitados para streaming, você deve incluir o parâmetro de query `evaluationInfo.continuous.enabled=true` no caminho da solicitação.

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

Uma resposta bem-sucedida retorna uma matriz de segmentos na organização IMS que estão habilitados para a segmentação em streaming.

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

## Criar um segmento habilitado para streaming

Um segmento será automaticamente habilitado para streaming se corresponder a um dos [tipos de segmentação de streaming listados acima](#streaming-segmentation-query-types).

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

Uma resposta bem-sucedida retorna os detalhes da definição de segmento habilitada para streaming recém-criada.

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

Depois que a avaliação de streaming estiver ativada, uma linha de base deverá ser criada (após a qual o segmento sempre estará atualizado). A avaliação agendada (também conhecida como segmentação agendada) deve ser ativada primeiro para que o sistema execute automaticamente a definição de linha de base. Com a segmentação programada, sua Organização IMS pode seguir uma programação recorrente para executar automaticamente as tarefas de exportação para avaliar segmentos.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de caixa de proteção, você não poderá usar a avaliação programada.

### Criar um agendamento

Ao fazer uma solicitação POST para o terminal `/config/schedules`, você pode criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

**Formato da API**

```http
POST /config/schedules
```

**Solicitação**

A solicitação a seguir cria uma nova programação com base nas especificações fornecidas na carga.

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
| `name` | **(Obrigatório)** O nome do agendamento. Deve ser uma string. |
| `type` | **(Obrigatório)** O tipo de trabalho no formato de string. Os tipos suportados são `batch_segmentation` e `export`. |
| `properties` | **(Obrigatório)** Um objeto que contém propriedades adicionais relacionadas à programação. |
| `properties.segments` | **(Obrigatório quando  `type` igual  `batch_segmentation`)** Usar  `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | **(Obrigatório)** Uma string que contém a programação da tarefa. As ordens de produção só podem ser programadas para execução uma vez por dia, o que significa que você não pode programar uma ordem de produção para execução mais de uma vez durante um período de 24 horas. O exemplo mostrado (`0 0 1 * * ?`) significa que o trabalho é acionado todos os dias às 13:00:00 UTC. Para obter mais informações, consulte a documentação [cron expressão format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). |
| `state` | *(Opcional)* String que contém o estado da programação. Valores disponíveis: `active` e `inactive`. O valor padrão é `inactive`. Uma organização IMS só pode criar uma programação. As etapas para atualizar o agendamento estão disponíveis posteriormente neste tutorial. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da programação recém-criada.

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

### Ativar um agendamento

Por padrão, uma programação fica inativa quando criada, a menos que a propriedade `state` esteja definida como `active` no corpo da solicitação create (POST). Você pode habilitar um agendamento (defina `state` como `active`), fazendo uma solicitação de PATCH para o terminal `/config/schedules` e incluindo a ID do agendamento no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa [formatação de Patch JSON](http://jsonpatch.com/) para atualizar `state` do agendamento para `active`.

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

A mesma operação pode ser usada para desativar uma programação substituindo o &quot;valor&quot; na solicitação anterior por &quot;inativo&quot;.

## Próximas etapas

Agora que você habilitou segmentos novos e existentes para a segmentação de fluxo contínuo e habilitou a segmentação programada para desenvolver uma linha de base e realizar avaliações recorrentes, você pode começar a criar segmentos para sua organização.

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [Guia do usuário do Construtor de segmentos](../ui/segment-builder.md).