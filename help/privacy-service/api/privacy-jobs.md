---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Ponto Final da API de Serviços de Privacidade
topic: developer guide
description: Saiba como gerenciar trabalhos de privacidade para aplicativos Experience Cloud usando a API Privacy Service.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 1%

---


# Ponto final de trabalhos de privacidade

Este documento aborda como trabalhar com trabalhos de privacidade usando chamadas de API. Especificamente, ela abrange o uso do ponto de extremidade `/job` na API [!DNL Privacy Service]. Antes de ler este guia, consulte a seção [introdução](./getting-started.md#getting-started) para obter informações importantes que você precisa saber para fazer chamadas à API com êxito, incluindo cabeçalhos necessários e como ler chamadas de exemplo de API.

>[!NOTE]
>
>Se você estiver tentando gerenciar solicitações de consentimento ou recusa de clientes, consulte o [guia de ponto de extremidade de consentimento](./consent.md).

## Lista de todos os trabalhos {#list}

Você pode visualização uma lista de todos os trabalhos de privacidade disponíveis em sua organização, fazendo uma solicitação de GET para o terminal `/jobs`.

**Formato da API**

Esse formato de solicitação usa um parâmetro de query `regulation` no terminal `/jobs`, portanto, ele começa com um ponto de interrogação (`?`), conforme mostrado abaixo. A resposta é paginada, permitindo que você use outros parâmetros de query (`page` e `size`) para filtrar a resposta. Você pode separar vários parâmetros usando os e-mails (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{REGULATION}` | O tipo de regulamento a ser query. Os valores aceitos incluem: <ul><li>`gdpr` (União europeia)</li><li>`ccpa` (Califórnia)</li><li>`lgpd_bra` (Brasil)</li><li>`nzpa_nzl` (Nova Zelândia)</li><li>`pdpa_tha` (Tailândia)</li></ul> |
| `{PAGE}` | A página de dados a ser exibida, usando a numeração com base em 0. O padrão é `0`. |
| `{SIZE}` | O número de resultados a serem exibidos em cada página. O padrão é `1` e o máximo é `100`. Exceder o máximo faz com que a API retorne um erro de código 400. |

**Solicitação**

A solicitação a seguir recupera uma lista paginada de todos os trabalhos em uma Organização IMS, começando na terceira página com um tamanho de página de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de trabalhos, com cada trabalho contendo detalhes como seus `jobId`. Neste exemplo, a resposta conteria uma lista de 50 trabalhos, começando na terceira página de resultados.

### Acessar páginas subsequentes

Para obter o próximo conjunto de resultados em uma resposta paginada, você deve fazer outra chamada de API para o mesmo terminal enquanto aumenta o parâmetro do query `page` em 1.

## Criar um trabalho de privacidade {#create-job}

Antes de criar uma nova solicitação de cargo, é necessário coletar primeiro informações de identificação sobre as pessoas cujos dados você deseja acessar, excluir ou opt out de venda. Depois que você tiver os dados necessários, eles deverão ser fornecidos na carga de uma solicitação de POST para o terminal `/jobs`.

>[!NOTE]
>
>Aplicativos Adobe Experience Cloud compatíveis usam valores diferentes para identificar pessoas de dados. Consulte o guia em [aplicativos Privacy Service e Experience Cloud](../experience-cloud-apps.md) para obter mais informações sobre os identificadores necessários para seus aplicativos. Para obter orientações mais gerais sobre como determinar quais IDs enviar para [!DNL Privacy Service], consulte o documento em [dados de identidade em solicitações de privacidade](../identity-data.md).

A API [!DNL Privacy Service] suporta dois tipos de solicitações de trabalho para dados pessoais:

* [Acesso e/ou eliminação](#access-delete): Acesse (leia) ou exclua dados pessoais.
* [Opt out de venda](#opt-out): Marcar dados pessoais como não vendidos.

>[!IMPORTANT]
>
>Embora as solicitações de acesso e exclusão possam ser combinadas como uma única chamada de API, as solicitações de cancelamento devem ser feitas separadamente.

### Criar um trabalho de acesso/exclusão {#access-delete}

Esta seção demonstra como fazer uma solicitação de trabalho de acesso/exclusão usando a API.

**Formato da API**

```http
POST /jobs
```

**Solicitação**

A solicitação a seguir cria uma nova solicitação de cargo, configurada pelos atributos fornecidos na carga, conforme descrito abaixo.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
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
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Propriedade | Descrição |
| --- | --- |
| `companyContexts` **(Obrigatório)** | Uma matriz que contém informações de autenticação para sua organização. Cada identificador listado inclui os seguintes atributos: <ul><li>`namespace`: A namespace de um identificador.</li><li>`value`: O valor do identificador.</li></ul>É **obrigatório** que um dos identificadores usa `imsOrgId` como seu `namespace`, com seu `value` contendo a ID exclusiva para sua Organização IMS. <br/><br/>Identificadores adicionais podem ser qualificadores de empresa específicos do produto (por exemplo,  `Campaign`), que identificam uma integração com um aplicativo Adobe pertencente à sua organização. Os valores potenciais incluem nomes de conta, códigos de cliente, IDs de locatário ou outros identificadores de aplicativo. |
| `users` **(Obrigatório)** | Uma matriz que contém uma coleção de pelo menos um usuário cujas informações você gostaria de acessar ou excluir. É possível fornecer no máximo 1000 IDs de usuário em uma única solicitação. Cada objeto de usuário contém as seguintes informações: <ul><li>`key`: Um identificador para um usuário que é usado para qualificar as IDs de trabalho separadas nos dados de resposta. É prática recomendada escolher uma string exclusiva e facilmente identificável para esse valor, para que possa ser facilmente referenciada ou pesquisada posteriormente.</li><li>`action`: Uma matriz que lista as ações desejadas para os dados do usuário. Dependendo das ações que você deseja realizar, essa matriz deve incluir `access`, `delete` ou ambos.</li><li>`userIDs`: Uma coleção de identidades para o usuário. O número de identidades que um único usuário pode ter está limitado a nove. Cada identidade consiste em um `namespace`, um `value` e um qualificador de namespace (`type`). Consulte o [apêndice](appendix.md) para obter mais detalhes sobre essas propriedades necessárias.</li></ul> Para obter uma explicação mais detalhada de `users` e `userIDs`, consulte o [guia de solução de problemas](../troubleshooting-guide.md#user-ids). |
| `include` **(Obrigatório)** | Uma matriz de produtos de Adobe para incluir no seu processamento. Se esse valor estiver ausente ou vazio, a solicitação será rejeitada. Inclua somente os produtos com os quais sua organização tem uma integração. Consulte a seção [valores de produto aceitos](appendix.md) no apêndice para obter mais informações. |
| `expandIDs` | Uma propriedade opcional que, quando definida como `true`, representa uma otimização para o processamento das IDs nos aplicativos (atualmente apenas compatível com [!DNL Analytics]). Se omitido, esse valor assumirá `false` como padrão. |
| `priority` | Uma propriedade opcional usada pela Adobe Analytics que define a prioridade para o processamento de solicitações. Os valores aceitos são `normal` e `low`. Se `priority` for omitido, o comportamento padrão será `normal`. |
| `analyticsDeleteMethod` | Uma propriedade opcional que especifica como a Adobe Analytics deve lidar com os dados pessoais. Dois valores possíveis são aceitos para este atributo: <ul><li>`anonymize`: Todos os dados referenciados pela coleção específica de IDs de usuário são tornados anônimos. Se `analyticsDeleteMethod` for omitido, esse é o comportamento padrão.</li><li>`purge`: Todos os dados são completamente removidos.</li></ul> |
| `regulation` **(Obrigatório)** | O regulamento para o trabalho de privacidade. Os seguintes valores são aceitos: <ul><li>`gdpr` (União europeia)</li><li>`ccpa` (Califórnia)</li><li>`lgpd_bra` (Brasil)</li><li>`nzpa_nzl` (Nova Zelândia)</li><li>`pdpa_tha` (Tailândia)</li></ul> |

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
| `jobId` | Uma ID gerada pelo sistema exclusiva e somente leitura para um trabalho. Esse valor é usado na próxima etapa da pesquisa de um trabalho específico. |

Depois de submeter com êxito a solicitação de trabalho, você pode prosseguir para a próxima etapa de [verificar o status do trabalho](#check-status).

## Verifique o status de um trabalho {#check-status}

Você pode recuperar informações sobre um trabalho específico, como seu status de processamento atual, incluindo `jobId` desse trabalho no caminho de uma solicitação de GET para o terminal `/jobs`.

>[!IMPORTANT]
>
>Os dados para trabalhos criados anteriormente só estão disponíveis para recuperação dentro de 30 dias da data de conclusão do trabalho.

**Formato da API**

```http
GET /jobs/{JOB_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{JOB_ID}` | A ID do trabalho que você deseja pesquisar. Essa ID é retornada em `jobId` em respostas de API bem-sucedidas para [criar um trabalho](#create-job) e [listando todos os trabalhos](#list). |

**Solicitação**

A solicitação a seguir recupera os detalhes do trabalho cujo `jobId` é fornecido no caminho da solicitação.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
| `productStatusResponse` | Cada objeto na matriz `productResponses` contém informações sobre o status atual da tarefa em relação a um aplicativo [!DNL Experience Cloud] específico. |
| `productStatusResponse.status` | A categoria de status atual do trabalho. Consulte a tabela abaixo para obter uma lista de [status disponível categoria](#status-categories) e seus significados correspondentes. |
| `productStatusResponse.message` | O status específico da tarefa, correspondente à categoria de status. |
| `productStatusResponse.responseMsgCode` | Um código padrão para mensagens de resposta do produto recebidas por [!DNL Privacy Service]. Os detalhes da mensagem são fornecidos em `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Uma explicação mais detalhada do status do trabalho. As mensagens para status semelhantes podem variar entre os produtos. |
| `productStatusResponse.results` | Para determinados status, alguns produtos podem retornar um objeto `results` que fornece informações adicionais não cobertas por `responseMsgDetail`. |
| `downloadURL` | Se o status do trabalho for `complete`, esse atributo fornecerá um URL para baixar os resultados do trabalho como um arquivo ZIP. Este arquivo está disponível para download por 60 dias após a conclusão do trabalho. |

### Categorias de status do trabalho {#status-categories}

A tabela a seguir lista as diferentes categorias de status possíveis da tarefa e seu significado correspondente:

| Categoria de status | Significado |
| -------------- | -------- |
| `complete` | O trabalho está concluído e (se necessário) os arquivos são carregados de cada aplicativo. |
| `processing` | Os aplicativos reconheceram o trabalho e estão sendo processados no momento. |
| `submitted` | O trabalho é submetido a cada solicitação aplicável. |
| `error` | Ocorreu uma falha no processamento da tarefa - informações mais específicas podem ser obtidas através da recuperação de detalhes da tarefa individual. |

>[!NOTE]
>
>Um trabalho enviado pode permanecer em um estado `processing` se ele tiver um trabalho filho dependente que ainda está sendo processado.

## Próximas etapas

Agora você sabe como criar e monitorar trabalhos de privacidade usando a API [!DNL Privacy Service]. Para obter informações sobre como executar as mesmas tarefas usando a interface do usuário, consulte a [visão geral da interface do usuário do Privacy Service](../ui/overview.md).
