---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Endpoint da API de tarefas de privacidade
topic-legacy: developer guide
description: Saiba como gerenciar tarefas de privacidade para aplicativos Experience Cloud usando a API do Privacy Service.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 3%

---

# Ponto de extremidade de tarefas de privacidade

Este documento aborda como trabalhar com tarefas de privacidade usando chamadas de API. Especificamente, abrange a utilização da variável `/job` endpoint no [!DNL Privacy Service] API. Antes de ler este guia, consulte [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo cabeçalhos necessários e como ler chamadas de API de exemplo.

>[!NOTE]
>
>Se você estiver tentando gerenciar solicitações de consentimento ou de recusa dos clientes, consulte o [guia do endpoint de consentimento](./consent.md).

## Listar todas as tarefas {#list}

Você pode exibir uma lista de todos os trabalhos de privacidade disponíveis em sua organização, fazendo uma solicitação do GET para a `/jobs` endpoint .

**Formato da API**

Esse formato de solicitação usa um `regulation` parâmetro de consulta no `/jobs` endpoint, portanto, começa com um ponto de interrogação (`?`) conforme mostrado abaixo. A resposta é paginada, permitindo usar outros parâmetros de consulta (`page` e `size`) para filtrar a resposta. Você pode separar vários parâmetros usando o sinal gráfico (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{REGULATION}` | O tipo de regulamento a ser procurado. Os valores aceitos incluem: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulte a visão geral em [regulamentos compatíveis](../regulations/overview.md) para obter mais informações sobre os regulamentos de privacidade que os valores acima representam. |
| `{PAGE}` | A página de dados a ser exibida, usando a numeração com base em 0. O padrão é `0`. |
| `{SIZE}` | O número de resultados a serem exibidos em cada página. O padrão é `1` e o máximo é `100`. Exceder o máximo faz com que a API retorne um erro de código 400. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera uma lista paginada de todas as tarefas em uma Organização IMS, começando na terceira página com um tamanho de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de tarefas, com cada tarefa contendo detalhes como `jobId`. Neste exemplo, a resposta conteria uma lista de 50 trabalhos, começando na terceira página de resultados.

### Acessar páginas subsequentes

Para obter o próximo conjunto de resultados em uma resposta paginada, você deve fazer outra chamada de API para o mesmo endpoint enquanto aumenta o valor de `page` parâmetro de consulta por 1.

## Criar um trabalho de privacidade {#create-job}

Antes de criar uma nova solicitação de cargo, você deve primeiro coletar informações de identificação sobre os titulares de dados cujos dados deseja acessar, excluir ou recusar a venda. Depois de ter os dados necessários, eles devem ser fornecidos na carga de uma solicitação do POST para a variável `/jobs` endpoint .

>[!NOTE]
>
>Aplicativos Adobe Experience Cloud compatíveis usam valores diferentes para identificar titulares de dados. Consulte o guia sobre [Aplicativos Privacy Service e Experience Cloud](../experience-cloud-apps.md) para obter mais informações sobre identificadores necessários para seus aplicativos. Para obter mais orientações gerais sobre como determinar para quais IDs enviar [!DNL Privacy Service], consulte o documento em [dados de identidade em solicitações de privacidade](../identity-data.md).

O [!DNL Privacy Service] A API suporta dois tipos de solicitações de trabalho para dados pessoais:

* [Acessar e/ou excluir](#access-delete): Acesse (leia) ou exclua dados pessoais.
* [Recusar venda](#opt-out): Marcar dados pessoais como não vendidos.

>[!IMPORTANT]
>
>Embora as solicitações de acesso e exclusão possam ser combinadas como uma única chamada de API, as solicitações de recusa devem ser feitas separadamente.

### Criar um trabalho de acesso/exclusão {#access-delete}

Esta seção demonstra como fazer uma solicitação de acesso/exclusão de trabalho usando a API.

**Formato da API**

```http
POST /jobs
```

**Solicitação**

A solicitação a seguir cria uma nova solicitação de trabalho, configurada pelos atributos fornecidos na carga, conforme descrito abaixo.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `companyContexts` **(Obrigatório)** | Uma matriz contendo informações de autenticação para sua organização. Cada identificador listado inclui os seguintes atributos: <ul><li>`namespace`: O namespace de um identificador.</li><li>`value`: O valor do identificador.</li></ul>É **obrigatório** que um dos identificadores usa `imsOrgId` como `namespace`, com `value` contendo a ID exclusiva para sua organização IMS. <br/><br/>Identificadores adicionais podem ser qualificadores de empresa específicos do produto (por exemplo, `Campaign`), que identificam uma integração com um aplicativo Adobe pertencente à sua organização. Os valores potenciais incluem nomes de conta, códigos de cliente, IDs de locatário ou outros identificadores de aplicativos. |
| `users` **(Obrigatório)** | Uma matriz contendo uma coleção de pelo menos um usuário cujas informações você gostaria de acessar ou excluir. Um máximo de 1000 IDs de usuário pode ser fornecido em uma única solicitação. Cada objeto de usuário contém as seguintes informações: <ul><li>`key`: Um identificador para um usuário que é usado para qualificar as IDs de trabalho separadas nos dados de resposta. É prática recomendada escolher uma string exclusiva e facilmente identificável para esse valor, para que possa ser facilmente referenciada ou pesquisada posteriormente.</li><li>`action`: Uma matriz que lista as ações desejadas para executar nos dados do usuário. Dependendo das ações que deseja realizar, essa matriz deve incluir `access`, `delete`ou ambos.</li><li>`userIDs`: Uma coleção de identidades para o usuário. O número de identidades que um único usuário pode ter é limitado a nove. Cada identidade consiste em um `namespace`, a `value`e um qualificador de namespace (`type`). Consulte a [apêndice](appendix.md) para obter mais detalhes sobre essas propriedades necessárias.</li></ul> Para obter uma explicação mais detalhada do `users` e `userIDs`, consulte o [guia de solução de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Obrigatório)** | Uma matriz de produtos de Adobe para incluir no seu processamento. Se esse valor estiver ausente ou vazio, a solicitação será rejeitada. Inclua somente produtos com os quais sua organização tenha uma integração. Consulte a seção sobre [valores de produto aceitos](appendix.md) no apêndice para mais informações. |
| `expandIDs` | Uma propriedade opcional que, quando definida como `true`, representa uma otimização para o processamento das IDs nos aplicativos (atualmente, há suporte apenas para [!DNL Analytics]). Se for omitido, esse valor assumirá como padrão `false`. |
| `priority` | Uma propriedade opcional usada pelo Adobe Analytics que define a prioridade para o processamento de solicitações. Os valores aceitos são `normal` e `low`. If `priority` for omitido, o comportamento padrão será `normal`. |
| `analyticsDeleteMethod` | Uma propriedade opcional que especifica como o Adobe Analytics deve lidar com os dados pessoais. Dois valores possíveis são aceitos para este atributo: <ul><li>`anonymize`: Todos os dados referenciados pela coleção de IDs de usuário fornecida são tornados anônimos. If `analyticsDeleteMethod` for omitido, esse será o comportamento padrão.</li><li>`purge`: Todos os dados são removidos completamente.</li></ul> |
| `mergePolicyId` | Ao fazer solicitações de privacidade para o Perfil do cliente em tempo real (`profileService`), é possível fornecer a ID do [política de mesclagem](../../profile/merge-policies/overview.md) que você deseja usar na compilação de ID. Ao especificar uma política de mesclagem, as solicitações de privacidade podem incluir informações do segmento ao retornar dados em um cliente. Somente uma política de mesclagem pode ser especificada por solicitação. Se nenhuma política de mesclagem for fornecida, as informações de segmentação não serão incluídas na resposta. |
| `regulation` **(Obrigatório)** | O regulamento para o trabalho de privacidade. Os seguintes valores são aceitos: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consulte a visão geral em [regulamentos compatíveis](../regulations/overview.md) para obter mais informações sobre os regulamentos de privacidade que os valores acima representam. |

{style=&quot;table-layout:auto&quot;}

**Resposta**

Uma resposta bem-sucedida retorna os detalhes dos trabalhos recém-criados.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Propriedade | Descrição |
| --- | --- |
| `jobId` | Uma ID exclusiva gerada pelo sistema e somente leitura para uma tarefa. Esse valor é usado na próxima etapa da pesquisa de um trabalho específico. |

{style=&quot;table-layout:auto&quot;}

Depois de enviar a solicitação de trabalho com sucesso, você pode prosseguir para a próxima etapa de [verificar o status da tarefa](#check-status).

## Verificar o status de um trabalho {#check-status}

Você pode recuperar informações sobre um trabalho específico, como seu status de processamento atual, incluindo o `jobId` no caminho de uma solicitação do GET para o `/jobs` endpoint .

>[!IMPORTANT]
>
>Os dados para trabalhos criados anteriormente só estão disponíveis para recuperação dentro de 30 dias da data de conclusão do trabalho.

**Formato da API**

```http
GET /jobs/{JOB_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{JOB_ID}` | A ID do trabalho que você deseja pesquisar. Esta ID é retornada em `jobId` em respostas de API bem-sucedidas para [criação de uma tarefa](#create-job) e [listar todos os trabalhos](#list). |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir recupera os detalhes da tarefa cuja `jobId` é fornecido no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Resposta**

Uma resposta bem-sucedida retorna os detalhes da tarefa especificada.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propriedade | Descrição |
| --- | --- |
| `productStatusResponse` | Cada objeto dentro da variável `productResponses` A matriz contém informações sobre o status atual da tarefa em relação a um [!DNL Experience Cloud] aplicativo. |
| `productStatusResponse.status` | A categoria de status atual da tarefa. Consulte a tabela abaixo para obter uma lista de [categorias de status disponíveis](#status-categories) e seus significados correspondentes. |
| `productStatusResponse.message` | O status específico da tarefa, correspondente à categoria de status. |
| `productStatusResponse.responseMsgCode` | Um código padrão para mensagens de resposta do produto recebidas por [!DNL Privacy Service]. Os detalhes da mensagem são fornecidos em `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Uma explicação mais detalhada do status da tarefa. As mensagens para status semelhantes podem variar entre produtos. |
| `productStatusResponse.results` | Para determinados status, alguns produtos podem retornar um valor de `results` objeto que fornece informações adicionais não cobertas por `responseMsgDetail`. |
| `downloadURL` | Se o status da tarefa for `complete`, este atributo fornece um URL para baixar os resultados do trabalho como um arquivo ZIP. Esse arquivo fica disponível para download por 60 dias após a conclusão do trabalho. |

{style=&quot;table-layout:auto&quot;}

### Categorias de status da tarefa {#status-categories}

A tabela a seguir lista as diferentes categorias possíveis de status da tarefa e seu significado correspondente:

| Categoria de status | Significado |
| -------------- | -------- |
| `complete` | O trabalho está concluído e (se necessário) os arquivos são carregados de cada aplicativo. |
| `processing` | As candidaturas reconheceram a tarefa e estão atualmente a ser processadas. |
| `submitted` | O trabalho é submetido a todos os pedidos aplicáveis. |
| `error` | Algo falhou no processamento da tarefa - informações mais específicas podem ser obtidas pela recuperação de detalhes de tarefas individuais. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Um trabalho enviado pode permanecer em um `processing` indicar se tem um trabalho filho dependente que ainda está em processamento.

## Próximas etapas

Agora você sabe como criar e monitorar tarefas de privacidade usando o [!DNL Privacy Service] API. Para obter informações sobre como executar as mesmas tarefas usando a interface do usuário, consulte o [Visão geral da interface do usuário do Privacy Service](../ui/overview.md).
