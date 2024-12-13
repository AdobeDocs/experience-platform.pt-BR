---
solution: Experience Platform
title: Avaliar eventos em tempo quase real com a segmentação de transmissão
description: Este documento contém exemplos sobre como usar a segmentação por transmissão com a API do Serviço de segmentação do Adobe Experience Platform.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: e6e9abc7ffe27a2ff9c4ccf4ca243cabdae3d631
workflow-type: tm+mt
source-wordcount: '2052'
ht-degree: 4%

---

# Avaliar eventos em tempo quase real com a segmentação de transmissão

>[!NOTE]
>
>O documento a seguir declara como usar a segmentação por transmissão usando a API. Para obter informações sobre como usar a segmentação por transmissão usando a interface, leia o [guia da interface de segmentação por transmissão](../ui/streaming-segmentation.md).

A segmentação por transmissão no [!DNL Adobe Experience Platform] permite que os clientes façam a segmentação em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação por transmissão, a qualificação de segmentos agora acontece à medida que os dados de transmissão chegam ao [!DNL Platform], diminuindo a necessidade de agendar e executar trabalhos de segmentação. Com esse recurso, a maioria das regras de segmento agora pode ser avaliada à medida que os dados são passados para [!DNL Platform], o que significa que a associação do segmento será mantida atualizada sem a execução de trabalhos de segmentação agendados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os segmentos assimilados usando uma origem em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão.
>
>Além disso, as definições de segmento avaliadas com a segmentação por transmissão podem variar entre a associação ideal e real se a definição do segmento se basear em outra definição de segmento que é avaliada usando a segmentação em lote. Por exemplo, se o Segmento A se basear no Segmento B, e o Segmento B for avaliado usando a segmentação em lote, já que o Segmento B é atualizado apenas a cada 24 horas, o Segmento A se afastará dos dados reais até ressincronizar com a atualização do Segmento B.

## Introdução

Este guia do desenvolvedor requer entendimento prático dos vários serviços do [!DNL Adobe Experience Platform] envolvidos na segmentação por transmissão. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real, com base em dados agregados de múltiplas fontes.
- [[!DNL Segmentation]](../home.md): Fornece a capacidade de criar públicos usando definições de segmento e outras fontes externas de seus dados do [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs do [!DNL Platform].

### Leitura de chamadas de API de amostra

Este guia do desenvolvedor fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Cabeçalhos adicionais podem ser necessários para concluir solicitações específicas. Os cabeçalhos corretos são mostrados em cada um dos exemplos deste documento. Preste atenção especial às solicitações de amostra para garantir que todos os cabeçalhos necessários sejam incluídos.

### Tipos de consulta habilitados para segmentação de transmissão {#query-types}

>[!NOTE]
>
>Você precisará ativar a segmentação programada para a organização para que a segmentação por transmissão funcione. Informações sobre como habilitar a segmentação agendada podem ser encontradas na [seção habilitar segmentação agendada](#enable-scheduled-segmentation)

Para que uma definição de segmento seja avaliada usando a segmentação por transmissão, o query deve estar em conformidade com as diretrizes a seguir.

| Tipo de consulta | Detalhes |
| ---------- | ------- |
| Evento único em uma janela de tempo de menos de 24 horas | Qualquer definição de segmento que se refira a um único evento recebido em uma janela de tempo de menos de 24 horas. |
| Somente perfil | Qualquer definição de segmento que se refere apenas a um atributo de perfil. |
| Evento único com um atributo de perfil em uma janela de tempo relativa de menos de 24 horas | Qualquer definição de segmento que se refere a um único evento recebido, com um ou mais atributos de perfil, e ocorre em uma janela de tempo relativa de menos de 24 horas. |
| Segmento de segmentos | Qualquer definição de segmento que contenha uma ou mais definições de segmento de lote ou transmissão. **Observação:** se o segmento de segmentos for usado com definições de segmento do **lote**, a desqualificação de perfil poderá levar **até 24 horas** para ocorrer. Se o segmento de segmentos for usado com **streaming** definições de segmento, a desqualificação de perfil ocorrerá de maneira streaming. |
| Vários eventos com um atributo de perfil | Qualquer definição de segmento que se refere a vários eventos **nas últimas 24 horas** e (opcionalmente) tem um ou mais atributos de perfil. |

Uma definição de segmento **não** será habilitada para segmentação por transmissão nos seguintes cenários:

- A definição do segmento inclui segmentos ou características do Adobe Audience Manager (AAM).
- A definição do segmento inclui várias entidades (consultas de várias entidades).
- A definição de segmento inclui uma combinação de um único evento e um evento `inSegment`.
   - No entanto, se o segmento contido no evento `inSegment` for somente perfil, a definição de segmento **será** habilitada para segmentação por transmissão.
- A definição do segmento usa &quot;Ignorar ano&quot; como parte de suas restrições de tempo.

Observe que as seguintes diretrizes se aplicam ao fazer a segmentação por transmissão:

| Tipo de consulta | Orientação |
| ---------- | -------- |
| Consulta de evento único | Não há limites para a janela de retrospectiva. |
| Consulta com histórico de eventos | <ul><li>A janela de pesquisa é limitada a **um dia**.</li><li>Uma condição estrita de ordenação de tempo **deve** existe entre os eventos.</li><li>Há suporte para consultas com pelo menos um evento negado. No entanto, o evento inteiro **não pode** ser uma negação.</li></ul> |

Se uma definição de segmento for modificada para não atender mais aos critérios de segmentação por transmissão, a definição de segmento mudará automaticamente de &quot;Transmissão&quot; para &quot;Lote&quot;.

Além disso, a desqualificação de segmentos, semelhante à qualificação de segmentos, acontece em tempo real. Como resultado, se um perfil não se qualificar mais para uma definição de segmento, ele será imediatamente desqualificado. Por exemplo, se a definição do segmento solicitar &quot;Todos os usuários que compraram sapatos vermelhos nas últimas três horas&quot;, após três horas, todos os perfis que se qualificaram inicialmente para a definição do segmento serão desqualificados.

## Recuperar todas as definições de segmento habilitadas para segmentação por transmissão

Você pode recuperar uma lista de todas as definições de segmento que estão habilitadas para segmentação por transmissão na organização fazendo uma solicitação GET para o ponto de extremidade `/segment/definitions`.

**Formato da API**

Para recuperar definições de segmento habilitado para streaming, você deve incluir o parâmetro de consulta `evaluationInfo.continuous.enabled=true` no caminho da solicitação.

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

Uma resposta bem-sucedida retorna uma matriz de definições de segmento na organização que estão habilitadas para segmentação por transmissão.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

## Criar uma definição de segmento habilitado para streaming

Uma definição de segmento será habilitada para streaming automaticamente se corresponder a um dos [tipos de segmentação de streaming listados acima](#query-types).

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
>Esta é uma solicitação padrão para &quot;criar uma definição de segmento&quot;. Para obter mais informações sobre como criar uma definição de segmento, leia o tutorial em [criando uma definição de segmento](../tutorials/create-a-segment.md).

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da definição de segmento habilitado para streaming recém-criada.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

Quando a avaliação de transmissão tiver sido habilitada, uma linha de base deverá ser criada (depois disso, a definição do segmento sempre estará atualizada). A avaliação programada (também conhecida como segmentação programada) deve ser ativada primeiro para que o sistema execute automaticamente a linha de base. Com a segmentação programada, sua organização pode seguir uma programação recorrente para executar automaticamente trabalhos de exportação para avaliar as definições de segmento.

>[!NOTE]
>
>A avaliação agendada pode ser habilitada para sandboxes com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, você não poderá usar a avaliação agendada.

### Criar um agendamento

Ao fazer uma solicitação POST para o ponto de extremidade `/config/schedules`, você pode criar um agendamento e incluir a hora específica em que o agendamento deve ser acionado.

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
| `name` | **(Obrigatório)** O nome do agendamento. Deve ser uma sequência de caracteres. |
| `type` | **(Obrigatório)** O tipo de trabalho no formato de cadeia de caracteres. Os tipos suportados são `batch_segmentation` e `export`. |
| `properties` | **(Obrigatório)** Um objeto que contém propriedades adicionais relacionadas ao agendamento. |
| `properties.segments` | **(Obrigatório quando `type` é igual a `batch_segmentation`)** O uso de `["*"]` garante que todas as definições de segmento sejam incluídas. |
| `schedule` | **(Obrigatório)** Uma cadeia de caracteres que contém o agendamento do trabalho. As ordens de produção só podem ser programadas para serem executadas uma vez por dia, o que significa que não é possível programar uma ordem de produção para ser executada mais de uma vez durante um período de 24 horas. O exemplo mostrado (`0 0 1 * * ?`) significa que o trabalho é acionado todos os dias às 1:00:00 UTC. Para obter mais informações, consulte o apêndice sobre o [formato de expressão cron](./schedules.md#appendix) na documentação sobre agendamentos dentro da segmentação. |
| `state` | *(Opcional)* Cadeia de caracteres contendo o estado da agenda. Valores disponíveis: `active` e `inactive`. O valor padrão é `inactive`. Uma organização só pode criar um agendamento. As etapas para atualizar o agendamento estão disponíveis posteriormente neste tutorial. |

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

Por padrão, um agendamento fica inativo quando criado, a menos que a propriedade `state` esteja definida como `active` no corpo da solicitação create (POST). Você pode habilitar um agendamento (definir `state` como `active`) fazendo uma solicitação PATCH para o ponto de extremidade `/config/schedules` e incluindo a ID do agendamento no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa [formatação de patch JSON](https://datatracker.ietf.org/doc/html/rfc6902) para atualizar o `state` do agendamento para `active`.

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

Agora que você ativou definições de segmento novas e existentes para segmentação por transmissão e ativou a segmentação agendada para desenvolver uma linha de base e executar avaliações recorrentes, é possível começar a criar definições de segmento com transmissão ativada para sua organização.

Para saber como executar ações semelhantes e trabalhar com definições de segmento usando a interface do usuário do Adobe Experience Platform, visite o [guia do usuário do Construtor de segmentos](../ui/segment-builder.md).

## Apêndice

A seção a seguir lista as perguntas frequentes relacionadas à segmentação de transmissão:

### A &quot;desqualificação&quot; da segmentação por transmissão também ocorre em tempo real?

Para a maioria das instâncias, a desqualificação da segmentação por transmissão ocorre em tempo real. No entanto, as definições de segmento de transmissão que usam segmentos de segmentos **não** não se qualificam em tempo real, em vez disso, se desqualificam após 24 horas.

### Em quais dados a segmentação por transmissão funciona?

A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os segmentos assimilados usando uma origem em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão. Os eventos transmitidos para o sistema com um carimbo de data e hora com mais de 24 horas serão processados na tarefa em lote subsequente.

### Como as definições de segmento são definidas como segmentação em lote ou por transmissão?

Uma definição de segmento é definida como segmentação em lote ou por transmissão com base em uma combinação de tipo de consulta e duração do histórico de eventos. Uma lista de quais definições de segmento serão avaliadas como um segmento de streaming pode ser encontrada na [seção de tipos de consulta de segmentação de streaming](#query-types).

Observe que se um segmento contiver **ambos** uma expressão `inSegment` e uma cadeia direta de evento único, ele não poderá se qualificar para segmentação por transmissão. Se quiser que essa definição de segmento se qualifique para segmentação por transmissão, você deve tornar a cadeia de evento único direta sua própria definição de segmento.

### Por que o número de definições de segmento &quot;total qualificado&quot; continua aumentando, enquanto o número em &quot;Últimos X dias&quot; permanece em zero na seção de detalhes de definição do segmento?

O número total de definições de segmento qualificado é obtido do trabalho diário de segmentação, que inclui públicos qualificados para definições de segmento em lote e de transmissão. Esse valor é mostrado para definições de segmento em lote e de transmissão.

O número nos &quot;Últimos X dias&quot; **somente** inclui públicos qualificados na segmentação por transmissão e **somente** aumenta se você tiver transmitido dados para o sistema e se contar para essa definição de transmissão. Este valor é **somente** exibido para definições de segmento de transmissão. Como resultado, o valor **maio** é exibido como 0 para definições de segmento em lote.

Como resultado, se você vir que o número em &quot;Últimos X dias&quot; é zero e o gráfico de linhas também está relatando zero, você **não** transmitiu qualquer perfil no sistema que se qualificaria para essa definição de segmento.

### Quanto tempo leva para uma definição de segmento ficar disponível?

Leva até uma hora para uma definição de segmento estar disponível.

### Existem limitações para os dados que estão sendo transmitidos?

Para que os dados transmitidos sejam usados na segmentação por transmissão, **deve** haver um espaçamento entre os eventos transmitidos. Se muitos eventos forem transmitidos no mesmo segundo, a Platform tratará esses eventos como dados gerados pelo bot e eles serão descartados. Como prática recomendada, você deve ter **pelo menos** cinco segundos entre os dados do evento para garantir que os dados sejam usados corretamente.
