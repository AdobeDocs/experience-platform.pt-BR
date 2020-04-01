---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentação em streaming
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Avalie eventos em tempo real com a segmentação de streaming (Beta)

>[!NOTE] A segmentação de fluxo contínuo é um recurso beta e estará disponível mediante solicitação.

A segmentação de fluxo (também conhecida como avaliação contínua do query) é a capacidade de avaliar instantaneamente um cliente assim que um evento entra em um grupo de segmentos específico. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para a Adobe Experience Platform, o que significa que a associação de segmento será mantida atualizada sem executar tarefas de segmentação programadas.

![](../images/api/streaming-segment-evaluation.png)

## Introdução

Este guia do desenvolvedor requer um entendimento prático dos vários serviços da plataforma Adobe Experience envolvidos com a segmentação de streaming. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado do consumidor em tempo real, com base em dados agregados de várias fontes.
- [Segmentação](../home.md): Fornece a capacidade de criar segmentos e audiências a partir dos dados do Perfil do cliente em tempo real.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para APIs de plataforma.

### Lendo chamadas de exemplo da API

Este guia do desenvolvedor fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para APIs de plataforma, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. Todas as solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Cabeçalhos adicionais podem ser necessários para concluir solicitações específicas. Os cabeçalhos corretos são mostrados em cada um dos exemplos dentro desse documento. Preste especial atenção às solicitações de amostra para garantir que todos os cabeçalhos obrigatórios sejam incluídos.

### Tipos de query com segmentação contínua ativada

A tabela a seguir lista os diferentes tipos de query de segmentação e se eles suportam ou não a segmentação em streaming.

| Tipo de Query | query de amostra | Segmentação de transmissão suportada |
| ---------- | ------------ | --------------------------------- |
| Demografia simples | &quot;Dê-me todas as pessoas cujo endereço residencial é no Canadá.&quot; | Compatível |
| eventos série cronológica | &quot;Dê-me todas as pessoas que baixaram o Lightroom.&quot; | Compatível |
| Demográfico e série cronológica | &quot;Dê-me todas as pessoas que moram no Canadá e fizeram um pedido nos últimos 30 dias.&quot; | Compatível |
| Ausência de eventos | &quot;Dê-me todas as pessoas que abandonaram dois carrinhos separados em dois dias.&quot; | Compatível |
| Multientidade | &quot;Dê-me todas as pessoas cujo tipo de direito é &#39;Experienciado&#39;.&quot; | Não suportado |
| Funções avançadas de PQL | &quot;Dê-me todos os perfis que fizeram um pedido na semana passada e inclua o SKU e o Nome de todos os produtos comprados.&quot; | Não suportado |

## Recuperar todos os segmentos ativados de segmentação de streaming

Antes de criar um novo segmento habilitado para streaming ou atualizar um segmento existente para ser habilitado para streaming, verifique se você não está duplicando as informações recuperando uma lista de todos os segmentos habilitados para streaming.

**Formato da API**

Para recuperar segmentos habilitados para streaming, você deve incluir o parâmetro query `evaluationInfo.continuous.enabled=true` no caminho da solicitação.

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

Depois de confirmar que o segmento que você deseja criar ainda não existe, você pode criar um novo segmento habilitado para a segmentação de streaming.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

A solicitação a seguir cria um novo segmento que está com a segmentação de streaming ativada. Note that the `continuous` section is set to `enabled: true`.

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
    }
}'
```

>[!NOTE] Esta é uma solicitação padrão de &quot;criar um segmento&quot;, com o parâmetro adicionado da `continuous` seção sendo definido como `enabled: true`. Para obter mais informações sobre como criar uma definição de segmento, leia a documentação sobre criação [de](../tutorials/create-a-segment.md)segmentos.

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

## Habilitar um segmento existente para a segmentação de streaming

Você pode ativar um segmento existente para a segmentação de fluxo contínuo fornecendo a ID da definição do segmento no caminho de uma solicitação PATCH. Além disso, a carga desta solicitação de PATCH deve incluir todos os detalhes da definição de segmento existente, que pode ser acessada fazendo uma solicitação GET para a definição de segmento em questão.

### Procurar uma definição de segmento existente

Para procurar uma definição de segmento existente, você deve fornecer sua ID no caminho de uma solicitação GET.

**Formato da API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | A ID da definição de segmento que você deseja pesquisar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retornará detalhes da definição de segmento solicitada.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] Para a próxima solicitação, você precisará de todos os detalhes da definição de segmento que foram retornados nessa resposta. Por favor, copie os detalhes desta resposta a ser usada no corpo da próxima solicitação.

### Habilitar o segmento existente para a segmentação de streaming

Agora que você sabe os detalhes do segmento que deseja atualizar, é possível executar uma solicitação PATCH para atualizar o segmento para permitir a segmentação de streaming.

**Formato da API**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Solicitação**

A carga da solicitação a seguir fornece os detalhes da definição do segmento (obtida na etapa [](#look-up-an-existing-segment-definition)anterior) e a atualiza alterando sua `continuous.enabled` propriedade para `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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
    }
}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento recém-atualizada.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Ativar avaliação agendada

Depois que a avaliação de streaming estiver ativada, uma linha de base deverá ser criada (após a qual o segmento sempre estará atualizado). Isso é feito automaticamente pelo sistema, no entanto, a avaliação programada (também conhecida como segmentação programada) deve primeiro ser ativada para que a ativação da linha de base ocorra.

Com a segmentação programada, sua Organização IMS pode criar uma programação recorrente para executar automaticamente as tarefas de exportação para avaliar segmentos.

>[!NOTE] A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para o Perfil individual XDM. Se sua organização tiver mais de cinco políticas de mesclagem para o Perfil individual XDM em um único ambiente de caixa de proteção, você não poderá usar a avaliação programada.

### Criar um agendamento

Ao fazer uma solicitação POST para o `/config/schedules` ponto de extremidade, você pode criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

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
| `properties.segments` | **(Obrigatório quando`type`igual`batch_segmentation`)** Usar `["*"]` garante que todos os segmentos sejam incluídos. |
| `schedule` | **(Obrigatório)** Uma string que contém a programação da tarefa. As ordens de produção só podem ser programadas para execução uma vez por dia, o que significa que você não pode programar uma ordem de produção para execução mais de uma vez durante um período de 24 horas. O exemplo mostrado (`0 0 1 * * ?`) significa que o trabalho é acionado todos os dias às 13:00:00 UTC. Para obter mais informações, consulte a documentação do formato [de expressão](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. |
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

Por padrão, uma programação fica inativa quando criada, a menos que a `state` propriedade esteja definida como `active` no corpo da solicitação de criação (POST). Você pode ativar uma programação (definir como `state` ) fazendo uma solicitação PATCH para o `active``/config/schedules` ponto final e incluindo a ID da programação no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa a formatação [de Patch](http://jsonpatch.com/) JSON para atualizar o conteúdo `state` do agendamento para `active`.

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

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário da plataforma Adobe Experience, visite o guia [do usuário do Construtor de](../ui/overview.md)segmentos.