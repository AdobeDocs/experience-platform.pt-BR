---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Avaliar um segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 2%

---


# Avaliar e acessar os resultados do segmento

Este documento fornece um tutorial para avaliar segmentos e acessar resultados de segmentos usando a API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)segmentação.

## Introdução

Este tutorial requer uma compreensão funcional dos vários serviços de Adobe Experience Platform envolvidos na criação de segmentos de audiência. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [Perfil](../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [Serviço](../home.md)de segmentação de Adobe Experience Platform: Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
- [Caixas de proteção](../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância do Platform em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

### Cabeçalhos obrigatórios

Este tutorial também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito às APIs da Platform. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos no Experience Platform são isolados para caixas de proteção virtuais específicas. As solicitações às APIs da Platform exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção no Platform, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Avaliar um segmento

Depois de desenvolver, testar e salvar sua definição de segmento, você pode avaliar o segmento por meio de avaliação programada ou por demanda.

[A avaliação](#scheduled-evaluation) programada (também conhecida como &quot;segmentação programada&quot;) permite criar uma programação recorrente para executar uma tarefa de exportação em um horário específico, enquanto a avaliação [](#on-demand-evaluation) sob demanda envolve a criação de uma tarefa de segmento para criar a audiência imediatamente. As etapas para cada um são descritas abaixo.

Se você ainda não tiver concluído o tutorial [Criar um segmento usando a API](./create-a-segment.md) de Perfil do cliente em tempo real ou criado uma definição de segmento usando o Construtor [de](../ui/overview.md)segmento, faça isso antes de prosseguir com este tutorial.

## Avaliação programada {#scheduled-evaulation}

Por meio da avaliação programada, sua Organização IMS pode criar uma programação recorrente para executar automaticamente as tarefas de exportação.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para o Perfil individual XDM. Se sua organização tiver mais de cinco políticas de mesclagem para o Perfil individual XDM em um único ambiente de caixa de proteção, você não poderá usar a avaliação programada.

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

### Atualizar a hora agendada

O cronograma pode ser atualizado fazendo uma solicitação PATCH para o `/config/schedules` endpoint e incluindo a ID da programação no caminho.

**Formato da API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitação**

A solicitação a seguir usa a formatação [Patch](http://jsonpatch.com/) JSON para atualizar a expressão [de](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron do agendamento. Neste exemplo, o agendamento agora seria acionado às 10:15:00 UTC.

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
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Resposta**

Uma atualização bem-sucedida retorna um corpo de resposta vazio e o Status HTTP 204 (Sem conteúdo).

## Avaliação a pedido

A avaliação sob demanda permite criar um trabalho de segmento para gerar um segmento de audiência sempre que necessário. Ao contrário da avaliação agendada, isso ocorrerá somente quando solicitado e não é recorrente.

### Criar um trabalho de segmento

Um trabalho de segmento é um processo assíncrono que cria um novo segmento de audiência. Ele faz referência a uma definição de segmento, bem como a quaisquer políticas de mesclagem que controlam como o Perfil de cliente em tempo real mescla atributos sobrepostos em seus fragmentos de perfil. Quando uma tarefa de segmento é concluída com êxito, você pode coletar várias informações sobre o segmento, como quaisquer erros que possam ter ocorrido durante o processamento e o tamanho final da sua audiência.

Você pode criar um novo trabalho de segmento, fazendo uma solicitação POST para o `/segment/jobs` terminal na API do Perfil do cliente em tempo real.

**Formato da API**

```http
POST /segment/jobs
```

**Solicitação**

A solicitação a seguir cria um novo trabalho de segmento com base nas duas definições de segmento fornecidas na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentId` | O identificador de uma definição de segmento a partir da qual criar a audiência. Pelo menos uma ID de segmento deve ser fornecida na matriz de carga. |

**Resposta**

Uma resposta bem-sucedida retorna os detalhes do trabalho de segmento recém-criado, incluindo seu valor `id`, somente leitura, gerado pelo sistema, exclusivo para esse trabalho de segmento.

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `id` | O identificador do novo trabalho de segmento, usado para fins de pesquisa. |
| `status` | O status atual do trabalho de segmento. Será &quot;PROCESSAMENTO&quot; até que o processamento seja concluído, e nesse momento ele se tornará &quot;SUCEDIDO&quot; ou &quot;FALHADO&quot;. |

### Pesquisar o status do trabalho do segmento

Você pode usar o `id` para um trabalho de segmento específico para executar uma solicitação de pesquisa (GET) para visualização do status atual do trabalho.

**Formato da API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | O `id` do trabalho de segmento que você deseja acessar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da tarefa de segmentação e fornecerá informações diferentes dependendo do status atual da tarefa. Você pode repetir a solicitação de pesquisa até que o `status` alcance &quot;SUCEDIDO&quot;, quando você pode exportar o segmento para um conjunto de dados.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentedProfileCounter` | O número total de perfis unidos que se qualificam para o segmento. |
| `segmentedProfileByNamespaceCounter` | Um detalhamento dos perfis que se qualificam para o segmento por código de namespace de identidade. Uma lista de códigos de namespace de identidade pode ser encontrada na visão geral [da namespace de](../../identity-service/namespaces.md)identidade. |

## Interpretar os resultados do segmento

Quando os trabalhos de segmento são executados com êxito, o `segmentMembership` mapa é atualizado para cada perfil incluído no segmento. `segmentMembership` também armazena quaisquer segmentos de audiência pré-avaliados que sejam ingeridos no Platform, permitindo a integração com outras soluções, como o Adobe Audience Manager.

O exemplo a seguir mostra a aparência do `segmentMembership` atributo para cada registro de perfil individual:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `lastQualificationTime` | O carimbo de data e hora quando a asserção de associação de segmento foi feita e o perfil entrou ou saiu do segmento. |
| `status` | O status da participação do segmento como parte da solicitação atual. Deve ser igual a um dos seguintes valores conhecidos: <ul><li>`existing`: A entidade continua a estar no segmento.</li><li>`realized`: A entidade está inserindo o segmento.</li><li>`exited`: A entidade está saindo do segmento.</li></ul> |

## Acessar resultados do segmento

Os resultados de um trabalho de segmento podem ser acessados de uma das duas maneiras: você pode acessar perfis individuais ou exportar uma audiência inteira para um conjunto de dados.

As seções a seguir descrevem essas opções com mais detalhes.

## Procure um perfil

Se você souber o perfil específico que gostaria de acessar, poderá fazê-lo usando a API do Perfil do cliente em tempo real. As etapas completas para acessar perfis individuais estão disponíveis nos dados do Perfil do cliente em tempo real [Acessar usando o tutorial da API](../../profile/api/entities.md) do Perfil.

## Exportar um segmento {#export}

Depois que um trabalho de segmentação for concluído com êxito (o valor do `status` atributo é &quot;SUCEDIDO&quot;), você poderá exportar sua audiência para um conjunto de dados no qual ele possa ser acessado e executado.

As etapas a seguir são necessárias para exportar sua audiência:

- [Criar um conjunto de dados](#create-a-target-dataset) de público alvo - Crie o conjunto de dados para manter membros de audiência.
- [Gerar perfis de audiência no conjunto de dados](#generate-profiles-for-audience-members) - Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- [Monitorar o progresso](#monitor-export-progress) da exportação - Verifique o andamento atual do processo de exportação.
- [Ler dados](#next-steps) de audiência - Recupere os Perfis individuais XDM resultantes que representam os membros da audiência.

### Criar um conjunto de dados de público alvo

Ao exportar uma audiência, um conjunto de dados de público alvo deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o schema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar um segmento, o conjunto de dados deve ser baseado no Schema de União de Perfil individual (`https://ns.adobe.com/xdm/context/profile__union`) do XDM. Um schema união é um schema gerado pelo sistema e somente leitura que agregação os campos de schemas que compartilham a mesma classe, neste caso, que é a classe de Perfil Individual XDM. Para obter mais informações sobre schemas de visualização de união, consulte a seção Perfil do cliente em tempo [real do guia](../../xdm/api/getting-started.md)do desenvolvedor do Registro de Schemas.

Há duas maneiras de criar o conjunto de dados necessário:

- **Uso de APIs:** As etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faz referência ao Schema de União de Perfil individual XDM usando a API de catálogo.
- **Usando a interface do usuário:** Para usar a interface do usuário do Adobe Experience Platform para criar um conjunto de dados que faça referência ao schema da união, siga as etapas no tutorial [da](../ui/overview.md) interface do usuário e retorne a este tutorial para prosseguir com as etapas de [geração de perfis](#generate-xdm-profiles-for-audience-members)da audiência.

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa de [geração de perfis](#generate-xdm-profiles-for-audience-members)audiências.

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome descritivo para o conjunto de dados. |
| `schemaRef.id` | A ID da visualização de união (schema) à qual o conjunto de dados será associado. |
| `fileDescription.persisted` | Um valor booliano que, quando definido como `true`, permite que o conjunto de dados persista na visualização da união. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID exclusiva somente leitura gerada pelo sistema do conjunto de dados recém-criado. Uma ID de conjunto de dados configurada corretamente é necessária para exportar membros da audiência com êxito.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Gerar perfis para membros da audiência

Depois de ter um conjunto de dados que persiste na união, você pode criar um trabalho de exportação para persistir os membros da audiência no conjunto de dados, fazendo uma solicitação POST para o ponto de extremidade na API do Perfil do cliente em tempo real e fornecendo a ID do conjunto de dados e as informações do segmento para os segmentos que você deseja exportar. `/export/jobs`

**Formato da API**

```http
POST /export/jobs
```

**Solicitação**

A solicitação a seguir cria uma nova tarefa de exportação, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita os campos de dados a serem incluídos na exportação somente àqueles fornecidos neste parâmetro. O mesmo parâmetro também está disponível ao criar um segmento, portanto os campos no segmento podem já ter sido filtrados. A omissão desse valor resultará na inclusão de todos os campos nos dados exportados |
| `mergePolicy` | *(Opcional)* Especifica a política de mesclagem para reger os dados exportados. Inclua esse parâmetro quando houver vários segmentos sendo exportados. Se esse valor for omitido, o Serviço de exportação usará a política de mesclagem fornecida pelo segmento. |
| `mergePolicy.id` | A ID da política de mesclagem |
| `mergePolicy.version` | A versão específica da política de mesclagem a ser usada. A omissão desse valor assumirá como padrão a versão mais recente. |
| `filter` | *(Opcional)* Especifica um ou mais dos seguintes filtros a serem aplicados ao segmento antes da exportação: |
| `filter.segments` | *(Opcional)* Especifica os segmentos a serem exportados. A omissão desse valor resultará na exportação de todos os dados de todos os perfis. Aceita uma matriz de objetos de segmento, cada um contendo os seguintes campos: |
| `filter.segments.segmentId` | **(Obrigatório se estiver usando`segments`)** a ID do segmento para perfis a serem exportados. |
| `filter.segments.segmentNs` | *(Opcional)* namespace de segmento para o determinado `segmentID`. |
| `filter.segments.status` | *(Opcional)* Uma matriz de strings que fornece um filtro de status para o `segmentID`. Por padrão, `status` terá o valor `["realized", "existing"]` que representa todos os perfis que se encaixam no segmento no momento atual. Os valores possíveis incluem: `"realized"`, `"existing"`e `"exited"`. |
| `filter.segmentQualificationTime` | *(Opcional)* Filtrar com base no tempo de qualificação do segmento. A hora e/ou a hora de término do start podem ser fornecidas. |
| `filter.segmentQualificationTime.startTime` | *(Opcional)* Hora do start de qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora do start para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Opcional)* Hora de término da qualificação de segmento para uma ID de segmento para um determinado status. Não fornecido, não haverá filtro na hora de término para uma qualificação de ID de segmento. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` | *(Opcional)* Limita os perfis exportados a incluírem apenas os que foram atualizados após esse carimbo de data e hora. O carimbo de data e hora deve ser fornecido no formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` para **perfis**, se fornecido | Inclui todos os perfis unidos nos quais o carimbo de data e hora atualizado unido é maior que o carimbo de data e hora fornecido. Suporta `greater_than` operando. |
| `filter.fromTimestamp` para eventos | Todos os eventos ingeridos após esse carimbo de data e hora serão exportados, correspondendo ao resultado do perfil resultante. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos. |
| `filter.emptyProfiles` | *(Opcional)* Booliano. Perfis podem conter registros de Perfis, registros ExperienceEvent ou ambos. Perfis sem registros de Perfis e somente registros ExperienceEvent são chamados de &quot;emptyProfiles&quot;. Para exportar todos os perfis no repositório de Perfis, incluindo &quot;emptyProfiles&quot;, defina o valor de `emptyProfiles` como `true`. Se `emptyProfiles` estiver definido como `false`, somente perfis com registros de Perfis na loja serão exportados. Por padrão, se `emptyProfiles` o atributo não estiver incluído, somente os perfis que contêm registros de Perfis serão exportados. |
| `additionalFields.eventList` | *(Opcional)* Controla os campos de evento da série de tempo exportados para objetos filhos ou associados, fornecendo uma ou mais das seguintes configurações: |
| `additionalFields.eventList.fields` | Controle os campos a serem exportados. |
| `additionalFields.eventList.filter` | Especifica critérios que limitam os resultados incluídos dos objetos associados. Espera um valor mínimo necessário para exportação, geralmente uma data. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Filtros eventos de séries cronológicas para os que foram ingeridos após o carimbo de data e hora fornecido. Não é o tempo de evento em si, mas o tempo de ingestão dos eventos. |
| `destination` | **(Obrigatório)** Informações de destino para os dados exportados |
| `destination.datasetId` | **(Obrigatório)** A ID do conjunto de dados no qual os dados devem ser exportados. |
| `destination.segmentPerBatch` | *(Opcional)* Um valor booliano que, se não fornecido, assumirá o padrão `false`. Um valor de `false` exporta todas as IDs de segmento para uma única ID de lote. Um valor de `true` exporta uma ID de segmento para uma ID de lote. Observe que a configuração do valor a ser `true` pode afetar o desempenho da exportação em lote. |
| `schema.name` | **(Obrigatório)** O nome do schema associado ao conjunto de dados no qual os dados devem ser exportados. |

**Resposta**

Uma resposta bem-sucedida retorna um conjunto de dados preenchido com perfis qualificados para a última execução concluída do trabalho de segmento. Todos os perfis que anteriormente existiam no conjunto de dados, mas não se qualificavam para o segmento durante a última execução concluída do trabalho de segmento, foram removidos.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Se não `destination.segmentPerBatch` tivesse sido incluído na solicitação (se não estiver presente, o padrão é `false`) ou o valor tiver sido definido como `false`, o `destination` objeto na resposta acima não teria uma `batches` matriz e, em vez disso, incluiria apenas uma `batchId`, como mostrado abaixo. Esse único lote incluiria todas as IDs de segmento, enquanto a resposta acima mostra uma única ID de segmento por ID de lote.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Lista de todos os trabalhos de exportação

Você pode retornar uma lista de todos os trabalhos de exportação para uma Organização IMS específica, executando uma solicitação GET para o `export/jobs` endpoint. A solicitação também suporta os parâmetros de query `limit` e `offset`, como mostrado abaixo.

**Formato da API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propriedade | Descrição |
| -------- | ----------- |
| `limit` | Especifique o número de registros a serem retornados. |
| `offset` | Deslocar a página de resultados a ser retornada pelo número fornecido. |


**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

A resposta inclui um `records` objeto que contém os trabalhos de exportação criados pela Organização IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Monitorar progresso de exportação

Como um trabalho de exportação processa, você pode monitorar seu status fazendo uma solicitação GET para o ponto de extremidade `/export/jobs` e incluindo o da tarefa `id` de exportação no caminho. A tarefa de exportação é concluída assim que o `status` campo retorna o valor &quot;SUCEDIDO&quot;.

**Formato da API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | O `id` da tarefa de exportação que você deseja acessar. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `batchId` | O identificador dos lotes criados a partir de uma exportação bem-sucedida, a ser usado para fins de pesquisa ao ler dados de audiência. |

## Próximas etapas

Quando a exportação for concluída com êxito, seus dados estarão disponíveis no Data Lake, no Experience Platform. Em seguida, você pode usar a API [de acesso a](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dados para acessar os dados usando a API `batchId` associada à exportação. Dependendo do tamanho do segmento, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar a API de acesso a dados para acessar e baixar arquivos em lote, siga o tutorial [de acesso a](../../data-access/tutorials/dataset-data.md)dados.

Você também pode acessar dados de segmento exportados com êxito usando o Serviço de Query do Adobe Experience Platform. Usando a interface do usuário ou RESTful API, o Serviço de Query permite que você grave, valide e execute query em dados dentro do Data Lake.

Para obter mais informações sobre como query dados de audiência, consulte a documentação [do serviço de](../../query-service/home.md)Query.
