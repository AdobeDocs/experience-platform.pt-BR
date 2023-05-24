---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Serviço de segmentação;segmentação por transmissão;Segmentação por transmissão;Avaliação contínua;
solution: Experience Platform
title: Avaliar eventos em tempo quase real com a segmentação de transmissão
description: Este documento contém exemplos sobre como usar a segmentação por transmissão com a API do Serviço de segmentação do Adobe Experience Platform.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 2%

---

# Avaliar eventos em tempo quase real com a segmentação de transmissão

>[!NOTE]
>
>O documento a seguir declara como usar a segmentação por transmissão usando a API. Para obter informações sobre como usar a segmentação por transmissão usando a interface do, leia o [guia da interface de segmentação por transmissão](../ui/streaming-segmentation.md).

Segmentação de transmissão ativada [!DNL Adobe Experience Platform] O permite que os clientes façam a segmentação em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação por transmissão, a qualificação de segmentos agora acontece à medida que os dados de transmissão chegam ao [!DNL Platform], reduzindo a necessidade de agendar e executar trabalhos de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação do segmento será mantida atualizada sem executar trabalhos de segmentação programados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os segmentos assimilados usando uma origem em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão.
>
>Além disso, os segmentos avaliados com segmentação por transmissão podem variar entre a associação ideal e real se o segmento se basear em outro segmento avaliado usando segmentação em lote. Por exemplo, se o Segmento A se basear no Segmento B, e o Segmento B for avaliado usando a segmentação em lote, já que o Segmento B é atualizado apenas a cada 24 horas, o Segmento A se afastará dos dados reais até ressincronizar com a atualização do Segmento B.

## Introdução

Este guia do desenvolvedor requer uma compreensão funcional dos vários [!DNL Adobe Experience Platform] serviços envolvidos com a segmentação por transmissão. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de várias fontes.
- [[!DNL Segmentation]](../home.md): oferece a capacidade de criar segmentos e públicos-alvo a partir do [!DNL Real-Time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Platform] APIs.

### Leitura de chamadas de API de amostra

Este guia do desenvolvedor fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Cabeçalhos adicionais podem ser necessários para concluir solicitações específicas. Os cabeçalhos corretos são mostrados em cada um dos exemplos deste documento. Preste atenção especial às solicitações de amostra para garantir que todos os cabeçalhos necessários sejam incluídos.

### Tipos de consulta habilitados para segmentação de transmissão {#query-types}

>[!NOTE]
>
>Você precisará ativar a segmentação programada para a organização para que a segmentação por transmissão funcione. Informações sobre como ativar a segmentação agendada podem ser encontradas no [ativar seção de segmentação programada](#enable-scheduled-segmentation)

Para que um segmento seja avaliado usando a segmentação por transmissão, o query deve estar em conformidade com as diretrizes a seguir.

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Evento único | Qualquer definição de segmento que se refere a um único evento recebido sem restrição de tempo. |
| Evento único em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada. |
| Evento único com uma janela de tempo | Qualquer definição de segmento que se refere a um único evento recebido com uma janela de tempo. |
| Somente perfil | Qualquer definição de segmento que se refere apenas a um atributo de perfil. |
| Evento único com um atributo de perfil | Qualquer definição de segmento que se refere a um único evento recebido, sem restrição de tempo e um ou mais atributos de perfil. **Nota:** A query é avaliada imediatamente quando o evento chega. No caso de um evento de perfil, no entanto, ele deve aguardar 24 horas para ser incorporado. |
| Evento único com um atributo de perfil em uma janela de tempo relativa | Qualquer definição de segmento que se refere a um único evento de entrada e um ou mais atributos de perfil. |
| Segmento de segmentos | Qualquer definição de segmento que contenha um ou mais segmentos em lote ou de fluxo. **Nota:** Se um segmento de segmentos for usado, ocorrerá a desqualificação do perfil **a cada 24 horas**. |
| Vários eventos com um atributo de perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) têm um ou mais atributos de perfil. |

Uma definição de segmento **não** ser ativado para segmentação por transmissão nos seguintes cenários:

- A definição do segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição do segmento inclui várias entidades (consultas de várias entidades).
- A definição de segmento inclui uma combinação de um único evento e uma `inSegment` evento.
   - No entanto, se o segmento contido na variável `inSegment` evento é somente perfil, a definição do segmento **irá** ser ativado para segmentação por transmissão.

Observe que as seguintes diretrizes se aplicam ao fazer a segmentação por transmissão:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Consulta de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de pesquisa está limitada a **um dia**.</li><li>Uma condição de ordenação de tempo estrita **deve** existe entre os eventos.</li><li>Há suporte para consultas com pelo menos um evento negado. No entanto, todo o evento **não é possível** seja uma negação.</li></ul> |

Se uma definição de segmento for modificada para não atender mais aos critérios de segmentação por transmissão, a definição de segmento mudará automaticamente de &quot;Transmissão&quot; para &quot;Lote&quot;.

Além disso, a desqualificação de segmentos, semelhante à qualificação de segmentos, acontece em tempo real. Como resultado, se um público-alvo não se qualificar mais para um segmento, ele será imediatamente desqualificado. Por exemplo, se a definição do segmento solicitar &quot;Todos os usuários que compraram sapatos vermelhos nas últimas três horas&quot;, após três horas, todos os perfis que se qualificaram inicialmente para a definição do segmento serão desqualificados.

## Recuperar todos os segmentos ativados para segmentação por transmissão

Você pode recuperar uma lista de todos os segmentos que estão ativados para segmentação por transmissão na organização fazendo uma solicitação GET para o `/segment/definitions` terminal.

**Formato da API**

Para recuperar segmentos habilitados para streaming, você deve incluir o parâmetro de consulta `evaluationInfo.continuous.enabled=true` no caminho da solicitação.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma matriz de segmentos em sua organização que estão habilitados para segmentação por transmissão.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Um segmento será ativado automaticamente para transmissão se corresponder a um dos [tipos de segmentação de transmissão listados acima](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

>[!NOTE]
>
>Esta é uma solicitação padrão de &quot;criar um segmento&quot;. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criação de um segmento](../tutorials/create-a-segment.md).

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento habilitado para streaming recém-criada.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
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

## Ativar avaliação programada {#enable-scheduled-segmentation}

Quando a avaliação de transmissão tiver sido habilitada, uma linha de base deverá ser criada (depois disso, o segmento sempre estará atualizado). A avaliação programada (também conhecida como segmentação programada) deve ser ativada primeiro para que o sistema execute automaticamente a linha de base. Com a segmentação programada, sua organização pode seguir uma programação recorrente para executar automaticamente trabalhos de exportação para avaliar segmentos.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para sandboxes com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, não será possível usar a avaliação programada.

### Criar um agendamento

Ao fazer uma solicitação POST para o `/config/schedules` você pode criar um agendamento e incluir a hora específica em que o agendamento deve ser acionado.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **(Obrigatório)** O nome da programação. Deve ser uma sequência de caracteres. |
| `type` | **(Obrigatório)** O tipo de processo em formato de sequência. Os tipos compatíveis são `batch_segmentation` e `export`. |
| `properties` | **(Obrigatório)** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **(Obrigatório quando `type` igual a `batch_segmentation`)** Usar `["*"]` A garante que todos os segmentos sejam incluídos. |
| `schedule` | **(Obrigatório)** Uma string contendo o agendamento do job. As ordens de produção só podem ser programadas para serem executadas uma vez por dia, o que significa que não é possível programar uma ordem de produção para ser executada mais de uma vez durante um período de 24 horas. O exemplo mostrado (`0 0 1 * * ?`) significa que a tarefa é acionada todos os dias às 1:00:00 UTC Para obter mais informações, consulte o apêndice na [formato de expressão do cron](./schedules.md#appendix) na documentação sobre agendamentos na segmentação. |
| `state` | *(Opcional)* Sequência de caracteres contendo o estado do agendamento. Valores disponíveis: `active` e `inactive`. O valor padrão é `inactive`. Uma organização só pode criar um agendamento. As etapas para atualizar o agendamento estão disponíveis posteriormente neste tutorial. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do agendamento recém-criado.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### Ativar um agendamento

Por padrão, um agendamento fica inativo quando criado, a menos que `state` propriedade está definida como `active` no corpo da solicitação create (POST). Você pode habilitar um agendamento (defina o `state` para `active`) fazendo um pedido PATCH ao `/config/schedules` e incluindo a ID do agendamento no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa [Formatação de patch de JSON](https://datatracker.ietf.org/doc/html/rfc6902) para atualizar a `state` da programação para `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Uma atualização bem-sucedida retorna um corpo de resposta vazio e um Status HTTP 204 (Sem conteúdo).

A mesma operação pode ser usada para desativar um agendamento substituindo o &quot;valor&quot; na solicitação anterior por &quot;inativo&quot;.

## Próximas etapas

Agora que você ativou segmentos novos e existentes para segmentação por transmissão e ativou a segmentação programada para desenvolver uma linha de base e executar avaliações recorrentes, é possível começar a criar segmentos com transmissão ativada para sua organização.

Para saber como executar ações semelhantes e trabalhar com segmentos usando a interface do usuário do Adobe Experience Platform, visite o [Guia do usuário do Construtor de segmentos](../ui/segment-builder.md).

## Apêndice

A seção a seguir lista as perguntas frequentes relacionadas à segmentação de transmissão:

### A &quot;desqualificação&quot; da segmentação por transmissão também ocorre em tempo real?

Para a maioria das instâncias, a desqualificação da segmentação por transmissão ocorre em tempo real. No entanto, os segmentos de transmissão que usam segmentos de segmentos não **não** desqualificar em tempo real, em vez de desqualificar após 24 horas.

### Em quais dados a segmentação por transmissão funciona?

A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os segmentos assimilados usando uma origem em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão. Os eventos transmitidos para o sistema com um carimbo de data e hora com mais de 24 horas serão processados na tarefa em lote subsequente.

### Como os segmentos são definidos como segmentação em lote ou por transmissão?

Um segmento é definido como segmentação em lote ou por transmissão com base em uma combinação de tipo de consulta e duração do histórico do evento. Uma lista de quais segmentos serão avaliados como um segmento de transmissão pode ser encontrada na [seção tipos de consulta de segmentação de transmissão](#query-types).

Observe que se um segmento contiver **ambos** um `inSegment` e uma cadeia direta de evento único, não pode se qualificar para segmentação por transmissão. Se quiser que esse segmento se qualifique para a segmentação por transmissão, transforme a cadeia direta de eventos únicos em seu próprio segmento.

### Por que o número de segmentos &quot;total qualificado&quot; continua aumentando, enquanto o número em &quot;Últimos X dias&quot; permanece em zero na seção de detalhes do segmento?

O número total de segmentos qualificados é retirado do trabalho diário de segmentação, que inclui públicos qualificados para segmentos em lote e de fluxo. Esse valor é mostrado para segmentos em lote e de transmissão.

O número abaixo de &quot;Últimos X dias&quot; **somente** inclui públicos qualificados na segmentação por transmissão e **somente** aumenta se você tiver transmitido dados para o sistema e contar para essa definição de transmissão. Este valor é **somente** exibido para segmentos de transmissão. Como resultado, esse valor **maio** exibir como 0 para segmentos em lote.

Como resultado, se você vir que o número em &quot;Últimos X dias&quot; é zero e o gráfico de linhas também está relatando zero, você **não** todos os perfis transmitidos para o sistema que se qualificariam para esse segmento.

### Quanto tempo leva para um segmento ficar disponível?

Leva até uma hora para um segmento estar disponível.
